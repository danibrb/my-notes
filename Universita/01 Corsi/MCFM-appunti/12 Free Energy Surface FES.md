
noi siamo in approssimazione semi classica
quando scartiamo gradi elettronici -> scartiamo entropia S ->
costruiamo una energia potenziale che ne tiene conto efficacemente
in TST gia a 2D troviamo effetti entropici (vibrazioni)
FES **necessaria per sistemi liquidi, soft matter, dove i gradi entropici sono fondamentali**

torniamo alla probabilita di occupazione di una posizione specifica
voglio ottenere posizione fissa $P(\vec{x})$ integro sui momenti

definizione 
Zid funzione di partizione del potenziale ideale (no U(x))
separo la parte cinetica (che dipende solo da **p**) da parte potenziale U che dipende da **x**

fattore di normalizzazione $V^N$
mi rimane **integrale configurazionale Q**
$$\begin{aligned}
Z_{\text{conf}} &= \frac{Q}{V^N} \\[1.5ex]
Z &= Z_{\text{id}} Z_{\text{conf}}
\end{aligned}$$
per $P(\vec{x})$ non integro sulle posizioni perche voglio una posizione specifica
$$P(\vec{x}) = \frac{e^{-\beta U(\vec{x})}}{Q}$$probabilita del singolo stato
per sfruttare concetto di energia libera mi devo riferire a un insieme statistico di configurazioni (non 1) a cui posso associare un'energia libera
problema di occupazione di un bacino / funnel (insieme di stati che raggruppiamo sulla base di qualche criterio)
probabilita di occupazione di un bacino
$$P_\Omega = \frac{Q_\Omega}{Q} = \frac{Z_\Omega}{Z_{\text{conf}}}$$
cerchiamo di scriverlo in funzione dell'energia libera
probabilita di occupazione relativa tra i due minimi
$$\frac{P_{\Omega_1}}{P_{\Omega_2}} = e^{-\beta \Delta F}$$
mi dice dove mi aspetto di trovare il sistema all'equilibrio

come definisco il bacino?
ci servono dei descrittori

## variabile collettiva CV

la chiamo $\xi$ 
funzione delle coordinate del sistema
la definizione di una CV corrisponde a un diminuzione della dimensione dello spazio
$I_\xi$ intervallo di valori assunti da $\xi$
NaCl
$I_{\xi_1}$ bacino stato slegato
$I_{\xi_2}$ bacino stato legato
![[Pasted image 20260719155836.png]]

$$\Delta F(I_{\xi_1}, I_{\xi_2}) > 0$$
come mai c'è una barriera tra i due stati?
da legato a slegato: forza di coulomb
da slegato a legato: forza di coulomb / van der waals con gli altri ioni

barriera di disidratazione
l'informazione del profilo della FES tiene quindi conto anche di altri gradi di liberta (quelli del solvente)

tra NVT o NPT non cambia molto: PV piccolo
rapporto tra PV e energia termica a disposizione molto piccolo
(vale per i liquidi non per i gas)

l'energia puo essere una CV? si
considero energia interna (termine energia cinetica piu potenziale) ed esprimo una probabilita p(E)
$\omega(E)$ densita di probabilita dell'energia
$\omega(E)dE = \Omega(E)$ probabilita di trovare stato con quell'energia, piu molteplicita (degenerazione)

$e^{-\beta E}$ sfavorisce l'occupazione di stati ad alta energia, mentre la molteplicita no
complessivamente: cio ci dice che a T diverso da 0 lo stato occupato non è quello a energia minima, ma a un'energia intermedia
fattore entropico fondamentale
$$\Delta F = \Delta E - k_B T \ln\left(\frac{\Omega(E_2)}{\Omega(E_1)}\right) = \Delta E - T \Delta S$$

$T \Delta S$ fattore entropico legato a conta degli stati

esempio 1
folding a T alta di una proteina globulare
esiste una configurazione funzionale per cui la proteina puo svolgere funzioni biologiche
differenza di energia tra stati 20-60 kJ/mol 
10/20 volte piu grande dell'energia termica, non esagerata
equilibrio delicato
se $\Delta G=0$ 50% folded 50% disordine
al variare della T $\Delta G>0$ o $\Delta G<0$

denaturazione a freddo

unfolding, perdita struttura nativa anche a T bassa
succede perche $\Delta G$ di unfolding $$\Delta G_u = G_u - G_f$$
se <0 unfolding piu probabile
$$\begin{aligned}
\Delta G(T_c) &= \Delta H(T_c) - T_c \Delta S(T_c) = 0 \\
&\Rightarrow \Delta S(T_c) = \frac{\Delta H(T_c)}{T_c}
\end{aligned}$$
Tc temperatura di transizione
espandiamo $\Delta G_u$
$$\begin{aligned}
\Delta H(T) &= \Delta H(T_c) + \int_{T_c}^{T} \Delta C_p(T) \, dT \qquad \Delta C_p(T) = \left( \frac{\partial \Delta H(T)}{\partial T} \right)_p \\[1ex]
&\text{(se } \Delta C_p(T) \text{ cost.)} \\[1.5ex]
&= \Delta H(T_c) + \Delta C_p(T)(T - T_c)
\end{aligned}$$

$$\Delta S(T) = \Delta S(T_c) + \int_{T_c}^{T} \underbrace{\left( \frac{\partial \Delta S(T)}{\partial T} \right)_p}_{\displaystyle \int_{T_c}^{T} \frac{\partial\Delta C_p(T)}{\partial T} \frac{1}{T} dT} dT \qquad \text{Nota: } \Delta S(T) \cdot T = \Delta C_p(T)$$
$$\begin{aligned}
\Delta S(T) &= \frac{\Delta H(T_c)}{T_c} + \int_{T_c}^{T} \Delta C_p \, d(\ln T) = \frac{\Delta H(T_c)}{T_c} + \Delta C_p \ln\left(\frac{T}{T_c}\right) \\[1.5ex]
\Rightarrow \Delta G(T) &= \frac{T_c - T}{T_c} \Delta H(T_c) + (T - T_c) \Delta C_p - T \Delta C_p \ln\left(\frac{T}{T_c}\right)
\end{aligned}$$
tutte quantita misurabili sperimentalemente abbas