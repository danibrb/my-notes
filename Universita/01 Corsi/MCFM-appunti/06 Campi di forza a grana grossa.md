
modelli a grana grossa a corto raggio
es polimero poliestre
rosso O bianco H verde legami C
interazioni di legame intramolecolari e non di legame
riduciamo il numero di atomi
cambia l'aspetto della superficie di energia libera e potenziale
scomponigli stati metastabili le barriere superficie piu smooth
conseguenze
- meno gradi di liberta meno integrali
- vibrazioni veloci che livitano il time step, ora sono piu lente, time step maggiori
- il sistema ha una dinamica piu veloce nella superficie a grana grossa
differenze nello sviluppo dei force fields
- trascuro interazioni a lungo range
- selezione delle proprieta target: difficilmente vengono da simulazioni ab initio e quelle da risoluzioni atomistiche (diverso da quanto visto precedentemente) target sperimentali anche qua (possiamo usare il ML)

#### interazioni a lungo range

noi abbiamo simulato particella nel vuoto: condizioni al contorno non considerate
se voglio simulare unaparte di un volume?
idea 1: ci metto un muro impenetrabile (urti elastici)
V 1L $10^{25}$ molecole d'acqua
molecole la cui dinamica è influenzata dalle pareti $10^{10}$ ok
ma per 1000 molecole tutte sono influenzate, non va bene
idea 2: condizioni periodiche al contorno
simulo infinite copie adiacenti della box di simulazione
- gestione posizione particelle easy
- gestione forze e distanze interazione: prendo distanza piu piccola di meta del box
interazione coulombiana di lungo range
(1) la si puo sempre troncare:
problemi tecnici:
- approssimazione non sempre possibile
![[Pasted image 20260718171459.png]]
![[Pasted image 20260718171509.png]]

interazione solo con particelle all'interno:
- per LJ buona approssimazione
- per lungo range no
mi da problemi con la conservazione dell'energia (se la particella esce dal $r_{cut-off}$  prima la conto poi sparisce)
mi da problemi anche con le forze
se io unisco i due potenziali 
![[Pasted image 20260718171758.png]]
per calcolare la derivata: non banale (forse numericamente riesco a cavarmela)

(2) coulomb: per ogni atomo con carica frazionaria calcolo interazione coulombiana
complessivamente scatola neutra
$$U_{\text{cell}} = \frac{1}{2} \sum_j q_j V(\vec{r}_j)$$
potenziale coulombiano generato da dentro la cella e da tutte le immagini periodiche (pbc)
densita di carica del sistema
$$\rho(\vec{r}) = \sum_{m} \sum_{j \in m} q_j \underset{\substack{\uparrow \\ \text{carica locale} \\ \text{(picco)}}}{\delta(\vec{r} - \vec{r}_j)}$$
equazione di poisson
$$\nabla^2 V(\vec{r}) = -4\pi\rho(\vec{r})$$
nota $\rho(\vec{r})$ ad ogni istante mi ricavo V
vale anche nello spazio reciproco
pero le cariche piccate hanno una FT che converge male
problema risolto da EWALD
![[Pasted image 20260718172600.png]]

distribuzioni gaussiane piccate nelle $\delta$      ---> delta originali piu gaussiane che annullano le altre
cosi si ottiene la convergenza: nello spazio reciproco e in quello diretto
ci sono poi dei termini correttivi che non vediamo troppo bene
costo computazionale $N^2$
soluzione FFT con una discretizzazione dello spazio (cariche su griglia) -> NlogN
PME Particle Mesh Ewald
la usiamo per simulazione in acqua

Appunti esperienza NPT:

coulomb type : 
PME non taglia bruscamente, oscillazioni piccole e T desiderata
Cut-off:
- taglia bruscamente
- discontinuita
- le forze sono giganti
- energie cinetiche grandi
- T grandi
il termostato cerca di compensare cio e di portare il sistema alla T desiderata
-> grandi fluttuazioni
se aumentassi il tempo di simulazione forse il termostato riuscirebbe a raggiungere la T desiderata ma resterebbero le fluttuazioni
per l'errore guarda RMSD perche errore probabilmente sopravvalutato
