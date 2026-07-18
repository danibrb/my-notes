
consideriamo cose che valgono per sistemi molto diversi
1. atomi metallici (quelli che abbiamo visto noi)
2. vetro colloidali: particelle colloidali che si autoassemblano e hanno transizioni di fase vetrose
3. folding di proteina
4. clatrato: struttura a gabbia di acqua congelata che ingloba metano
noi pero continuiamo a fare l'esempio della particella metallica

PES Potential Energy Surface
superficie di energia: dipende dalle 3N coordinate delle N particelle
minimi (condizioni metastabili): zeri della derivata di U e hessiano con autovalori positivi

punti sella (saddles): utili per la cinetica e dinamica
attraversati per passare da un minimo a un altro, l'hessiano ha un autovalore negativo
rappresentano i punti di massima energia nei percorsi di minima energia (teorema del passo di montagna)
quanti minimi ci sono?
data una configurazione quante e quali si possono considerare configurazioni identiche?
cluster con $N_A$ e $N_B$ 
posso fare operazioni di simmetria continue (traslazioni e rotazioni) o discrete (permutazioni degli atomi della stessa specie, inversione rispetto a un sistema di riferimento con centro nel CM della struttura, solo se la struttura non è chirale, altrimenti trovo un enantiometro)
stessa composizione chimica, per inversione/permutazione: $2N_A!!$
se la struttura ha delle simmetrie geometriche queste sarebbero gia contate nell'inversione, per non contarle due volte divido per h (es numero di riflessione)

esempio

LJ7 cluster
in ordine dal meno legato al piu
5h -> 5 rotazioni
D -> piano di riflessione
ho 504 minimi locali equivalenti
$N_{min}>10^{12}$ per N=55
esistono regole precise per la crescita del numero di punti stazionari corrispondenti a strutture diverse

## grafici di disconnettività

mi da informazioni su esistenza di minimo a un certo valore di U e anche su come è connesso agli altri minimi dato un percorso di minimi energetici
un superbacino è l'insieme di tutti i minimi che stanno sotto un certo taglio di energia
quello che abbiamo fatto noi:
eravamo al minimo globale, aumentando T davamo energia al sistema
a volte il sistema finiva in un minimo, non era piu una transizione del primo ordine (torna solido per un pochino) soprattutto nel raffreddamento, non torno al minimo globale ma resto intrappolato in un altro (struttura esagonale e non FCC)

### Classificazione dei grafici

#### a palma

- minimo globale ben definito (a energie molto distante da quello sopra)
- barriere a scendere sono piccole (è facile tornare al minimo globale)

#### a salice piangente

- minimo globale ben definito
- barriere alte rispetto alle energie dei minimi stessi (es vetri: tantissimi minimi in competizione tra loro, sistemi disordinati)

#### a baniano

- minimo globale non ben definito
- degenerazione estrema delle barriere di minimo energetico -> dinamica lenta (tanti minimi equiprobabili: mi muovo orizzontalmente per trovare il minimo piu basso)

es LJ13 cluster
minimo icosaedrico 12 vertici 1 al centro
simple funnel (imbuto)

es LJ38 cluster
multifunnel
funnel rosso: quello dove siamo partiti
funnel blu: molto piu largo (ce ne sono di piu) è piu probabile finirci dentro
raffreddando non torniamo al minimo di partenza ma a un altro (configurazione atomi diversa)

es Paradosso di Levinthal

proteine sono capaci di andare a trovare la loro configurazione nativa
residuo: amminoacido in una proteina (proteina è un polimero di amminoacidi)
liberta di piegamenti della proteina e anche di conformazione dei residui
tantissimi minimi
come fa la proteina?
evolutivamente ci siamo arrivati, non è un processo completamente spontaneo (catalizzatori)
problema computazionale enorme (difficile capire la struttura dai modelli computazionali, perche questi non foldano, trovano subito i minimi globali)
problema parzialmente risolto da alphafold ML
scala di tempo $10^{-12}s$ timestep di ps
per esplorare una superficie con $10^{30}$ minimi servono $10^{18}$s
