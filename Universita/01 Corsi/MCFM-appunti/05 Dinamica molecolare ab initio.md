
DM classica:
- ignora gradi di liberta elettroniche (interazione tra palle)
- contiene molti parametri (necessaria pre parametrizzazione)
- forme funzionali semplici
- posso simulare per scale temporali maggiori
altro approccio:
- calcolo potenziale ab initio da equazione di Schrodinger ad ogni step calcolo energia e forze cosi
- approccio piu accurato (non ho piu un modello a sfere con molle)
- nono devo parametrizzare il force field ogni volta
- permette rottura di legame (potenziale armonico no)
- ![[Pasted image 20260718144234.png]]
- per risolvere l'equazione di Schrodinger bisogna diagonalizzare matrici molto grandi, non possiamo studiare sistemi con un numero di atomi troppo grande (100 atomi vs 100'000 atomi in molecola)
- posso fare pochi ps di simulazione
cambiano le scale spaziali e temporali
da equazione di Schrodinger time dependent possiamo arrivare a DM ab initio
formula scritta in unita atomica (non c'è $m_e$)

**approssimazione born huang**
$$\Psi(\vec{r}, \vec{R}, t) = \underset{\substack{\uparrow \\ \text{stati elettronici} \\ \text{del sistema}}}{\sum_{J}^{\infty}} \Omega_J(\vec{R}, t) \Phi_J(\vec{r}, \vec{R})$$
![[Pasted image 20260718144857.png]]

sappiamo gia risolvere l'equazione per $$\Phi_J(\vec{r}, \vec{R})$$
con un po di algebra si ottiene
funzione d'onda nucleare ha equazione con:
- energia nucleare
- energia potenziale $E_I(\vec{R})$
- altri termini di interazione tra stati elettronici diversi I e J
- termine di accoppiamento tra stati elettronici diversi, ci dice come questo accoppiamento influenza il moto nucleare
di solito questi termini misti di accoppiamento sono piccoli, trascurabili
$$\Psi(\vec{r}, \vec{R}, t) \simeq \Omega_J(\vec{R}, t) \Phi_J(\vec{r}, \vec{R})$$
considero un solo stato
sto disaccoppiando il mio sistema
studiamo evoluzione dinamica del sistema in un singolo stato elettronico (valido solo se l'interazione tra stati diversi è trascurabile)
di solito se c'è interazione con la luce questo non si puo fare questa approssimazione (laser)

andiamo a risolver l'equazione di Newton per i singoli atomi
come ottengo $V_j$? risolvendo l'equazione di ??

vogliamo esprimere E come funzionale della densità di stati elettronica, ci sono pero tanti gradi di approssimazione (trade off tra accuratezza e costo computazionale)
velocity verlet
codice dinamica molecolare ab initio: come quello classico piu un'altra funzione per calcolare energia da equazione di Schrodinger
per risolvere il costo computazionale della MD ab initio
Car-Parrinello MD (utilizzata prima delle GPU)
approssimazione: 
- diamo una massa fittizia agli elettroni (li rallentiamo)
riducendo l'importanza dell'approssimazione adiabatica
- utilizzo equazione di N classiche onde per elettrone (cosi non devo usare Schrodinger)
- equazioni classiche per propagare il moto degli elettroni
- lagrangiana: una per il moto nucleare
						- elettronico
- $\Phi_i$ coefficiente da equazione lagrangiana (classica), non sono piu autofunzioni ottenute diagonalizzando matrici grandi
sto semplificando il problema (masse fittizie) ma accelero il tutto
bisogna comunque soddisfare dei limiti quantistici (es orbitali ortogonali)
anche gli elettroni hanno una T fittizia elettronica -> energia elettronica
non deve essere alta
frequenza nucleare piu alta:
- data legami di H
- si sostituiscono con ?? per aumentare frequenza -> aumentare energia cinetica

con le GPU si è perso questo vantaggio computazionale nel fare questa approssimazione
primi anni 2000: MD classica con calcolo dell'energia ab initio risolvendo equazioni di Schrodinger
$$FC = \varepsilon CS \qquad \psi = \sum_i c_i \phi_i$$
con F matrice di Fock

cosa si ottiene in piu da MD ab initio?
posso studiare sistemi in stato solido, liquido, simulazioni di spettroscopia e proprieta strutturali

come faccio a simulare processi su scale lunghe?
spazio delle fasi: per passare da uno stato all'altro -> barriera energetica
da questa dipende il tempo di transizione

#### Enhanced sampling

cerco di diminuire le barriere
se la barrera alta
![[Pasted image 20260718151528.png]]

se la barriera è bassa 
![[Pasted image 20260718151602.png]]
vedo transizioni

quindi devo modificare H per diminuire la barriera

#### well tempered metadynamics

è un modo per abbassare la barriera
consiste nell'aggiungere un potenziale di bias
s variabile collettiva, parametro d'ordine che descrive lo stato del sistema
riusciamo a osservare eventi rari
si possono fare analisi statistiche
fare distribuzioni calcolare funzioni di correlazione valori medi 
si possono ricavare diverse informazioni
- spettroscopia vibrazionale: ft di particolari proprieta legata a come gli atomi si muovono nel tempo (permette di considerare effetti anarmonici del potenziale)
- spettri infrarossi RAMAN
- posso simulare formazione distruzione di legami

Nuovo approccio ML
utilizzare metodi di ML per fare MD ab initio accurata ma piu veloce
come lo utilizziamo?
invece di risolvere equazioni di Schrodinger si cerca di imparare relazioni tra dati input (posizione atomiche) e dati output (forze energie) con NN
abbiamo sempre dinamica approssimata am con errori decisamente piu piccoli
con i modelli di ML possiamo studiare centinai di migliaia di particelle su scale anche di ns come MD classica (anche se un pochino piu lentamente)
serve un dataset accurato
struttura: coordinate atomiche
devo trasformarli in una rappresentazione adatta alle NN
trasformo struttura in descrittori
i descrittori vengono passati a un modello di apprendimento
mi restituisce proprietà di interesse (energie e forze)
1. data collection: come costruisco il data set 
2. descrittori: funzioni che descrivono ambiente attorno agli atomi
3. ML modello
4. mi restituisce la forma del potenziale

esempio molecola a 2 atomi
![[Pasted image 20260718155306.png]]
soluzione esatta
![[Pasted image 20260718155252.png]]
noi prendiamo N configurazioni in punti diversi, training set iniziale
train $$\{x, y, z\} \rightarrow E, F$$
il modello fara un fitting (interpolazione tra punti) per imparare a dare E e F data le $\{x, y, z\}$

il modello fa un fitting cercando di minimizzare l'errore tra il valore predetto e quello vero

#### modello di behler Parrinello

Etot somma delle energie dei singoli atomi
prende le coordinate atomiche (trasformate in descrittori)
studia environment
cerca di dare il contributo delle interazioni energie per il singolo atomo
cerca di minimizzare RMSE
E somma di contribuiti atomici individuali
es solido composto da 100 atomi
posso fare estrapolazioni e fare predizioni su sistemi molto grandi (migliaia centinaia di migliaia di atomi)
piccolo train set 100 atomi

simulazioni di batterie al litio
portatore di carica Li
deve esserci diffusione per applicazione di campo elettrico
ma come diffonde?
litio fluoruro: 2 particelle diverse cariche Li e F in un reticolo
potrei farlo anche con MD classica (non è un sistema complesso)
**radial distribution function** (RDF) ci dicono l'ordine del reticolo cristallino, come sono distribuiti gli atomi attorno a uno centrale
per un reticolo cristallino Li e F mi aspetto RDF piccole (non si possono muovere tanto)
se c'è RDF tra due picchi: atomi si possono muover (probabilita di trovare atomi al di fuori del sito reticolare)
utilizzando classical force field: osservo RDF in un solido meltato (eccessiva libertà di movimento)
solido descritto come liquido a temperatura ambiente
descrizione non va bene
anche cercando riparametrizzazione, si conserva stato solido solo per tempi brevi (10-20ps)
utilizzando modello ML: sistemi con 10000 atomi si ottiene un RDF su scala di ns che rappresenta un solido
processo di diffusione del Li su scala lunga
lo si riesce ad osservare si vede atomo di Li che ne calcia un altro su un sito libero