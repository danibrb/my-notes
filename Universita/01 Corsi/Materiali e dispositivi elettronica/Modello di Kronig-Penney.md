
![[kronig penney.png|500]]

[[da livelli a bande 2025.pdf#page=36&rect=110,367,619,494|da livelli a bande 2025, p.36]]

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

