# T09: Servidor fitxers Linux. NFS 

## Introducció
Aquest projecte té com a objectiu resoldre un problema habitual en entorns Linux: la **centralització de dades**. Els nostres clients sovint necessiten una solució que permeti compartir fitxers de manera eficient entre diversos equips.

## Cas Client: DevOptimize Solutions
- **Perfil del client:** Startup de desenvolupament de programari que treballa exclusivament amb Linux.
- **Problema:** El codi font i els actius (documents, scripts) estan dispersos en còpies locals, provocant:
  - Errors de versió constants.
  - Pèrdua d’eficiència en el flux de treball.
- **Requisit:** Implementar un **servidor de fitxers centralitzat** sense autenticació centralitzada.

## Solució proposada
- **Tecnologia:** NFS (Network File System), versió 3.
- **Entorn:** Tot Linux.
- **Objectiu:** Crear una demostració funcional amb:
  - Un **servidor NFS** que comparteixi recursos.
  - Un **client Linux** que consumeixi aquests recursos.

## Tasques principals
1. Configurar el **servidor NFS**:
   - Definir exportacions a `/etc/exports`.
   - Configurar permisos i opcions d’accés.
2. Configurar el **client NFS**:
   - Muntar els recursos compartits.
3. Simular entorn del client:
   - Crear **usuaris i grups**.
   - Demostrar control d’accés amb:
     - Permisos del sistema de fitxers (`chmod`, `chown`).
     - Opcions d’exportació.

## Limitacions
- No hi ha autenticació centralitzada (LDAP, Kerberos).
- Control d’accés basat en permisos locals i configuració N
