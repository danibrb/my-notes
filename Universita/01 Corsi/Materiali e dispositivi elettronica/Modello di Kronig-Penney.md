
![[kronig penney.png|500]]

[[01 da livelli a bande 2025.pdf#page=36&rect=110,367,619,494|da livelli a bande 2025, p.36]]

- periodo potenziale: a+b $$
V(x) =
\begin{cases}
0, & 0 < x < a \\
V_0, & -b < x < 0
\end{cases}
$$
$$
\begin{cases}
-\dfrac{\hbar^2}{2m} \dfrac{\partial^2 \psi}{\partial x^2} = E \psi, & 0 < x < a \\[1em]
-\dfrac{\hbar^2}{2m} \dfrac{\partial^2 \psi}{\partial x^2} + V \psi = E \psi, & -b < x < 0 \\[1em]
\end{cases} \qquad
\begin{cases}
\dfrac{\partial^2 \psi}{\partial x^2} + \dfrac{2mE}{\hbar^2} \psi = 0, & 0 < x < a \\[1em]
\dfrac{\partial^2 \psi}{\partial x^2} + \dfrac{2m}{\hbar^2}(E - V)\psi = 0, & -b < x < 0
\end{cases}
$$

introduco 
$$\alpha^2=\dfrac{2mE}{\hbar^2}, \qquad \beta^2=\dfrac{2m(V-E)}{\hbar^2}$$
$\beta>0$ se $V>E$ avendolo definito come un quadrato
sostituisco e ottengo
$$\begin{cases}
\dfrac{\partial^2 \psi}{\partial x^2} + \alpha^2 \psi = 0 \\[1em]
\dfrac{\partial^2 \psi}{\partial x^2} - \beta^2\psi = 0
\end{cases}$$
trovo soluzioni
$$\begin{cases}
\psi(x)=Ae^{i\alpha x} + Be^{-i\alpha x}, & 0 < x < a \\[1em]
\psi(x)=Ce^{\beta x} + De^{-\beta x}, & -b < x < 0
\end{cases}$$
impongo continuità della funzione e della derivata prima in x=0 e x=a

per x=0 ho
$$\begin{align}
A+B &=C+D \\ 
i\alpha(A-B) &=\beta(C-D)
\end{align}$$

per x=a ho
$$
\begin{align*}
A e^{i\alpha a} + B e^{-i\alpha a} &= C e^{\beta a} + D e^{-\beta a} \\
i\alpha A e^{i\alpha a} - i\alpha B e^{-i\alpha a} &= C\beta e^{\beta a} - D\beta e^{-\beta a}
\end{align*}
$$
inoltre deve soddisfare il [[Teorema di Bloch]]

$$\psi(x+(a+b))=e^{ik(a+b)}\psi(x)$$
metto insieme e ottengo un sistema di 4 equazioni e 4 incognite
$$
\begin{align*}
A e^{i\alpha a} + B e^{-i\alpha a} &= (C e^{-\beta b} + D e^{\beta b})e^{ik(a+b)} \\
i\alpha A e^{i\alpha a} - i\alpha B e^{-i\alpha a} &= (C\beta e^{-\beta b} - D\beta e^{\beta b})e^{ik(a+b)}
\end{align*}
$$
il sistema ha una soluzione 
$$
\frac{\beta^2 - \alpha^2}{2 \alpha \beta}
\sinh(\beta b)\sin(\alpha a) + \cosh(\beta b)\cos(\alpha a) = \cos(k a)
$$
introduco P, che ==misura l'area della barriera di potenziale==
$$P=\dfrac{\beta^2ba}{2}$$
Considero il caso $V_0 \rightarrow \infty$ e $b \rightarrow 0$ allora $\beta >> \alpha$ e $\beta b <<1$, ottengo
$$\dfrac{P}{\alpha a}\sin(\alpha a) +\cos(\alpha a)=\cos(ka)$$
risolvo per via grafica
![[soluzione kronig penney.png]]

[[01 da livelli a bande 2025.pdf#page=39&rect=154,155,597,342|da livelli a bande 2025, p.39]]

- Ci sono valori di $\alpha a$ che non hanno soluzioni per l'equazione del moto
- hp valori di energia che non producono moto
$$\alpha a = \dfrac{\sqrt{2mE}}{\hbar}a$$
