
il sistema con la dinamica di Langevin
ha come differenza che descriviamo il sistema con la dinamica di langevin
gia nominato nel termostato
$$m \frac{d^2 x}{d t^2} = -m \gamma \frac{d x}{d t} - \frac{d U}{d x} + \zeta(t)$$

$\zeta(t)$ rumore bianco -> interazione con il bagno termico
cosi teniamo esplicitamente conte di un solvente in cui si sposta il mio sistema esempio proteina nell'acqua
limiti in cui sta il sistema
$\gamma \rightarrow 0$ poco smorzamento (dissipazioni), moto conservativo, 
energia termica < barriera
tanto tempo per superare la barriera
$\gamma \rightarrow \infty$ ambiente estremamente perturbato dalla dinamica del sistema
calcoli casuali ostacolano superamento della barriera (mandano le particelle in direzioni casuali)
in entrambi i casi $r \rightarrow 0$
$$\frac{k_{\text{Kramer}}}{k_{\text{TST}}}$$
rapporto tra prefattori

c'è un fattore di $\gamma$ per cui riesco a massimizzare il rate
TST sovrastima sempre il rate, non tiene conto del passaggio per percorsi sfavoriti energeticamente, non tiene conto della possibilita di tornare indietro per il sistema dovuto al solvente
kramer per $\gamma \rightarrow 0$ traiettorie balistiche (salti lunghi)
puo succedere di saltare non ai minimi vicini
non è facile stimare i prefattori
noi ci concentriamo sul calcolare l'altezza della barriera Ea o $\Delta F$
ora cerchiamo dove sono e quanto sono profondi i minimi
e quanto sono alti i punti di transizione (di sella)

### ottimizzazione globale

cercare il mimino globale di una funzione (PES)
l'algoritmo deve lavorare senza informazioni a priori tranne sul numero di particelle interagenti e interazioni
deve trovare piu funnel possibili
famiglie di minimi che si assomigliano
inoltre deve trovare il fondo del funnel
non richiesta del campionamento statistico dell'enseble
non mi interessano le condizioni termodinamiche
algoritmi classificati in due famiglie
- stocastici o termodinamici (SA, basin hopping)
- euristici (genetici)

#### Simulated annealing SA

simulazione di una rampa in T del sistema
sistema inizializzato a una T alta e poi raffreddato
(tipo come abbiamo fatto in MD)
parto da T alta, sono a energie alte
quando inizio a scendere, molto piu probabilmente finiro nel funnel principale
se pero raffreddo piano ho piu probabilita di superare la barriera tra due funnel

#### Genetic algorithms GA

euristico, si ispira a principi di evoluzione biologica
costruisco una popolazione di individui ciascuno con un proprio patrimonio genetico (un array di numeri)
fitness: proprieta target che voglio che il mio sistema soddisfi (es energia piu bassa possibile)
passo alla seconda generazione della popolazione: accoppio individui e tengo i figli con fitness migliore
es 2 cluster con forme diverse
taglio le due stringhe e li metto insieme
oppure in modo piu confuso (physically blind)
gli individui sono soggetti anche a mutazioni casuali
scambio alcuni numeri delle stringhe
il ciclo continua e tengo sempre i fitness migliori
come capisco quando fermarmi?
es negli ultimi 1000 passi ho raggiunto la soglia o la fitness non è cambiata

##### apprendimento lamarkiano

se un individuo impara qualcosa, la trasmette alla progenie
prima di selezionare li sottopongo a un'ottimizzazione di minimo locale, minimi piu belli, algoritmo piu efficiente

#### Basin hopping

efficiente per i cluster
ricerca di minimo globale basata su campionamento casuale delle configurazioni
ci conviene lavorare sulla step function che corrisponde alla minimizzazione della configurazione del sistema
assegno le energie dei minimi locali anche alle x vicine
regole monte carlo metropolis: da S a D mi muovo con una probabilita <1
invece se mi guardo la linea rossa (minimo locale) probabilita 1 di muoversi
sulla superficie originale rischio di perdere delle transizioni nel bacino giusto ma a energie piu alte
mosse monte carlo:
- spostamento piccolo, grande
- cambiamento proprietà di superficie
- swap di atomi diversi (ottimizzazione dell'ordinamento chimico della struttura)
aspetti importanti
**introdurre un elemento di memoria**
evitare di tornare dove sono gia stato
devo identificare i funnel, si fa con parametro d'ordine che discriminano i funnel
per i cluster: common neighbor analysis
coppia di atomi (poi ripeto su tutti)
r = n di PV che A e B hanno in comune
p = n di legami presenti di PV
t = lunghezza della catena piu lunga

nell'esempio (5,5,5)
ottengo una distribuzione delle triplette buone a distinguere i funnel

es Au90Cu190 B,C,D hanno energie simili ma occupano regioni diverse delle percentuali d (5,5,5)
n di legami misti puo essre un parametro d'ordine

**condurre tante ottimizzazioni / ricerche in parallelo cercando di evitare ripetizioni**
sempre con parametro d'ordine
PEW algoritmo che consente ricerche in parallelo
grafico di n atomi con successo a parita di n di BH

