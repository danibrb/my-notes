
modelli e algoritmi delle interazioni
no gradi elettronici, approssimazione Born-Oppenheimer
risposta rapida degli elettroni (stato fondamentale)
o risolvi esplicitamente Schrodinger (ab-initio) oppure usi potenziali efficaci

#### force fields

insieme di forme funzionale e parametri che descrivono il sistema
limite: non si possono fare processi che prevedono trasferimento di carica tra una molecola e l'altra
pro: riusciamo a simulare per tempi piu lunghi (ms) se faccio ab-initio ho solo ns
si sceglie classica o ab-initio iin base alle necessita

#### sviluppo di campo di forze (force fields)

1. selezione di modelli appropriati: quali interazioni vogliamo riprodurre?
	1. a corto / lungo range
	2. molecole polarizzabili o meno
	3. criteri di scelta: intuizione chimico fisica, scopo finale
2. selezione delle forme funzionali per descrivere quel tipo di fisica
	1. interazione a multicorpi / due corpi
	2. scelta compromesso tra affidabilita e efficenza
3. selezione delle condizioni e proprieta target termodinamiche
	1. es transizioni di fase
4. parametrizzazione
	1. deve fare qualche tipo di fit per trovare valori adatti dei parametri
	2. manuale, automatica, machine learning
5. validazione
	1. devo vedere quanto bene è in grado il mio modello di riprodurre proprieta che non avevo gia pianificato (per capire i limiti del modello)
	2. trasferibilita del modello (faccio in modo che il mio modello non sia pessimo anche in un contesto diverso da quello pianificato)

### force fields classici

#### atomistici

ho due possibilita
- tutti gli atomi del sistema
- atomi di H associati a C non vengono descritti (C + H unico centro di interazione)
diciamo cose che valgono per entrambi
1. interazione di legame (intramolecolari)
2. interazioni di non legame (intramolecolari e intermolecolari)

nello specifico ho 
(1)
- di legame (2 corpi)
- di angolo (3 corpi)
- di angolo torsionale (4 corpi) angolo tra il piano definito dalla prima tripletta e quello della seconda

(2)
- interazione coulombiana (corto o lungo range)
- van der waals (corto raggio)
(1)
(a) potenziale armonico o di Morse (consente la rottura del legame) $\sim 10^2 \text{ kcal/ molÅ}^2$ 200 - 700
(b) funzione quadratica in $\theta$ o nel $\cos \theta$ 
gradi di liberta abbastanza ripidi
facendo una stima $$\Delta x_{\text{rms}} \sim 0,039 \text{ Å} \text{ di legame} \quad \Delta \theta_{\text{rms}} \sim 7,7^\circ \text{ di angolo}$$
sono variazioni piccolissime, la piu significativa è la terza:
(c) sono effettivamente superabili
serie di coseni: cosi ho una serie du minimi che hanno barriere che conservano passaggio da un minimo a un altro, ho piu configurazioni metastabili
ogni termine ha un riferimento di equilibrio ma si influenzano tra di loro (non sono gli equilibri della configurazione completa) e ci sono interazioni no di legame
(2)(d) espansione multipoli
- problema di convergenza: non è chiaro quanti termini sono necessari, dipende da distanza molecolare, probabilita sistema di riferimento in cui costruisco il tensore di quadripolo
- inoltre questa espansione è valida solo se a grandi distanze, ma qua non lo siamo (magari in un gas si, in un liquido no)
- per molecole molto grandi?
- cariche parziali: possono essere anche frazionarie a ciascuna molecola vengono attribuite cariche anche frazionarie sui nuclei degli atomi delle molecole o no. come le misuro? non è un'osservabile la carica
(1) come assegniamo i parametri? con algoritmi ab-Initio struttura elettronica con molecola nel vuoto
posso usare ab initio per ottenere una carica? si output densita di carica in tutti i punti della molecola
$$\Phi(\vec{r}) = \Phi_{\text{nucl}} + \Phi_{\text{ele}}$$
voglio assegnare a delle posizioni predefinite delle cariche parziali che generino un campo piu simile a questo qui
![[Pasted image 20260718110338.png]]
caso semplice, conosciamo la distribuzione
fitto $$\phi^0(\vec{r}) \rightarrow \phi^0(\vec{x}_i)$$
piazzo N punti i = 1, 2, ... , N
$$\phi^{\text{calc}}(\vec{x}_i)$$
calcolato attribuendo una carica parziale ne due punti discreti attorno alla molecola
campio i valori delle due cariche parziali per avere la miglior rappresentazione del mio potenziale vero
i punti possono avere ?? diverso in base a se sono alla distanza tipica
carica complessiva molecola: nota
vogliamo assegnare N cariche parziali 
vogliamo minimizzare
$$R = \sum_{i=1}^{N_{\text{points}}} w_i \left( \phi_i^0 - \phi_i^{\text{calc}} \right)^2$$
$$\frac{\partial R}{\partial q_k} = 0 = -2 \sum_{i=1}^{N_{\text{points}}} w_i \left( \phi_i^0 - \phi_i^{\text{calc}} \right) \left( \frac{\partial \phi_i^{\text{calc}}}{\partial q_k} \right) = 0$$
$$\frac{\partial \phi_i^{\text{calc}}}{\partial q_k} = \frac{\partial}{\partial q_k} \left( \sum_{j=1}^{N-1} \frac{q_j}{4\pi\varepsilon_0 r_{ij}} + \underset{\substack{\text{non dipende da } k}}{\cancel{\frac{Z}{4\pi\varepsilon_0 r_{iN}}}} - \sum_{j=1}^{N-1} \frac{q_j}{4\pi\varepsilon_0 r_{iN}} \right) =$$
$$= \frac{1}{4\pi\varepsilon_0 r_{ik}} - \frac{1}{4\pi\varepsilon_0 r_{iN}} = \frac{1}{4\pi\varepsilon_0} \left( \frac{1}{r_{ik}} - \frac{1}{r_{iN}} \right)$$
$$\frac{\partial R}{\partial q_k} = 0 \quad \rightarrow \quad \sum_{i=1}^{N_{\text{points}}} w_i \left( \phi_i^0 - \phi_i^{\text{calc}} \right) \left( \frac{1}{r_{ik}} - \frac{1}{r_{iN}} \right) = 0$$
$$\rightarrow \quad \sum_{i=1}^{N_{\text{points}}} w_i \left( \phi_i^0 - \left[ \sum_{j=1}^{N-1} \frac{q_j}{4\pi\varepsilon_0 r_{ij}} + \frac{Z}{4\pi\varepsilon_0 r_{iN}} - \sum_{j=1}^{N-1} \frac{q_j}{4\pi\varepsilon_0 r_{iN}} \right] \right) \left( \frac{1}{r_{ik}} - \frac{1}{r_{iN}} \right) = 0$$
risulta lineare in qj: scriviamolo come sistema lineare in N-1 variabili incognite e abbiamo fatto
$$$$
$$\begin{aligned}
\sum_{i=1}^{N_{\text{points}}} w_i \left( \phi_i^0 - \frac{Z}{4\pi\varepsilon_0 r_{iN}} \right) &\left( \frac{1}{r_{ik}} - \frac{1}{r_{iN}} \right) \underset{\substack{\uparrow \\ \text{posso invertire} \\ \text{le due somme} \\ \text{(indipendenti)}}}{=} \\
&= \sum_{i=1}^{N_{\text{points}}} w_i \sum_{j=1}^{N-1} q_j \left( \frac{1}{4\pi\varepsilon_0 r_{ij}} - \frac{1}{4\pi\varepsilon_0 r_{iN}} \right) \left( \frac{1}{r_{ik}} - \frac{1}{r_{iN}} \right)
\end{aligned}
$$

