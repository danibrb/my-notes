
"computer simulations of liquids" di allen tilderley
"molecole" -> liquidi materia soffice e biologica sono gli ambiti in cui è utilizzata

paper di alder 1957

Evoluzione
sfere dure

$$V_{HS}(r) = \begin{cases} \infty & r < \sigma \\ 0 & r \ge \sigma \end{cases}$$
Lennard Jones
$$V_{LJ}(r) = 4\varepsilon \left[ \left(\frac{\sigma}{r}\right)^{12} - \left(\frac{\sigma}{r}\right)^6 \right]$$
simulazioni sull'acqua
-> force field: 
- considero mutue interazioni tra particelle diverse -> interazione a coppie
- insieme delle forme funzionali delle interazioni e dei parametri che le caratterizzano

Dinamica molecolare classica

due ipotesi di lavoro
- non ci interessa la descrizione esplicita dei gradi di libertà elettronica (non vale per fenomeni conduzione, interazione luce materia, processi chimici)
- lavoriamo a una temperatura (dei nuclei) per cui possiamo trascurare le differenze em discrete negli atomi dovute a vibrazioni
$$k_B T \gg \hbar \omega \rightarrow T \gg \frac{\hbar \omega}{k_B}$$
frequenza di Debye max frequenza fononica possibile

### equazioni del moto di Newton

sistema di N atomi con stessa massa m che interagiscono tra lor con un potenziale di interazione 
$$U(\vec{x}_1, \vec{x}_2, \dots, \vec{x}_N)$$
3N equazioni del secondo ordine 
$$m \vec{a}_i = \vec{F}_i \qquad \vec{F}_i = -\frac{\partial U}{\partial \vec{x}_i}$$
quello che si ha piu spesso:
$$U = \sum_{j > i} u(x_{ij})$$
potenziale a coppie es LJ

oppure 6N equazioni del primo ordine
$$m \frac{d\vec{v}_i}{dt} = \vec{F}_i \qquad \frac{d\vec{x}_i}{dt} = \vec{v}_i$$
sistema isolato equazioni conservano la quantita di moto, momento angolare e energia totale
si risolvono con integrazione numerica -> discretizziamo il tempo (interpretiamo le equazioni in modo iterabile)

Simulazioni le posso fare in enseble diversi:
- Microcanonico
- Canonico -> conserva temperatura -> deve tenere conto di interazioni con il termostato del sistema
- NPT costante (termostato e barostato)
- aperto (es crescita)

1. inizializzazione di posizioni e velocita iniziali delle particelle
2. calcolo delle forze -> serve U -> trovo le posizioni
3. algoritmo di integrazione delle 6N equazioni
4. analisi e salvataggio output
algoritmo cicla aggiornando posizioni e velocita

1 e 2 sono comuni a tutti gli ensemble
3 e 4 sono specifici

#### scelta della discretizzazione temporale
es pot di LJ  O-----O
$$\text{Ar}: \omega = 3.6 \cdot 10^{12} \text{ s}^{-1} \rightarrow \tau = 1.7 \cdot 10^{-12} \text{ s}$$
serve un tempo di discretizzazione ad esempio 10 volte piu piccolo
pero per CC o CH ho tempi molto piu piccoli

potrei fregarmene delle vibrazioni e considerarle ???
es ferritina (proteina che immagazzina Fe e ne gestisce la quantita)
$m = 4.7 \cdot 10^5 amu$ 
cristallizza -> solida all'interno
studiamo questo cambio di fase
frequenza tipica di oscillazione $\tau \simeq 4.6 \cdot 10^{-9} \text{ s}$ time step dell'ordine di 0.1ns

**time step piu piccolo del piu veloce periodo di oscillazione**

pero piu è piccolo piu la performance computazionale diminuisce
(es 15 giorni per simulare 1ms)
c'è anche il limite di errori di precisione numerica
troppi errori di arrotondamento

#### inizializzazione del sistema

- posizioni iniziali lette da file $\{x_i(t=0)\}_{i=1,N}$
- velocita da file se disponibili
se non lo sono? generiamo noi le velocita
$$\begin{aligned}
g(v) &= f(v_x) f(v_y) f(v_z) \\[1.5ex]
f(v_x) &= \left( \frac{m}{2\pi k_B T} \right)^{1/2} e^{-\frac{m v_x^2}{2k_B T}}
\end{aligned}$$

g è una maxwelliana

