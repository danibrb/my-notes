
### Un paper rivoluzionario (1957)

-  la MD storicamente nasce nel 1957
- studio collisioni elastiche di sfere rigide (Alder e Wainwright)
	- analisi fenomeni di rilassamento
	- dimostrazione esistenza transizione di fase solido-liquido
	- potenziale discontinuo
	- $$V_{HS}(r) = \begin{cases} \infty, & r < \sigma \\ 0, & r \ge \sigma \end{cases}$$
	- nessuna interazione attrattiva
	- repulsione infinita a corto raggio

### Evoluzione storica

- superamento potenziale discontinuo verso quelli continui
- sfere rigide (Alder, 1957)
- Lennard-Jones (Rahman, 1964)
- acqua (Rahman and Stillinger, 1971)
	- interazioni intra-molecolari e inter-molecolari
	- concetto di force field
- idrocarburi flessibili (Ryckaert and Bellesman, 1975)
- polimeri (Binder, 1995)
- nanoparticelle e biomolecole, oggi

I campi di applicazione spaziano dalla chimica, fisica scienza dei materiali

### La Transizione tra Dinamica Classica e Ab Initio

#### MD classico

- non siamo interessati alla descrizione del moto degli elettroni
- per trascurare il comportamento quantistico dei nuclei atomici devo avere $$k_B T \gg \hbar\omega \quad \rightarrow \quad T \gg \frac{\hbar\omega}{k_B}$$
- ==energia termica del sistema ($k_B T$)  >> spaziatura energetica tra i livelli vibrazionali discreti dei modi nucleari ($\hbar\omega$)
- **Esempio 1: Fluido di Argon (Lennard-Jones)**
- oscillazioni armoniche di un atomo di argon in una buca LJ $$\omega = \sqrt{\frac{72\epsilon}{m r_0^2}}$$
- parametri classici dell'Argon ($\epsilon = 0.01\text{ eV} \approx 120\text{ K}$, $r_0 = 3.71\text{ Å}$, $m = 40\text{ amu}$), si ottiene una frequenza d'oscillazione $\omega \approx 3.6 \times 10^{12}\text{ s}^{-1}$
- ottengo soglia di temperatura classica pari a:

$$T \gg 27\text{ K}$$
- a temperatura ambiente l'argon si trova nel regime classico

- **Esempio 2: Solido Cristallino Metallico (fcc)**
- In un solido cristallino, i moti collettivi dei nuclei (fononi) presentano uno spettro di frequenze limitato superiormente dalla frequenza di Debye $\omega_D$
- limite classico per la simulazione di un solido cristallino si riduce alla condizione $T \gg \Theta_D$, dove $\Theta_D$ è la temperatura di Debye del metallo
	Au → 165 K
	Ag → 225 K
	Cu → 343 K

#### Ab Initio MD

- considero i gradi di libertà elettronici
- rottura e formazione di legami chimici, trasferimento di carica
- si risolvono le equazioni di Schrodinger

### Architettura dell'algoritmo MD classico

- integrazione numerica delle equazioni del moto di Newton
- ho N particelle interagenti
- posso definire diversi scenari (ensemble)
- **Microcanonico** (NVE) 
	- sistema isolato termicamente e meccanicamente
- **Canonico** (NVT) 
	- sistema scambia calore con un termostato
- **Isotermico-Isobarico** (NPT)
	- il volume fluttua per mantenere P costante tramite barostato
- **Aperto** 
	- il numero di particelle varia (es crescita)
#### Diagramma di flusso

1. inizializzazione posizioni e velocità $r_i$ e $v_i$
2. calcolo forze al tempo t $F_i(t)$
3. aggiornamento posizioni e velocità al tempo t + dt
4. output, ritorno al punto 2

- la scelta del passo dt avviene tramite un compromesso
	- troppo piccolo -> si allungano i tempi computazionali
	- troppo grande -> errori su integrazione che potrebbe divergere
- di solito si prende 10 volte più piccolo del periodo vibrazionale più veloce del sistema

- Nelle molecole organiche, i moti più rapidi sono associati allo stretching dei legami covalenti leggeri, come i legami carbonio-idrogeno : $\tau_{C-H} \approx 10\text{ fs} \quad \rightarrow \quad \Delta t \le 1\text{ fs}$
- per l'argon abbiamo $\tau_{Ar} \approx 1.7\text{ ps} \quad \rightarrow \quad \Delta t \le 10\text{ fs}$
- limite inferiore dovuto alla precisione del formato dei dati
- singola precisione 32bit -> $10^{-4}$ e $10^{-5}\text{ fs}$
- doppia precisione 64bit -> $10^{-6}$ e $10^{-8}\text{ fs}$
- valori tipici di step sono:
	- 1 - 2 fs per biomolecole
	- 0.5 - 1 fs per sistemi con alte frequenze vibrazionali (acqua)

#### 1 Inizializzazione

- si leggono le posizioni iniziali da un file $\{r_i(t=0)\}_{i=1,N}$
- eventualmente si leggono le velocità iniziali da un file $\{v_i(t=0)\}_{i=1,N}$ se disponibili ad esempio da una simulazione precedente
- se non sono disponibili, le generiamo secondo una distribuzione gaussiana
- $$g(v)=f(v_x)f(v_y)f(v_z)$$$$f(v_x)=\left( \frac{m}{2\pi k_B T} \right)^{1/2}e^{-\dfrac{mv^2_x}{2k_BT}}$$
- estraiamo con box muller $\vec{v}^{\,BM}_i$
- si rimuove il moto del centro di massa $$\{\vec{v}^*_i = \vec{v}^{\,BM}_i - \vec{v}^{\,CM}\}_{i=1,N}$$
- calcoliamo l'energia attuale del sistema $$K^* = \frac{1}{2} m \sum_i v_i^{*2}$$
- scaliamo le velocità per ottenere l'energia desiderata $$v_i = v_i^* \sqrt{\frac{K}{K^*}}$$
- l'energia target può essere ottenuta da K = E - U(t=0)
- nel caso di simulazione NVT $K = \frac{3}{2} N k_B T$

#### 2 Calcolo delle forze

- per un potenziale di coppia, serve un doppio loop, dispendioso a livello computazionale
- possiamo usare dei trucchi per alleggerire i calcoli
- terza legge di Newton, sfruttando la simmetria delle forze $\vec{f}_{ij} = -\vec{f}_{ji}$, si dimezza il numero di valutazioni necessarie nel ciclo di calcolo
- le interazioni a corto raggio decadono rapidamente, introduciamo un *cut-off*
	- riduciamo il loop interno a un loop con i primi vicini

#### 3 Propagazione della traiettoria

$$r_i(t), v_i(t), \mathbf{F}_i(i) \rightarrow r_i(t + \delta t), v_i(t + \delta t)$$
- Accuratezza
	- le predizioni di MD vanno interpretate come statistiche
- Conservazione dell'energia
	- piccole fluttuazioni sono ammesse, no drift
- Efficienza
	- calcolo delle forze una volta per time step
- Uso della memoria non esagerato