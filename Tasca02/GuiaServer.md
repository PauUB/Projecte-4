# Part 2 – Guia pas a pas: Còpia de seguretat servidor Linux amb Duplicity

## Objectiu
Implementar i provar una política de còpies de seguretat en un **servidor Linux (Ubuntu Server)** utilitzant **Duplicity** i **cron**, amb còpies completes i incrementals sobre una unitat externa muntada només durant el procés de backup.

---

## PAS 1. Preparar la màquina virtual
1. Crear una **màquina virtual Ubuntu Server**.
2. Afegir un **segon disc de 10 GB** (simula unitat externa).
3. Iniciar el sistema i accedir com a usuari amb permisos `sudo`.

---

## PAS 2. Inicialitzar i formatar el disc auxiliar
1. Identificar el disc:
```bash
lsblk
```
2. Suposant que és `/dev/sdb`, crear sistema de fitxers **XFS**:
```bash
sudo mkfs.xfs /dev/sdb
```
3. Crear el punt de muntatge:
```bash
sudo mkdir /media/backup
```
4. Muntar manualment el disc:
```bash
sudo mount /dev/sdb /media/backup
```
5. Verificar:
```bash
df -h | grep backup
```

---

## PAS 3. Instal·lar Duplicity
1. Actualitzar repositoris:
```bash
sudo apt update
```
2. Instal·lar duplicity:
```bash
sudo apt install duplicity -y
```
3. Comprovar instal·lació:
```bash
duplicity --version
```

---

## PAS 4. Crear usuaris i dades de prova

### 4.1 Crear usuaris
```bash
sudo adduser user1
sudo adduser user2
```

### 4.2 Crear arxius de 10 MB
1. Com a usuari principal:
```bash
cd ~
```
2. Crear 4 fitxers de 10 MB:
```bash
fallocate -l 10M fitxer1.bin
fallocate -l 10M fitxer2.bin
fallocate -l 10M fitxer3.bin
fallocate -l 10M fitxer4.bin
```

---

## PAS 5. Còpia de seguretat completa de /home

1. Definir passphrase:
```bash
export PASSPHRASE=contrasenyaSegura
```
2. Executar còpia completa:
```bash
duplicity /home file:///media/backup/home_backup
```
3. Verificar contingut:
```bash
ls /media/backup/home_backup
```

---

## PAS 6. Restauració de dades

1. Esborrar els arxius creats:
```bash
rm ~/fitxer*.bin
```
2. Restaurar des de la còpia:
```bash
duplicity restore file:///media/backup/home_backup /home
```
3. Comprovar que els fitxers s’han recuperat correctament.

---

## PAS 7. Còpia incremental

1. Crear un nou fitxer de 4 MB:
```bash
fallocate -l 4M noufitxer.bin
```
2. Tornar a executar duplicity:
```bash
duplicity /home file:///media/backup/home_backup
```
3. Observar que la còpia és **incremental**.

4. Desmuntar la unitat:
```bash
sudo umount /media/backup
```

---

## PAS 8. Script de còpia completa (fullbackup.sh)

1. Crear l’script:
```bash
sudo nano /usr/local/bin/fullbackup.sh
```

2. Contingut de l’script:
```bash
#!/bin/bash
export PASSPHRASE=contrasenyaSegura
mount /dev/sdb /media/backup
duplicity full /home file:///media/backup/home_backup
umount /media/backup
```

3. Donar permisos:
```bash
sudo chmod +x /usr/local/bin/fullbackup.sh
```

---

## PAS 9. Programar còpia completa amb cron

1. Editar cron de root:
```bash
sudo crontab -e
```
2. Afegir:
```cron
0 23 * * 0 /usr/local/bin/fullbackup.sh
```

---

## PAS 10. Script de còpia incremental (incrementalbackup.sh)

1. Crear l’script:
```bash
sudo nano /usr/local/bin/incrementalbackup.sh
```

2. Contingut:
```bash
#!/bin/bash
export PASSPHRASE=contrasenyaSegura
mount /dev/sdb /media/backup
duplicity /home file:///media/backup/home_backup
umount /media/backup
```

3. Donar permisos:
```bash
sudo chmod +x /usr/local/bin/incrementalbackup.sh
```

---

## PAS 11. Programar còpies incrementals amb cron

1. Editar cron de root:
```bash
sudo crontab -e
```
2. Afegir:
```cron
0 23 * * 1-6 /usr/local/bin/incrementalbackup.sh
```

---

## Resultat final
- ✔ Còpies completes els diumenges a les 23:00.
- ✔ Còpies incrementals de dilluns a dissabte.
- ✔ Disc de backup desmuntat per defecte.
- ✔ Restauració verificada correctament.

**Guia tècnica completada amb èxit.**
