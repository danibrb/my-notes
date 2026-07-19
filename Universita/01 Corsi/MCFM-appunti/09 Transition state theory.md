
cerca di spiegare la cinetica: come si passa da un minimo all'altro
![[Pasted image 20260719101243.png]]
diamo una stima del rate per cui la particella riesce a scappare

2 ipotesi:
- barriera piu alta dell'energia termica
- se particella supera la barriera non torna piu indietro

densita di probabilita che la particella sia in corrispondenza della barriera con impulso p 
$$\phi(\vec{x}_b, \vec{p})$$
???
due funzioni di partizione associata al bacino che il minimo in x0

$$Z = \dots = \left( \sqrt{2\pi m k_B T} \right)^{3N} Z_{\text{conf}}$$
$$\frac{1}{\int_{x_0, \text{basin}} dx \, e^{-\beta U(x)}}$$
$$\text{approx. arm.} \qquad \text{flusso} = \nu e^{-\beta E_a}$$

$\nu$ frequenza di oscillazione in fondo alla buca (frequenza del minimo di partenza)
Ea altezza della barriera che separa i minimi
il flusso è tanto > quanto e > $\nu$ e quanto è < Ea

formalismo di Arrhenius
$$\text{flusso} = k = \frac{\omega}{2\pi} e^{-\beta E_a}$$
$\frac{\omega}{2\pi}$ prefattore
$e^{-\beta E_a}$  termine di arrhenius

#### sistema di N particelle all'equilibio nell'insieme canonico

siamo nel bacino m
due minimi separati da un punto di sella di primo ordine
con quale frequenza si supera la buca?
k= 3N - 6
sono in un minimo, tutti gli autovalori sono positivi
energia dello stato di transizione Ut = Ea + approssimazione armonica
$$\omega_1^2 < 0$$
e gli altri positivi (punto sella)
definisco una superficie identificata dalla coordinata O di transizione $\zeta_1$ arbitraria
devo considerare solo le traiettorie (\*) che hanno derivata positiva
nella direzione della transizione
$$\theta(\dot{\xi}_{t, 1}) = \begin{cases} 1 & \text{se } \text{deriv.} > 0 \\ 0 & \text{se } \text{deriv.} < 0 \end{cases}$$
$$\zeta_i = \sqrt{m_i} q_i \qquad \pi_i = \frac{p_i}{\sqrt{m_i}} \qquad i = 1, \dots, k$$
$$H = E_m + \sum_{i=1}^{k} \frac{1}{2} \left( \pi_i^2 + \omega_{m,i}^2 \xi_i^2 \right)$$
Em energia del minimo di partenza (si puo mettere a zero)
$\omega_{m,i}^2$ tutti positivi
allo stato di transizione 
$$\omega_{c,1}^2 < 0, \qquad \omega_{c,i}^2 > 0 \qquad i = 2, \dots, k$$
calcoliamo la funzione di partizione nel minimo
$$Z_m = \int e^{-\beta H} d^k\xi d^k\pi \simeq e^{-\beta E_m} \prod_{i=1}^{k} \left[ \int_{-\infty}^{+\infty} d\pi_i \, e^{-\beta \frac{1}{2} \pi_i^2} \int_{-\infty}^{+\infty} e^{-\beta \frac{1}{2} \omega_{m,i}^2 \xi_i^2} d\xi_i \right] =$$
ricordando che
$$\left( \int_{0}^{\infty} e^{-ax^2} dx = \frac{1}{2} \sqrt{\frac{\pi}{a}} \right)$$
$$= e^{-\beta E_m} \prod_{i=1}^{k} \left[ \left(\frac{2\pi}{\beta}\right)^{1/2} \left(\frac{2\pi}{\beta}\right)^{1/2} \frac{1}{\omega_{m,i}} \right] = e^{-\beta E_m} \left(\frac{2\pi}{\beta}\right)^k \prod_{i=1}^{k} \frac{1}{\omega_{m,i}}$$
al numeratore invece ci restringiamo alla coordinata con $\zeta =0 \ (\zeta_1)$
e alle traiettorie che hanno derivata positiva (\*)
$$\begin{aligned}
&\int \delta(\xi_1) \theta(\pi_1) \pi_1 e^{-\beta H} d^k\xi d^k\pi \simeq \\
&\simeq e^{-\beta E_a} \int_{0}^{\infty} \pi_1 e^{-\beta \frac{1}{2} \pi_1^2} d\pi_1 \cdot \left(\frac{2\pi}{\beta}\right)^{k-1} \prod_{i=2}^{k} \frac{1}{\omega_{c,i}} =
\end{aligned}$$
$$= e^{-\beta E_a} \frac{1}{\beta} \left(\frac{2\pi}{\beta}\right)^{k-1} \prod_{i=2}^{k} \frac{1}{\omega_{c,i}} \qquad \left( \int_{0}^{\infty} x e^{-ax^2} dx = \frac{1}{2a} \right)$$
facendo il rapporto tra numeratore e denominatore otteniamo il rate
$$k = \frac{1}{2\pi} \frac{\prod_{i=1}^{k} \omega_{m,i}}{\prod_{i=2}^{k} \omega_{c,i}} e^{-\beta E_a} \qquad \leftarrow i=2$$
i = 2 perche 1 è vincolato sostanzialmente

il prefattore ora dipende anche dalle caratteristiche vibrazionali dello stato di transizione, dipende dalla probabilita che quello stato sia occupato
tanto piu è morbida la forma della PES alla direzione di transizione e tanto piu è favorevole
un sistema rea che si muove per agitazione termica, potrebbe cascare nel bacino dell'altro minimo per un'altra strada meno probabile che non è il cammino di energia minima
colleghiamo cio all'energia libera
$$\begin{aligned}
\Delta F &= -k_B T (\ln Z_t - \ln Z_m) \\
&\Rightarrow k = \frac{k_B T}{h} e^{-\frac{\Delta F}{k_B T}}
\end{aligned}$$
la possibilita di attraversare la barriera dipende non solo dall'energia potenziale disponibile ma anche dalla probabilita di accedere ai bacini minimi non per il cammino di energia minima
bisogna anche considerare il rapporto tra le entropie
dipendenza da energia libera $\Delta F$ non solo potenzial