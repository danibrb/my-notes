
come [[Elettrone in una scatola infinita]] ma non forzo $\psi$ ai bordi della scatola

parto da $-\dfrac{\hbar^2}{2m}\nabla^2\psi+V\psi=E\psi$
distinguo due casi attorno all'interfaccia x=0

![[scatola finita.png|300]]

[[da livelli a bande 2025.pdf#page=7&rect=553,428,714,539|da livelli a bande 2025, p.7]]

$$(1)\ -\dfrac{\hbar^2}{2m}\nabla^2\psi=E\psi \quad x<0 \Rightarrow \psi=Ae^{ikx}+Be^{-ikx} \Rightarrow k=\sqrt{\dfrac{2mE}{\hbar^2}}$$
$$(2)\ -\dfrac{\hbar^2}{2m}\nabla^2\psi+V\psi=E\psi \quad x>0 \Rightarrow \dfrac{\partial^2}{\partial x^2}\psi=\dfrac{2m(V_0-E)}{\hbar^2}\psi$$
per $E<V_0$ ho $\psi=Ce^{-Kx}+De^{Kx}$ ma il secondo termine non c'è
impongo la continuità della funzione e della derivata in $x=0$
$A+B=C \quad ikA-ikB = -KC$
sostituisco e divido per A, ottengo $ik(1-B/A)=-K(1+B/A)$
risolvo per B/A, trovo il coefficiente di trasmissione e riflessione
$$\dfrac{B}{A}=\dfrac{ik+K}{ik-K} \Rightarrow R= \left\lvert\dfrac{B}{A}\right\rvert^2=1 \quad T=1-R=0$$
ho riflessione totale all'interfaccia x=0
tuttavia la probabilità di trovare un elettrone oltre la barriera è $\vert \psi(x)\vert^2 \ne 0$
infatti per $x>0 \quad \psi_2=Ce^{-Kx} \Rightarrow \vert \psi_2\vert^2 = C^2e^{-2Kx}$
effetto tunnel