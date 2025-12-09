# T09: Servidor fitxers Linux. NFS


##  Fase 1: Preparació de l'entorn

- Un adaptador en NAT i l'altre en Host-Only
- Instal·lem nfs

```bash
sudo apt install nfs-kernel-server
```


## Fase 2: Preparació del servidor

- Creació de Grups: Crear dos grups per al client: devs i admins.

![](img/img02.png)

![](img/img03.png)

- Creació d'Usuaris: Crear un usuari dev01 (membre del grup devs).

![](img/img04.png)

![](img/img05.png)

- Crear un usuari admin01 (membre del grup admins). Creació de Directoris (al Servidor):

![](img/img06.png)

![](img/img07.png)

- Crear el directori per als projectes de desenvolupament: /srv/nfs/dev_projects

![](img/img09.png)

- Crear el directori per a les eines d'administració: /srv/nfs/admin_tools
  
![](img/img10.png)

- Permisos del Servidor (El punt clau):

  Es vol que els developers tinguin control total sobre els seus projectes, i que  admins tinguin control total sobre les      seves eines. En tots dos casos el propietari sera `root`

![](img/img11.png)

![](img/img12.png)

  
- Com a pas final, s'instal·laran els paquets necessaris per al servei NFS al servidor i es configurarà l'exportació dels directoris amb les opcions adequades.

![](img/img13.png)

![](img/img14.png)


## Fase 3: L'Exportació d'Administració (El Dilema del root_squash)

Problema:
Root del client no pot escriure al directori NFS perquè s’aplica root_squash, que redueix els privilegis per seguretat.

Solució:
Afegir l’opció no_root_squash a l’exportació NFS. Això permet que root del client mantingui privilegis i pugui crear fitxers com a root.

![](img/img27.png)


## Fase 4: L'Exportació de Desenvolupament (Permisos rw vs ro)
Abans de tot intal·lem el servei nfs
![](img/img15.png)
Crearem els grups i usuaris amb els mateixos UID i GID que el server

![](img/img22.png)

![](img/img23.png)

![](img/img24.png)

![](img/img25.png)

Objectiu:
Configurar /etc/exports amb dues exportacions del mateix directori:

Xarxa d’administració (192.168.56.0/24) → escriptura.

Xarxa de consultors (192.168.56.100) → només lectura.

Proves:

Muntar a /mnt/dev_projects i escriure com dev01 → ha de funcionar.

![](img/img19.png)

![](img/img20.png)

Canviar IP a 192.168.56.100, provar d’escriure → només lectura.

Canviar usuari a admin01, provar d’escriure → falla (no és al grup devs).


## Fase 5: Muntatge Automàtic amb /etc/fstab

Objectiu:
Configurar el client perquè munti automàticament els recursos NFS a /mnt/admin_tools i /mnt/dev_projects en iniciar el sistema.
Passos:

Editar /etc/fstab i afegir les entrades NFS corresponents.

![](img/img26.png)

Executar mount -a per provar sense reiniciar.

![](img/img28.png)
