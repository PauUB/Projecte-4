# T01: DRP: còpies de seguretat. Estudi cas client (treball cooperatiu)

---

### 1. Què copiar? (Priorització)
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

### **2. Periodicitat i Tipus de Còpia**

**Bases de dades (Comptabilitat i Clients):**
Còpies incrementals o de logs cada 4 hores (per garantir RPO < 4 h).
Còpia completa cada nit.
Còpia completa setmanal i mensual per disposar d’històric ampli.

**Documents de projectes i carpetes personals:**
Còpia incremental diària (optimitza espai i temps).
Còpia completa setmanal i mensual per punts de restauració sòlids.

### **3. Mitjans i Ubicació (Regla 3-2-1)**

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

---

## Fase 2: Treball per trio

| Element | Proposta del trio | Justificació |
| :-- | :-- | :-- |
| Dades Crítiques | Bases de Dades de Comptabilitat i Clients | Són essencials per al funcionament diari i canvien sovint |
| Periodicitat (BD) | Cada 4 hores (incremental) + còpia completa diària | Permet recuperar fins a l’última actualització sense perdre més de 4 h |
| Tipus de Còpia (BD) | Incremental + Completa | Redueix temps i espai de còpia |
| Mitjà 1 (Local) | NAS dins de la sala de servidors | Accés ràpid per a recuperacions menors |
| Mitjà 2 (Extern) | Cloud (Google Cloud) | Garantia d’una còpia fora de lloc, segura i automàtica |

---

## Fase 3: Treball en grup

1. Debat i selecció
Després de compartir les propostes, hem coincidit que el NAS local i el núvol són la millor combinació qualitat-preu. Les cintes LTO serien més segures a llarg termini, però massa cares per l’empresa.
2. Política final de còpies de seguretat

### Dades objecte de còpia

Servidor:
    - Comptabilitat i Clients (crítiques): còpia incremental cada 4 h, completa cada dia.
    - Projectes i plànols (no crítiques): còpia diferencial diària i completa setmanal.
Equips clients: només els documents importants de cada tècnic (sincronitzats un cop al dia amb el servidor).


### Cronograma setmanal detallat

| Dia | Dades | Tipus de còpia | Mitjà |
| :-- | :-- | :-- | :-- |
| Dilluns | BD i Documents crítics | Completa | NAS |
| Dimarts | BD | Incremental | NAS |
| Dimecres | BD i Documents | Diferencial | NAS |
| Dijous | BD | Incremental | NAS |
| Divendres | BD i Documents | Diferencial | NAS |
| Dissabte | BD | Incremental | Cloud |
| Diumenge | Tot (completa) | Completa | Cloud |

### Elecció de mitjans i ubicació (regla 3-2-1)

Mitjà 1 (Local): NAS intern amb discs redundants.
Mitjà 2 (Extern): Còpia automàtica al núvol (Google Cloud).
Ubicació fora de lloc: còpia al núvol gestionada pel responsable de seguretat.


### Estratègia de recuperació (RTO/RPO)

RTO (Temps de recuperació): Les còpies al NAS permeten restablir bases de dades en menys de 4 h.
RPO (Pèrdua màxima de dades): Còpies incrementals cada 4 h asseguren una pèrdua màxima de només aquest marge.
