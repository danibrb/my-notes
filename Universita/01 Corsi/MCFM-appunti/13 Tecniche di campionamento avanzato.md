
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

è una costante: dipende dalla CV, la 