
algoritmi che modificano l'esito di integrazione di uno step della DM per introdurre interazioni con il bagno termico
idea: riscalaggio semplice delle velocita di tutte le particelle 
$$v_i = v_i^* \sqrt{\frac{K}{K^*}}$$
problema: 
- puo modificare tanto le traiettorie
- non ottengo distribuzione corretta per le velocita e energia cinetica che dovrei avere nella distribuzione canonica
allora:

#### termostato di Berendensten

se il sistema tende alla T target con una velocita che dipende da un parametro $\tau$
$$\frac{dT}{dt} = \frac{1}{\tau} \left( T - T^*(t) \right)$$
con T = target e T* = attuale
riscala sempre le velocita ma non improvvisamente, da un istante all'altro gradualmente
$$T^*(t + \Delta t) = T^*(t) + \frac{\Delta t}{\tau} \left( T - T^*(t) \right)$$
è un po piu vicina a T
identifichiamo fattore di scala $v_i = \lambda v_i^*$
$$\lambda^2 = \frac{T^*(t + \Delta t)}{T^*(t)}$$
sostituendo $$\lambda = \sqrt{1 + \frac{\Delta t}{\tau} \left( \frac{T}{T^*(t)} - 1 \right)}$$
funziona bene, regolando bene $\tau$ ci porta a T velocemente
$\tau$ deve essere sensibilmente piu grande del timestep
ma non riusciamo a riprodurre bene le distribuzioni canoniche

#### termostato di Bussi Parrinello

riscalo $$v_i = v_i^* \sqrt{\frac{K}{K^*}}$$
ma invece che mettere la K target, la ricavo da $$P(K) = \frac{2}{\sqrt{\pi}} \frac{K^{1/2}}{(k_B T)^{3/2}} e^{-\frac{K}{k_B T}}$$

#### termostato di Andersen

considero che ciascuna particella abbia una certa probabilita di collidere con il bagno termico $$p_c(t) = \eta_c \delta t$$
se avviene allora la v delle particelle la estraggo dalla distribuzione alla T desisderata
c'è ancora un problema di convergenza
bisogna tarare bene $\eta_c$
$$\langle v(t) v(0) \rangle \propto \exp\left( -\frac{t}{\tau_v} \right)$$
faccio il plot di questa funzione di correlazione $\langle v(t) v(0) \rangle$ e trovo $\tau_v$ tempo di correlazione
dovrebbe essere $$\tau_v < \eta_c^{-1}$$

$$10 \frac{\text{m}}{\text{s}} = 10 \cdot 10^{10} \frac{\text{Å}}{\text{s}} = 10^{11} \frac{\text{Å}}{\text{s}} = 10^{11} \frac{\text{Å}}{\cancel{\text{s}}} \cdot \frac{\cancel{\text{s}}}{10^{12} \text{ps}} = 0,1 \frac{\text{Å}}{\text{ps}}$$
timestep 0,001 ps

per implementare:
a ogni passo e per ogni particella estraggo un numero 
se $r < \eta_c \delta t$ estraggo 
se $r > \eta_c \delta t$ integro con verlet
$$[\text{eV}] = \frac{1}{2} m v^2 \quad \rightarrow \quad [v^2] = \frac{\text{eV}}{\text{kg}} = \frac{1,6 \cdot 10^{-19} \text{J}}{\text{kg}}$$
$$1 \frac{\text{m}^2}{\text{s}^2} = \frac{10^{20} \text{Å}^2}{\text{s}^2} \qquad \qquad 1,6 \cdot 10^{-19} \frac{\text{m}^2}{\text{s}^2}$$


#### termostato di Langevin

particelle del sistema si muovono in un background caratterizzato da una resistenza viscosa

$$m \frac{dv}{dt} = \underset{\substack{\uparrow \\ \text{termine dissipativo} \\ \text{(attrito viscoso)}}}{-m v \eta_f} + F(x) + \underset{\substack{\uparrow \\ \text{rumore bianco che} \\ \text{compensa la dissipazione} \\ \text{(per cons. e{ }an.)}}}{\Gamma(t)}$$
si va a toccare l'integratore le equazioni del moto vanno riformulate
$\Gamma(t)$ segnale distribuito gaussianamente centrato in zero
la larghezza è data da $C = \Gamma(0) \Gamma(0)$
$$\langle \Gamma(t) \cdot \Gamma(t') \rangle = C \delta(t - t')$$
$$C = 2 \eta_f k_B T m$$
modifica di piu di Andersen la traiettoria del moto

**Barostati** seguono la stessa filosofia

## Implementazione codice MD

- cluster di 38 atomi di AR
- siamo in un minimo di U
- U è la somma di interazioni a coppie di LJ
- unita di misura sul file $\text{Å}$
a T=0 quel minimo ha probabilita 1 di essere occupato
a T>0 diminuisce

si puo calcolare $E_{tot} = U_0 + K$ con K da stimare
Microcanonico: E = costante
potrei scegliere K tc T= 20K
- simulazione microcanonico: verifico conservazione dell'energia
- T costante
- vediamo transizioni di fase
- analisi probabilita di cascare dentro al minimo locale piu basso



