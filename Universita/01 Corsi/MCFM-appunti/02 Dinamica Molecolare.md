
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

**scelta della discretizzazione temporale**
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

