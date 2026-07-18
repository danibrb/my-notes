
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
ma invece che mettere la K target, la ricavo da $$p(K) = \frac{2}{\sqrt{\pi}} \frac{K^{1/2}}{(k_B T)^{3/2}} e^{-\frac{K}{k_B T}}$$