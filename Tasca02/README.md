# T02: DPR: còpies de seguretat. Cas pràctic

## Introducció al cas

Després de dissenyar una política de còpies de seguretat per al client *Muntatges i Serveis Tècnics SL*, ara cal implementar-la amb guies tècniques i proves de concepte perquè el personal pugui aplicar el pla.

---

### Part 1: Còpia de seguretat en equips Windows
- **Excepció**: fer còpia de l’equip Windows del director (informació sensible fora del servidor).
- **Política**: esquema **3-2-1**:
  - **Còpia local**: disc secundari del mateix equip.
  - **Còpia al núvol**: Google Drive amb **Duplicati**.
- **Prova de concepte**:
  - Crear VM Windows 11 amb dos discos (SO + disc secundari de 10 GB).
  - Simular Google Drive amb un compte específic.
- **Configuració**:
  - Còpia del perfil d’usuari **cada hora** al disc secundari.
  - Còpia **a les 18:00** a Google Drive.
- **Tasques**:
  - Instal·lar i configurar Duplicati.
  - Afegir arxius a *Documents*, fer còpies, esborrar i restaurar des del disc i des del núvol.

---

### Part 2: Còpia de seguretat en servidor Linux
- **Eina**: **Duplicity** + **cron** per automatitzar.
- **Prova de concepte**:
  - Crear VM Ubuntu Server amb segon disc de 10 GB.
  - Formatar en **XFS** i muntar a `/media/backup`.
  - Instal·lar duplicity.
  - Crear usuaris i arxius (4 fitxers de 10 MB).
  - Fer còpia de `/home`, esborrar i restaurar.
  - Afegir nou arxiu (4 MB) i comprovar còpia incremental.
- **Automatització**:
  - **Scripts**:
    - `fullbackup.sh`: còpia completa amb variable d’entorn `PASSPHRASE`.
    - `incrementalbackup.sh`: còpia incremental.
  - **Programació amb cron**:
    - Full backup: diumenge 23:00.
    - Incremental: dilluns-dissabte 23:00.
  - Important: muntar unitat abans i desmuntar després de cada còpia.

