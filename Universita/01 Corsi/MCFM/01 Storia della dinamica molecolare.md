
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

