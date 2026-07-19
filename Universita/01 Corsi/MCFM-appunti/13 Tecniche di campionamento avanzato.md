
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
