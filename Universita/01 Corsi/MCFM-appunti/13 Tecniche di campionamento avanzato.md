
algoritmi che forzano il campionamento in regioni della FES che non sarebbero accessibili perche barriere troppo alte
e poi dovemmo riuscire a riscostruire il profilo
vediamo due tecniche

## Umbrella sampling

introduco potenziale di bias
confina il sistema a campionare una regione della FES con un particolare valore della CV
voglio campionare finestre tra $\xi_A$ e $\xi_B$  (es stato associato e dissociato in NaCl)
faccio tnate simulazioni di MD a variabili indipendenti "finestre" in cui $\xi$ è fissata a un valore
$$U^{\text{biased}} = U^{\text{originale}}\big(\{\vec{R}\}\big) + \omega_i\big(C\{\vec{R}\}\big)$$
$\omega_i$ dipende dalla finestra che stiamo campionando
a noi interessa la probabilita unbiased, noi pero troviamo quella biased
$$e^{+\dfrac{w_i\big(C(\vec{R})\big)}{k_B T}}$$

è una costante: dipende dalla CV, la $C(\vec{R}) = \xi$ 
$$P_i^u(\xi) = P_i^b(\xi) e^{\dfrac{w_i(\xi)}{k_B T}} \frac{\int \dots}{\int \dots}$$
media secondo la distribuzione unbiased
$$F_i(\xi) = -k_B T \ln P_i^u(\xi) = -k_B T \ln P_i^b(\xi) - w_i(\xi) + C_i$$
con Ci offset che non conosciamo
![[Pasted image 20260719180027.png]]
serve una procedura che ci aiuti a raccordare i pezzo tra loro (serve continuita)
questa pero è la versione semplificata: noi in ogni finestra otteniamo un profilo completo, non solo nell'intervallo
quindi in ogni intervallo ho il contributo di tutte le finestre, ma i valori piu attendibili sono quelli che sono maggiormente campionati in quell'intervallo

#### WHAM
algoritmo che risolve cio
abbiamo un fattore d'indeterminazione che è una costante
$$P^u(\xi) = \sum_i p_i(\xi) P_i^u(\xi)$$
pi mi pesa la finestra con maggior contributo
come trovo i pesi
finestra iesima colleziono Ni campioni
peso = valore atteso del suo istogramma / somma sui valori attesi degli istogrammi delle altre finestre (possono esserci contributi nulli)

H altezza delle barre degli istogrammi
WHAM utilizza una procedura iterativa per risolvere il problema che non conosciamo <>u
all'inizio assegna valori casuali tipo 1 poi trova $P^u(\xi)$ e si ricava la <>u
ricalcola la $P^u(\xi)$ e cosi via
$$w_i(\xi) = \frac{1}{2} k \left( \xi - \xi_i^{\text{ref}} \right)^2$$
scelta semplice ma gettonata
bisogna scegliere bene i parametri
k deve essere abbastanza grande da campionare la finestra che mi interessa, ma non troppo grande da non avere overlapping, non campionare tutte le finestre adiacenti

esempio
proteina misfoldata (protofibrilla)
cv:
serve una configurazione di partenza che sia al centro della finestra (se no la simulazione esplode)
una per ciascuna finestra
steered MD (applico una forza artificiale)
devo calcolare la probabilita biased -> altezze istogrammi
questi devono sovrapporsi un po
grafico vero (istogrammi colorati) dove gli istogrammi sono brutti con poca sovrapposizione -> FE è ripida li ($\xi$ piccola istogramma verde e marrone)
dove c'è parabola perfetta -> andamento piatto della FE
effettivamente usando WHAM viene come ci aspettavamo
stato aggregato, molto stabile favorito
se volessimo sapere contributo entropico dovremmo calcolare a 2 T diverse

### Metadinamica

il bias dipenda dal tempo e ha memoria
metafora: tizio ubriaco casca in piscina, vorrebbe uscire ma non trova le scale, ma ha una sorgente infinita di sabbia
riempie il fondo della piscina di sabbia dove cammina
il livello si alza puo uscire
la sabbia ricostruisce anche il profilo della piscina
sabbia <-> potenziale di bias
è fatto da gaussiane che esercitano ina F che spinge il sistema lontano dalla posizione in cui si trova
una volta che è stato depositato, il potenziale resta li, history dependent
le gaussiane sono definite nello spazio della CV
sono depositate a intervalli regolari 
le gaussiane sono centrate nel valore della CV a cui si trovava quando è stato depositato il potenziale

grafico 
regime diffusivo: ho depositato gaussiane in tutte le buche e posso andare in tutti i minimi 
per ricostruire il bias serve ?? $$\lim_{t \to \infty} \omega_G(\xi, t) = -F(\xi) + c$$
le gaussiane non devono essere troppo grandi (altrimenti profilo rugoso, creo barriere)
ne troppo piccoli se no ci metto una vita (vario l'altezza)
il rate di deposito?
il sistema si muove nello spazio della CV molto piu lentamente che nello spazio delle coordinate delle sue vibrazioni tipiche
il tempo caratteristico con cui confrontarsi è il tempo di diffusione della CV
spesso io non so quanto sia profonda la buca di potenziale, stimo un po, approccio empirico
quanto ampia deve essere la larghezza della gaussiana?
dipende dal range di campionamento della CV in MD classica
(piu è piccolo e piu puo essere piccola $\sigma$)

esempio

sistema a singola buca
dopo 2000 passi raggiungo il regime diffusivo
poi uso potenziale per ricostruire il profilo
dovrebbe esserci un minimo in zero
i dati pero sono ancora molto rumorosi
devo giocare con tempo, altezza h e larghezza $\sigma$ delle gaussiane
probabilmente la buca non era pazzesca, quindi faccio fatica a vederla cosi
posso ridurre il rate di deposito e la h

### Metadinamica Well tempered

h=h(t)
cosi quando sono nella buca è maggior e in cima meno
ottimizzo un po
voglio profilo piatto solo in cima
si puo dimostrare che mentre la metadinamica classica a parte la rugosita, converge all'infinito a $-F(\xi$) con questa si converge alla F per un fattore che pero è noto (bias factor)

esempio
ci sono due minimi
è uno spazio 2D a 2CV
vediamo di fare metadinamica
gromacs e plumed
c'è uno shift verticale delle curve dovuto al fatto che continuo ad aggiungere bias
bisogna capire se si sta convergendo al profilo della FE
effettivamente si perche cambia la profondita delle buche
1,4 kj/mol circa mezzo kbT 
usando well tempered
ogni volta che si deposita in un punto nuovo le gaussiane hanno l'altezza di partenza
figura di convergenza dei profili di FE nei due casi
la metadinamica well tempered ha oscillazioni piu regolari -> risultato con errore piu piccolo
con MetaD W-T puo capitare di rimanere dentro una buca per sempre (se h diminuisce troppo in fretta, se $\gamma$ troppo piccolo)

esempio
studio il dipeptide dell'alanina, ma usando una sola delle CV, non riesco a discriminare bene i due minimi
la convergenza diventa problematica perche non sto monitorando l'altro grado direzionale ortogonale