sistema lineare di N-1 equazioni una $\forall \ \frac{\partial R}{\partial q_k}$ al variare di k in N-1 incognite $q_j$
$\phi_i^0$ la ottengo da un sistema che mi calcola il potenziale ab initio
se ho un cambio funzionale importante nella molecola, se rifacessi il calcolo ab initio potrei ottenere $\phi_i^0$ diverso quindi la mia minimizzazione potrebbe non essere piu vera
compromesso: posso cercare il mimino tra piu conformazioni e pesarle
(2)(e) forze di dispersione (di van der waals)
interazione tra dipoli oscillanti $$\propto \frac{1}{r^6}$$
corto raggio
descritta da potenziale di lennar Jones
si vede anche il diagramma di fase
se sono presenti tanti tipi di atomi diversi, parametri di LJ omogenei tra atomi uguali e eterogenei tra quelli diversi
di solito si assegnano prima quelli omogenei (proprieta target) e quelli eterogenei
$$\sigma_{AB} = \frac{\sigma_A + \sigma_B}{2} \qquad \varepsilon_{AB} = \sqrt{\varepsilon_A \varepsilon_B}$$

#### acqua

esistono tanti modelli
consideriamo modelli
- rigidi (sbarrette rigide tra H e O)
- non polarizzabili (cariche parziali non cambiano una volta assegnate)
vediamo due modelli a tre siti di interazione TIP3, SPC/E
in realta considero LJ solo per O-O
cariche spaziali su O e su H
i due modelli hanno parametri molto diversi
target per parametrizzare
- densita
- entalpia di vaporizzazione ($\Delta$H tra molecola nel vuoto e in fase liquida) in un caso si tiene conto dell'energia di costo per la modifica della forma del dipolo
- angolo di legame
altri modelli:
- TIP4P: centro di interazione LJ su O ma carica parziale non proprio su O
- TIP5P: 5 cariche parziali 2 nuvole elettroniche (q negativa), segue intuizione chimica
vediamo come riproducono altre proprieta:
- proprieta interfaccia migliore per SPC/E perche $\sigma$ migliore
- $\rho \rightarrow$  era target, tutte buone ???
- $T_{fusione}$ solo TIP5P funziona
- pendenza della curva di coesistenza solido-liquido $\frac{dp}{dT}$ è sempre negativa (ok) ma con valori molto diversi (TIP5P sbagliatissima)
non esiste un modello perfetto, ma se teniamo conto di tutta la fisica simuliamo troppo poco (pochi ns)