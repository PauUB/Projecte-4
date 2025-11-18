# T01: DRP: còpies de seguretat. Estudi cas client (treball cooperatiu)

---

## 1. Què copiar? (Priorització)
**Màxima prioritat:**
Bases de dades de Comptabilitat i Clients (20 GB, ús constant).
No poden perdre més de 4 hores de treball.

**Segona prioritat:**
Documents de projectes (plànols, especificacions tècniques).
Carpetes personals dels usuaris.
Canvis poc freqüents; es pot admetre una pèrdua de fins a 24 hores.

**Equips clients (10 Windows):**
No cal còpia completa.
Els fitxers importants han d’estar centralitzats al servidor.
Recomanació: aplicar polítiques perquè tot el treball es guardi al servidor, evitant backups locals.

## **2. Periodicitat i Tipus de Còpia**

**Bases de dades (Comptabilitat i Clients):**
Còpies incrementals o de logs cada 4 hores (per garantir RPO < 4 h).
Còpia completa cada nit.
Còpia completa setmanal i mensual per disposar d’històric ampli.

**Documents de projectes i carpetes personals:**
Còpia incremental diària (optimitza espai i temps).
Còpia completa setmanal i mensual per punts de restauració sòlids.

## **3. Mitjans i Ubicació (Regla 3-2-1)**

Solució recomanada:
NAS local → restauracions ràpides i gran capacitat.
Còpia al núvol → protecció davant desastres físics (incendis, robatoris, ransomware).
Discs externs → suport addicional per còpies mensuals, amb rotació i emmagatzematge en lloc segur extern.

No recomanat: cintes magnètiques (cost elevat i gestió complexa).

Regla 3-2-1:
3 còpies de cada dada.
2 tipus de mitjans diferents.
1 còpia fora de la ubicació principal.
Amb servidor original + NAS local + còpia al núvol, la regla queda complerta.
