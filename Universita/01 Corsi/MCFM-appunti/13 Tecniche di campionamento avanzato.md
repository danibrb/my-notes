
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

##