
cerchiamo problema di occupazione dei minimi in funzione di una grandezza termodinamica
$$P(\vec{r}, \vec{p}) = \frac{e^{-\beta H(\vec{r}, \vec{p})}}{Z} \qquad Z = \frac{1}{h^{3N} N!} \int_{V} d^{3N}r \int_{-\infty}^{+\infty} d^{3N}p \, e^{-\beta H(\vec{r}, \vec{p})}$$
con N numero di atomi
considero una serie di minimi locali per cui definiamo una Z locale
$$Z_s = \frac{1}{h^{3N} N!} \int_{V_s} d^{3N}r \int_{-\infty}^{+\infty} d^{3N}p \, e^{-\beta H(\vec{r}, \vec{p})}$$
mi aspetto che $$Z = \sum_{s} Z_s$$
moti: traslazioni, rotazioni attorno al CM, vibrazioni
posso fattorizzare
$$\text{dividiamo:} \quad Z_s = Z^{\text{trans}} \cdot Z_s^{\text{rot}} \cdot Z_s^{\text{vib}} e^{-\beta E_s^0}$$
$E_0$ energia al fondo $e^{-\beta E_s^0}$ 

termine traslazionale (1)
non dipende da S
$$Z^{\text{trans}} = \left( \frac{2\pi M k_B T}{h^2} \right)^{\frac{3N}{2}} V$$
termine rotazionale (2)
approssimazione: oggetto corpo rigido
3 tre assi principali d'inerzia
integrale su angolo solido: liberta di orientazione nello spazio degli assi (angoli di eulero)  -> $8\pi^2$
integrale su tutti i possibili valori del momento angolare
poi divido per l'ordine del gruppo di simmetria
NB per cluster piccoli, moti rotazionali e vibrazionali sono disaccoppiati solo a T basse
(uguale per le molecole organiche fluffy, con tanti gradi di liberta configurazionali)
approssimazione classica solo se energia termica del sistema è >> della distanza classica tra i livelli

termine vibrazionale (3)
piccole oscillazioni -> espansione
$\zeta$ zeta dimensione $[lunghezza][radice \ di \ m]$
bisogna tenere conto di tutti i modi vibrazionali
3N-6 6 modi con autovalori nulli
problema di occupazione del bacino s $$P_s = \frac{Z_s}{Z}$$
probabilità tra due minimi 
$$\frac{P_{s'}}{P_s} = \frac{Z_{s'}}{Z_s} = \frac{\sigma_s}{\sigma_{s'}} \frac{Z_{s'}^{\text{rot}}}{Z_s^{\text{rot}}} \frac{Z_{s'}^{\text{vib}}}{Z_s^{\text{vib}}} e^{-\beta (E_{s'}^0 - E_s^0)}$$
termine rotazionale dipende dalla differenza tra i corpi rigidi dei due minimi

esempio
potenziale 1D con due minimi attorno a x0 e x1
probabilità di vedere popolata configurazione x0 o x1 a una certa T?
non ho termine rotazionale solo vibrazioni
a T bassa domina x0 domina $$e^{-\beta(U_1 - U_0)}$$
all'aumentare di T x1 domina $$\frac{w_0}{w_1}$$
è il modo di manifestarsi di una transizione che deriva dall'entropia (all'aumnetare di T anche se x1 non è minimo globale, è comunque favorito entropicamente)

esempio cluster bimetallico
minimo globale struttura decaedrica
la sua caratteristica vibrazionale non cambia molto
6-fold struttura piu favorevole vibrazionalmente
esiste una T alla quale il fattore entropico inverte le probabilita
T di transizione per 
$$\frac{P_{s'}}{P_s} = 1$$
transizione solido - solido (su strutture diverse)
questo è un esempio, volendo uno stato puo essere minimo globale e anche favorito entropicamente

energia potenziale vs energia libera:
per cluster semplici fatti nel vuoto basta energia potenziale, mentre per fasi liquide ci sono transizioni, l'entropia cambia
devi compensare con potenziale fittizio ??