estraiamo velocita da una gaussiana usando l'algoritmo di box-muller
(dispense dinamica molecolare di Ferrando), usando librerie
N (numero di particelle del sistema da simulare) è finito (38)
-> il centro di massa ha velocita non nulla (la avrebbe per N -> $\infty$)
problema numerico: dopo un po non ho piu digits per scrivere i numeri delle velocita (poco pratico)
-> rimuoviamo il CM ogni volta 
$$\{\vec{v}_i^* = \vec{v}_i^{BM} - \vec{v}^{CM}\}_{i=1,N}$$
poi calcolo energia cinetica del sistema ( o T) 
$$K^* = \frac{1}{2} m \sum_i v_i^{*2}$$
se quella ottenuta non è quella desiderata, riscalo 
$$v_i = v_i^* \sqrt{\frac{K}{K^*}}$$
non è detto che è l'energia cinetica conservata, non K ma E
simulazione microcanonica  a E e T specifici per ottenere cio K deve essere uguale a E-U energia potenziale

Ora calcoliamo le forze all'istante t
introduciamo un cut-off distanza oltre la quale non considero l'nterazione tra le molecole
interazione a coppie (no multicorpi) -> non è un'approssimazione da poco,
funziona bene su sistemi in fase liquida, meno sui solidi (specialmente i metalli)
nanoparticelle: decine di atomi di argon
se fossero atomi di metallo perderei un fenomeno:
si contraggono i legami di superficie e si espandono quelli interni (dovuto a interazione a multicorpi, dipende da primi vicini)
è la parte piu dispendiosa computazionalmente
2 indici per atomo -> 2 loop
per semplificare:
- sfrutto principio azione reazione
- cut off (per 38 atomi non serve)

aggiorniamo ora posizione e velocita delle particelle
evoluzione a t+dt

Considerazioni:
accuratezza della dinamica molecolare
non sara mai precisissima (errori approssimazione numerica)
$$|\Delta x^2| = \frac{1}{N} \sum_{i=1}^N |x_i(t) - x_i^{ref}(t)|^2$$
espresso in unita $\sigma$ di Lennard Jones
le previsioni della dinamica molecolare vanno sempre interpretare in senso statistico

propagatore della traiettoria:
- accuratezza
- buona conservazione dell'energia
- efficiente (una chiamata al calcolo della forza per loop)
- uso non eccessivo di memoria

vediamo un po di algoritmi di integrazione delle equazioni del moto

#### Eulero

sviluppo di Taylor al secondo ordine
$$\begin{aligned}
\vec{x}_i(t+dt) &= \vec{x}_i(t) + \vec{v}_i(t) \delta t + \frac{1}{2} \vec{a}_i(t) \delta t^2 + O(\delta t^3) \\[1.5ex]
\vec{v}_i(t+dt) &= \vec{v}_i(t) + \vec{a}_i(t) \delta t + O(\delta^2)
\end{aligned}$$
problema di questo algoritmo
non è invariante per inversione temporale (\*)
se voglio calcolare $\vec{x}_i(t + dt - dt)$ non ottengo $\vec{x}_i(t)$
$$\begin{aligned}
\vec{x}_i(t+dt-dt) &= \vec{x}_i(t+dt) - \vec{v}_i(t+dt)dt + \frac{1}{2}\vec{a}_i(t+dt)dt^2 \\[1.5ex]
&= \vec{x}_i(t) + \vec{v}_i(t)dt + \frac{1}{2}\vec{a}_i(t)dt^2 - \vec{v}_i(t)dt - {} \\[1.5ex]
&\quad - \vec{a}_i(t)dt^2 + \frac{1}{2}\vec{a}_i(t+dt)dt^2 \neq \vec{x}_i(t)
\end{aligned}$$
è associato un drift di energia a questi algoritmi (\*)

#### Verlet

sviluppo al terzo ordine di $\vec{x}_i(t + dt)$ e $\vec{x}_i(t - dt)$
$$\begin{aligned}
\vec{x}_i(t+dt) &= \vec{x}_i(t) + \vec{v}_i(t)dt + \frac{1}{2}\vec{a}_i(t)dt^2 + \frac{1}{6}\vec{b}_i(t)dt^3 + O(dt^4) \\[1.5ex]
\vec{x}_i(t-dt) &= \vec{x}_i(t) - \vec{v}_i(t)dt + \frac{1}{2}\vec{a}_i(t)dt^2 - \frac{1}{6}\vec{b}_i(t)dt^3 + O(dt^4)
\end{aligned}$$
sommandoli ottengo l'equazione del propagatore
$$\vec{x}_i(t+dt) = 2\vec{x}_i(t) - \vec{x}_i(t-dt) + \vec{a}_i(t)dt^2 + O(dt^4)$$
