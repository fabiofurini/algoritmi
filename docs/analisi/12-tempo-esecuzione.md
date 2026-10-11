---
title: "Tempo di esecuzione"
---

# Tempo di esecuzione

<div class="info-capitolo" markdown>

**Parte 4 · Analisi degli algoritmi · Capitolo 12** · [:material-file-pdf-box: Dispensa, volume 4 (PDF)](../pdf/dispensa-4-analisi.pdf) · [:material-pencil: Esercizi](../esercizi/es-12-tempo-esecuzione.md)

</div>

Nel capitolo «Dimensione dell'input» abbiamo imparato a misurare la dimensione $|I|$ di un'istanza di input $I$, cioè il numero di bit necessari per rappresentarla. In questo capitolo usiamo tale misura per rispondere alla domanda centrale dell'analisi degli algoritmi: <strong>come cresce il tempo richiesto da un algoritmo quando cresce l'input?</strong>

Il piano del capitolo è il seguente.

- Nella Sezione [12.1](#sez-sec-rt-definition) definiamo il tempo di esecuzione di un algoritmo, le operazioni elementari (<strong>passi</strong>) che esso esegue e il <strong>caso peggiore</strong>. Fissiamo inoltre le convenzioni con cui si contano, riga per riga, i passi di uno pseudocodice.

- Nelle Sezioni [12.2](#sez-sec-rt-findmax)–[12.5](#sez-sec-rt-primality) applichiamo il metodo a quattro algoritmi già incontrati nei capitoli precedenti: <code>FindMaximum</code>, <code>InsertionSort</code>, <code>ChangeToBase2</code> e <code>PrimalityTest</code>. Per ciascuno di essi contiamo prima il numero di passi $S(n)$ in funzione di un parametro naturale $n$, e poi esprimiamo l'ordine di crescita in funzione della dimensione dell'input $|I|$.

- Le quattro analisi portano a quattro comportamenti diversi (lineare, quadratico, lineare in $|I|$ benché logaritmico in $n$, esponenziale in $|I|$ benché solo $\Theta(\sqrt n)$ in $n$), che vengono confrontati nella Sezione [12.6](#sez-sec-rt-summary).

## 12.1 Tempo di esecuzione di un algoritmo { #sez-sec-rt-definition }

<a id="box-1-defRunningTime"></a>

!!! definizione "Definizione 12.1: tempo di esecuzione"

    Il <strong>tempo di esecuzione</strong> di un algoritmo è una stima del tempo necessario per eseguirlo, in funzione della <strong>dimensione dell'input</strong> $|I|$.

- Non ci interessa il tempo esatto in secondi, che dipende dal calcolatore, dal compilatore e da molti altri dettagli, ma l'<strong>ordine di crescita</strong> del tempo di esecuzione, espresso con la notazione asintotica $O$, $\Omega$ e $\Theta$ (capitolo 9 «Notazione asintotica», richiamata nel capitolo «Dimensione dell'input»).

- Il tempo di esecuzione di un algoritmo dipende dal numero di <strong>operazioni elementari</strong> che l'algoritmo esegue su un input di una data dimensione.

### 12.1.1 Operazioni elementari

<a id="box-2-defPrimitiveOperation"></a>

!!! definizione "Definizione 12.2: operazione elementare"

    Un'<strong>operazione elementare</strong> è una singola operazione che può essere eseguita da un calcolatore.

- Le principali operazioni elementari sono le seguenti:

    1. operazioni aritmetiche su numeri di dimensione fissata;

    2. confronto di due numeri di dimensione fissata;

    3. assegnamento di un valore a una variabile;

    4. accesso a un elemento di un array tramite indice;

    5. operazioni di controllo del flusso (per esempio, la valutazione della condizione di un'istruzione <code>if</code>, oppure l'iterazione di un ciclo).

!!! chiave ""

    Assumiamo che per eseguire ciascuna operazione elementare di un algoritmo sia richiesta una <strong>quantità di tempo costante</strong>. In questo modo l'analisi risulta il più possibile indipendente dalla macchina.

- Per brevità, chiamiamo <strong>passo</strong> ogni operazione elementare.

### 12.1.2 Contare i passi di uno pseudocodice

- Ogni riga degli pseudocodici di queste dispense esegue un numero <strong>costante</strong> di operazioni elementari (qualche confronto, operazione aritmetica e assegnamento). Poiché ci interessa l'ordine di crescita, contiamo <strong>un passo per ogni esecuzione di una riga</strong>: questo modifica il numero di passi solo per un fattore costante.

- Per contare i passi si determina, per ogni riga, quante volte viene eseguita, e si sommano questi numeri. Le convenzioni seguenti sono usate in tutto il capitolo (e nei suoi esercizi).

!!! chiave ""

    <strong>Conteggio riga per riga.</strong>

    - Ogni esecuzione di una riga numerata è <strong>un passo</strong>, comprese le righe <code>return</code>.

    - La condizione di un ciclo <code>while</code> il cui corpo viene eseguito $k$ volte viene valutata $k+1$ volte: l'ultima valutazione è quella che trova la condizione falsa e termina il ciclo.

    - La condizione di un <code>if</code> viene valutata ogni volta che si raggiunge la riga; le righe del ramo che non viene percorso non vengono eseguite.

    - Quando il numero di esecuzioni di una riga dipende dallo specifico input (e non soltanto dalla sua dimensione), lo descriviamo con una funzione ausiliaria, di solito indicata con $t$, e poi cerchiamo l'input che rende il numero totale di passi il più grande possibile.

### 12.1.3 Tempo di esecuzione nel caso peggiore

- Anche per input di una data dimensione, il tempo di esecuzione di un algoritmo può dipendere da quale specifico input di quella dimensione viene fornito.

- Tipicamente, nell'analisi degli algoritmi si considera il caso peggiore possibile, perché esso determina il tempo di esecuzione più lungo per qualunque input di una data dimensione.

<a id="box-3-defWorstCaseRunningTime"></a>

!!! definizione "Definizione 12.3: tempo di esecuzione nel caso peggiore"

    Il <strong>tempo di esecuzione nel caso peggiore</strong> $T(|I|)$ di un algoritmo è il massimo numero di passi eseguiti dall'algoritmo su un qualunque input $I$ di una data dimensione $|I|$.

- Di solito è più facile contare i passi in funzione di un <strong>parametro naturale</strong> dell'input, come il numero $n$ di elementi di un array, o il valore $n$ del numero in input. La dimensione dell'input $|I|$, invece, è il numero di bit dell'input. Questo porta al metodo seguito in tutti gli esempi del capitolo.

!!! chiave ""

    <strong>I due passi dell'analisi.</strong>

    1. Contare il numero di passi $S(n)$ eseguiti nel caso peggiore, in funzione del parametro naturale $n$, e determinarne l'ordine di crescita (per esempio $S(n)=\Theta(n^2)$).

    2. Determinare la relazione tra $n$ e la dimensione dell'input $|I|$ (per esempio $|I|=\Theta(n)$, oppure $|I|=\Theta(\log_2 n)$), e usarla per esprimere l'ordine di crescita del tempo di esecuzione nel caso peggiore $T(|I|)$.

- Il secondo passo non è una formalità: come vedremo, lo stesso numero di passi $\Theta(n)$ corrisponde a un tempo di esecuzione lineare in $|I|$ se $n$ è il numero di elementi di un array, ed esponenziale in $|I|$ se $n$ è il valore del numero in input.

## 12.2 Ricerca del massimo { #sez-sec-rt-findmax }

!!! chiave ""

    Dato un array $a[1..n]$ di $n \ge 1$ numeri interi, consideriamo il problema di determinare il valore massimo nell'array.

- Questo è lo pseudocodice di un semplice algoritmo, chiamato <code>FindMaximum</code>, che risolve il problema.

!!! algoritmo "Algoritmo: FindMaximum"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore massimo nell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMaximum(a, n)</span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max := a&#91;1&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-line-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(max&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/FindMaximum_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python di FindMaximum">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/FindMaximum_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ di FindMaximum">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/FindMaximum_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java di FindMaximum">Java</a></div>

### 12.2.1 Numero di passi

- Sia $S(n)$ il numero di passi eseguiti da <code>FindMaximum</code> nel caso peggiore, dove $n$ è la dimensione dell'array.

- Il corpo del ciclo viene eseguito per $i=2,3,\dots,n$, cioè $n-1$ volte, quindi la condizione della riga [4](#riga-12-tempo-esecuzione-line-c) viene valutata $n$ volte. L'esecuzione della riga [6](#riga-12-tempo-esecuzione-line-e), invece, dipende dall'iterazione. Definiamo una funzione

    $$
    t:\{2,3,\dots,n\}\to\{0,1\},
    $$

    dove $t(i)=1$ se la riga [6](#riga-12-tempo-esecuzione-line-e) viene eseguita all'iterazione $i$, e $t(i)=0$ altrimenti.

- Il numero di volte in cui ciascuna riga di codice viene eseguita è:

<div class="tabella" markdown="0"><table>
<tr>
<th>riga</th>
<th>numero di esecuzioni</th>
</tr>
<tr>
<td>[2](#riga-12-tempo-esecuzione-line-a)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
<tr>
<td>[3](#riga-12-tempo-esecuzione-line-b)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
<tr>
<td>[4](#riga-12-tempo-esecuzione-line-c)</td>
<td><span class="arithmatex">&#92;(n&#92;)</span></td>
</tr>
<tr>
<td>[5](#riga-12-tempo-esecuzione-line-d)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
<tr>
<td>[6](#riga-12-tempo-esecuzione-line-e)</td>
<td><span class="arithmatex">&#92;(&#92;sum&#95;{i=2}^{n} t(i)&#92;)</span></td>
</tr>
<tr>
<td>[8](#riga-12-tempo-esecuzione-line-f)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
<tr>
<td>[10](#riga-12-tempo-esecuzione-line-g)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
</table></div>

- Quindi il numero totale di passi è

    $$
    1+1+n+(n-1)+\sum_{i=2}^{n}t(i)+(n-1)+1
    =
    3n+1+\sum_{i=2}^{n}t(i).
    $$

- Il valore di $t(i)$ dipende dallo specifico array in input, quindi analizziamo il caso peggiore possibile. Il caso peggiore possibile si ha quando gli elementi dell'array sono in ordine crescente, cioè

    $$
    a[1]<a[2]<\cdots<a[n].
    $$

    Allora $t(i)=1$ per ogni $i \in \{2,3,\dots,n\}$: entriamo nell'<code>if</code> a ogni iterazione e aggiorniamo ogni volta il valore massimo. Il numero totale di passi nel caso peggiore è

    $$
    3n+1+\sum_{i=2}^{n}1
    =
    3n+1+(n-1)
    =
    4n.
    $$

- Quindi,

    $$
    S(n)=4n=\Theta(n).
    $$

    Dunque $S(n)$ cresce linearmente in $n$. Infatti,

    $$
    \lim_{n\to\infty}\frac{4n}{n}
    =
    4\in\R_{>0}.
    $$

<a id="box-4-exStepsFindMax"></a>

!!! esempio "Esempio 12.1: conteggio dei passi di FindMaximum"

    Consideriamo l'array $a[1..4]=(3,1,4,5)$.

    - Iterazione $i=2$: $a[2]=1 > 3$ è falsa, quindi $t(2)=0$.

    - Iterazione $i=3$: $a[3]=4 > 3$ è vera, $max$ diventa $4$, quindi $t(3)=1$.

    - Iterazione $i=4$: $a[4]=5 > 4$ è vera, $max$ diventa $5$, quindi $t(4)=1$.

    L'algoritmo restituisce $5$ dopo

    $$
    3\cdot 4+1+\big(t(2)+t(3)+t(4)\big)=13+2=15
    $$

    passi. Sull'array crescente $(1,2,3,4)$, invece, $t(2)=t(3)=t(4)=1$ e l'algoritmo esegue $S(4)=4\cdot 4=16$ passi, il massimo per $n=4$.

### 12.2.2 Tempo di esecuzione in funzione della dimensione dell'input

- Determiniamo ora il tempo di esecuzione nel caso peggiore dell'algoritmo, esprimendo l'ordine di crescita del numero di passi in funzione della dimensione dell'input $|I|$.

<strong>Caso generale.</strong> Poiché l'input dell'algoritmo è costituito da un array $a[1..n]$ di $n$ numeri interi, la dimensione dell'input soddisfa

$$
|I|=\Omega(n),
$$

perché l'input deve contenere almeno gli $n$ elementi dell'array. Questo significa che, per una certa costante $c>0$ e per ogni $n$ sufficientemente grande,

$$
|I|\ge c\,n.
$$

Equivalentemente,

$$
n\le \frac{1}{c}|I|,
$$

e quindi $n=O(|I|)$. Poiché $S(n)=\Theta(n)$, esiste una costante $a>0$ tale che

$$
S(n)\le a\,n
$$

per ogni $n$ sufficientemente grande. Poiché $n\le \frac{1}{c}|I|$, otteniamo

$$
S(n)\le \frac{a}{c}|I|.
$$

Dunque il numero di passi è limitato superiormente da una costante per la dimensione dell'input.

!!! chiave ""

    Il tempo di esecuzione nel caso peggiore dell'algoritmo <code>FindMaximum</code>, in funzione della dimensione dell'input $|I|$, è

    $$
    T(|I|)=O(|I|).
    $$

    Dunque, nel caso generale, il tempo di esecuzione nel caso peggiore è al più lineare nella dimensione dell'input.

<strong>Elementi con un numero fissato di bit.</strong> Spesso si fa l'ipotesi che tutti i valori dell'input possano essere memorizzati usando un numero costante fissato di bit, per esempio $32$ bit. Sotto questa ipotesi, la dimensione dell'input soddisfa

$$
|I|=\Theta(n),
$$

perché l'input è costituito da $n$ elementi dell'array e ciascun elemento richiede un numero costante di bit. Questo significa che esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

$$
c_1 n \le |I| \le c_2 n.
$$

Equivalentemente,

$$
\frac{1}{c_2}|I| \le n \le \frac{1}{c_1}|I|,
$$

cioè $n=\Theta(|I|)$. Poiché $S(n)=\Theta(n)$, esistono costanti $a_1,a_2>0$ tali che, per ogni $n$ sufficientemente grande,

$$
a_1 n \le S(n) \le a_2 n.
$$

Usando i limiti su $n$ in funzione di $|I|$, otteniamo

$$
\frac{a_1}{c_2}|I| \le S(n) \le \frac{a_2}{c_1}|I|,
$$

cioè $S(n)=\Theta(|I|)$.

!!! chiave ""

    Se tutti i valori dell'input usano un numero costante fissato di bit, allora il tempo di esecuzione nel caso peggiore dell'algoritmo <code>FindMaximum</code> è

    $$
    T(|I|)=\Theta(|I|).
    $$

    Dunque, sotto questa ipotesi, l'algoritmo è lineare nella dimensione dell'input.

## 12.3 Insertion sort { #sez-sec-rt-insertion }

- In <code>FindMaximum</code> il corpo del ciclo esegue un numero costante di passi. In <code>InsertionSort</code> il corpo del ciclo esterno contiene un altro ciclo, il cui numero di iterazioni dipende dall'input: questo produce un numero quadratico di passi.

!!! chiave ""

    Dato un array $a[1..n]$ di $n$ numeri naturali, consideriamo il problema di ordinare l'array in ordine non decrescente:

    $$
    a[1] \le a[2] \le \cdots \le a[n].
    $$

- Questo è lo pseudocodice dell'algoritmo <code>InsertionSort</code>.

!!! algoritmo "Algoritmo: InsertionSort"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array <span class="arithmatex">&#92;(a&#92;)</span> ordinato in ordine non decrescente</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> InsertionSort(a, n)</span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(key := a&#91;i&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := i - 1&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;ge 1&#92;)</span> <strong>and</strong> <span class="arithmatex">&#92;(a&#91;j&#93; &gt; key&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;j+1&#93; &#92;leftarrow a&#91;j&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j - 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;j+1&#93; &#92;leftarrow key&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-ins-i"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/InsertionSort_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python di InsertionSort">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/InsertionSort_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ di InsertionSort">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/InsertionSort_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java di InsertionSort">Java</a></div>

### 12.3.1 Numero di passi

- Sia $S(n)$ il numero di passi eseguiti da <code>InsertionSort</code> nel caso peggiore, dove $n$ è la dimensione dell'array.

- L'esecuzione delle righe [7](#riga-12-tempo-esecuzione-ins-f)–[8](#riga-12-tempo-esecuzione-ins-g) dipende dall'iterazione. Definiamo una funzione

    $$
    t:\{2,3,\dots,n\}\to\{0,1,\dots,n-1\},
    $$

    dove $t(i)$ indica il numero di volte in cui il corpo del ciclo interno (righe [7](#riga-12-tempo-esecuzione-ins-f)–[8](#riga-12-tempo-esecuzione-ins-g)) viene eseguito durante l'iterazione $i$ del ciclo esterno. La condizione del ciclo interno (riga [6](#riga-12-tempo-esecuzione-ins-e)) viene quindi valutata $t(i)+1$ volte durante la stessa iterazione.

- Il numero di volte in cui ciascuna riga di codice viene eseguita è:

<div class="tabella" markdown="0"><table>
<tr>
<th>riga</th>
<th>numero di esecuzioni</th>
</tr>
<tr>
<td>[2](#riga-12-tempo-esecuzione-ins-a)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
<tr>
<td>[3](#riga-12-tempo-esecuzione-ins-b)</td>
<td><span class="arithmatex">&#92;(n&#92;)</span></td>
</tr>
<tr>
<td>[4](#riga-12-tempo-esecuzione-ins-c)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
<tr>
<td>[5](#riga-12-tempo-esecuzione-ins-d)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
<tr>
<td>[6](#riga-12-tempo-esecuzione-ins-e)</td>
<td><span class="arithmatex">&#92;(&#92;displaystyle(n-1)+&#92;sum&#95;{i=2}^{n}t(i)&#92;)</span></td>
</tr>
<tr>
<td>[7](#riga-12-tempo-esecuzione-ins-f)</td>
<td><span class="arithmatex">&#92;(&#92;displaystyle&#92;sum&#95;{i=2}^{n}t(i)&#92;)</span></td>
</tr>
<tr>
<td>[8](#riga-12-tempo-esecuzione-ins-g)</td>
<td><span class="arithmatex">&#92;(&#92;displaystyle&#92;sum&#95;{i=2}^{n}t(i)&#92;)</span></td>
</tr>
<tr>
<td>[10](#riga-12-tempo-esecuzione-ins-h)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
<tr>
<td>[11](#riga-12-tempo-esecuzione-ins-i)</td>
<td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
</tr>
</table></div>

- Quindi il numero totale di passi è

    $$
    \begin{aligned}
    &1 + n + (n-1) + (n-1) + \left((n-1)+\sum_{i=2}^{n}t(i)\right) + \sum_{i=2}^{n}t(i) + \sum_{i=2}^{n}t(i) + (n-1) + (n-1)\\
    &\qquad =
    6n - 4 + 3\sum_{i=2}^{n}t(i).
    \end{aligned}
    $$

- Il valore di $t(i)$ dipende dallo specifico array in input, quindi analizziamo il caso peggiore possibile. Poiché $j$ parte da $i-1$ e decresce al più fino a $0$, si ha sempre $t(i)\le i-1$. Il caso peggiore possibile si ha quando gli elementi dell'array sono in ordine strettamente decrescente, cioè

    $$
    a[1]>a[2]>\cdots>a[n].
    $$

    In questo caso, a ogni iterazione esterna $i$, l'elemento $key=a[i]$ è più piccolo di tutti gli elementi che lo precedono. Quindi il ciclo while interno viene eseguito fino in fondo:

    $$
    t(i)=i-1
    \qquad
    \forall i \in \{2,3,\dots,n\}.
    $$

    Perciò,

    $$
    \sum_{i=2}^{n}t(i)=\sum_{i=2}^{n}(i-1)
    =
    1+2+\cdots+(n-1)
    =\frac{n(n-1)}{2}.
    $$

- Il numero totale di passi nel caso peggiore è

    $$
    6n-4+3\cdot\frac{n(n-1)}{2}
    =
    \frac{12n-8+3n^2-3n}{2}
    =
    \frac{3n^2+9n-8}{2}.
    $$

    Quindi,

    $$
    S(n)=\frac{3n^2+9n-8}{2}=\Theta(n^2).
    $$

    Dunque $S(n)$ cresce quadraticamente in $n$. Infatti,

    $$
    \lim_{n\to\infty}
    \frac{3n^2+9n-8}{2n^2}
    =
    \lim_{n\to\infty}
    \frac{1}{2}\left(3+\frac{9}{n}-\frac{8}{n^2}\right)
    =
    \frac{3}{2}\in\R_{>0}.
    $$

<a id="box-5-exStepsInsertion"></a>

!!! esempio "Esempio 12.2: la funzione $t$ di InsertionSort"

    Consideriamo l'array $a[1..6]=(5,2,4,6,1,3)$. A ogni iterazione $i$, $t(i)$ è il numero di elementi di $a[1..i-1]$ più grandi di $key=a[i]$, cioè il numero di elementi spostati di una posizione verso destra.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(key&#92;)</span></th>
    <th><span class="arithmatex">&#92;(t(i)&#92;)</span></th>
    <th>array dopo l'iterazione</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;((2,5,4,6,1,3)&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;((2,4,5,6,1,3)&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;((2,4,5,6,1,3)&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;((1,2,4,5,6,3)&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;((1,2,3,4,5,6)&#92;)</span></td>
    </tr>
    </table></div>

    Abbiamo $\sum_{i=2}^{6} t(i)=9$, quindi l'algoritmo esegue

    $$
    6\cdot 6-4+3\cdot 9=59
    $$

    passi. Su un array decrescente di $6$ elementi, invece, $\sum_{i=2}^{6} t(i)=1+2+3+4+5=15$ e l'algoritmo esegue

    $$
    S(6)=\frac{3\cdot 36+9\cdot 6-8}{2}=77
    $$

    passi.

### 12.3.2 Tempo di esecuzione in funzione della dimensione dell'input

- Determiniamo ora il tempo di esecuzione nel caso peggiore dell'algoritmo, esprimendo l'ordine di crescita del numero di passi in funzione della dimensione dell'input $|I|$.

<strong>Caso generale.</strong> Poiché l'input dell'algoritmo è costituito da un array $a[1..n]$ di $n$ numeri naturali, la dimensione dell'input soddisfa

$$
|I|=\Omega(n),
$$

perché l'input deve contenere almeno gli $n$ elementi dell'array. Questo significa che, per una certa costante $c>0$ e per ogni $n$ sufficientemente grande,

$$
|I|\ge c\,n.
$$

Equivalentemente,

$$
n\le \frac{1}{c}|I|,
$$

e quindi $n=O(|I|)$. Poiché $S(n)=\Theta(n^2)$, esiste una costante $a>0$ tale che

$$
S(n)\le a\,n^2
$$

per ogni $n$ sufficientemente grande. Poiché $n\le \frac{1}{c}|I|$, otteniamo

$$
S(n)\le a\left(\frac{1}{c}|I|\right)^2
=
\frac{a}{c^2}|I|^2.
$$

Dunque il numero di passi è limitato superiormente da una costante per $|I|^2$.

!!! chiave ""

    Il tempo di esecuzione nel caso peggiore dell'algoritmo <code>InsertionSort</code>, in funzione della dimensione dell'input $|I|$, è

    $$
    T(|I|)=O(|I|^2).
    $$

    Dunque, nel caso generale, il tempo di esecuzione nel caso peggiore è al più quadratico nella dimensione dell'input.

<strong>Elementi con un numero fissato di bit.</strong> Spesso si fa l'ipotesi che tutti i valori dell'input possano essere memorizzati usando un numero costante fissato di bit, per esempio $32$ bit. Sotto questa ipotesi, la dimensione dell'input soddisfa

$$
|I|=\Theta(n),
$$

perché l'input è costituito da $n$ elementi dell'array e ciascun elemento richiede un numero costante di bit. Questo significa che esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

$$
c_1 n \le |I| \le c_2 n.
$$

Equivalentemente,

$$
\frac{1}{c_2}|I| \le n \le \frac{1}{c_1}|I|.
$$

Poiché $S(n)=\Theta(n^2)$, esistono costanti $a_1,a_2>0$ tali che, per ogni $n$ sufficientemente grande,

$$
a_1 n^2 \le S(n) \le a_2 n^2.
$$

Usando i limiti su $n$ in funzione di $|I|$, otteniamo

$$
a_1\left(\frac{1}{c_2}|I|\right)^2
\le S(n) \le
a_2\left(\frac{1}{c_1}|I|\right)^2,
\qquad\text{cioè}\qquad
\frac{a_1}{c_2^2}|I|^2
\le S(n) \le
\frac{a_2}{c_1^2}|I|^2.
$$

Dunque $S(n)=\Theta(|I|^2)$.

!!! chiave ""

    Se tutti i valori dell'input usano un numero costante fissato di bit, allora il tempo di esecuzione nel caso peggiore dell'algoritmo <code>InsertionSort</code> è

    $$
    T(|I|)=\Theta(|I|^2).
    $$

    Dunque, sotto questa ipotesi, l'algoritmo è quadratico nella dimensione dell'input.

## 12.4 Cambio di base { #sez-sec-rt-changebase }

- Nei primi due esempi l'input è un array e il parametro naturale $n$ è il numero dei suoi elementi. Consideriamo ora un algoritmo il cui input è un <strong>singolo numero</strong> $n$: il parametro $n$ è ora un valore, e la relazione tra $n$ e $|I|$ cambia completamente.

!!! chiave ""

    Dato un numero naturale $n \ge 1$ rappresentato in base $10$, consideriamo il problema di convertire $n$ in base $2$.

- Questo è lo pseudocodice dell'algoritmo <code>ChangeToBase2</code>. È l'algoritmo <code>ChangeOfBase</code> del capitolo «Algoritmi numerici», con base $b=2$. Le cifre binarie sono memorizzate in un array $d[0..nd-1]$ indicizzato a partire da $0$, in modo che $d[k]$ sia la cifra di peso $2^k$.

!!! algoritmo "Algoritmo: ChangeToBase2"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> in base <span class="arithmatex">&#92;(10&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un array <span class="arithmatex">&#92;(d&#92;)</span> di cifre binarie e il numero di cifre <span class="arithmatex">&#92;(nd&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ChangeToBase2(n)</span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(nd := &#92;lfloor &#92;log&#95;2 n &#92;rfloor + 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d :=&#92;)</span> nuovo array<span class="arithmatex">&#92;(&#91;0..nd-1&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(k := 0&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(n &gt; 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(q := &#92;lfloor n / 2 &#92;rfloor&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r := n &#92;bmod 2&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d&#91;k&#93; &#92;leftarrow r&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-h"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow q&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-i"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(k &#92;leftarrow k + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-cob-j"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(d, nd&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/ChangeToBase2_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python di ChangeToBase2">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/ChangeToBase2_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ di ChangeToBase2">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/ChangeToBase2_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java di ChangeToBase2">Java</a></div>

### 12.4.1 Numero di passi

- Sia $S(n)$ il numero di passi eseguiti da <code>ChangeToBase2</code>, dove $n$ è il valore in input da convertire. Per ogni valore di $n$ c'è un solo input, quindi non c'è distinzione tra il caso peggiore e gli altri casi.

- Il numero di cifre necessarie per rappresentare $n$ in base $2$ è

    $$
    \lfloor\log_2 n\rfloor+1.
    $$

    A ogni iterazione del ciclo while, il valore corrente di $n$ viene sostituito con $\lfloor n/2\rfloor$. Dopo $s$ iterazioni, il valore corrente è

    $$
    \left\lfloor \frac{n}{2^s}\right\rfloor.
    $$

    Il ciclo termina quando questo valore diventa $0$, cioè quando

    $$
    \left\lfloor \frac{n}{2^s}\right\rfloor=0.
    $$

    Questo accade esattamente quando $2^s>n$. Il più piccolo intero $s$ tale che $2^s>n$ è

    $$
    s=\lfloor\log_2 n\rfloor+1.
    $$

    Quindi il corpo del ciclo while viene eseguito esattamente $\lfloor\log_2 n\rfloor+1$ volte (un'iterazione per ogni cifra binaria), e la sua condizione viene valutata $\lfloor\log_2 n\rfloor+2$ volte.

- Il numero di volte in cui ciascuna riga di codice viene eseguita è:

<div class="tabella" markdown="0"><table>
<tr>
<th>riga</th>
<th>numero di esecuzioni</th>
</tr>
<tr>
<td>[2](#riga-12-tempo-esecuzione-cob-a), [3](#riga-12-tempo-esecuzione-cob-b), [4](#riga-12-tempo-esecuzione-cob-c)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span> ciascuna</td>
</tr>
<tr>
<td>[5](#riga-12-tempo-esecuzione-cob-d)</td>
<td><span class="arithmatex">&#92;(&#92;lfloor&#92;log&#95;2 n&#92;rfloor+2&#92;)</span></td>
</tr>
<tr>
<td>[6](#riga-12-tempo-esecuzione-cob-e), [7](#riga-12-tempo-esecuzione-cob-f), [8](#riga-12-tempo-esecuzione-cob-g), [9](#riga-12-tempo-esecuzione-cob-h), [10](#riga-12-tempo-esecuzione-cob-i)</td>
<td><span class="arithmatex">&#92;(&#92;lfloor&#92;log&#95;2 n&#92;rfloor+1&#92;)</span> ciascuna</td>
</tr>
<tr>
<td>[12](#riga-12-tempo-esecuzione-cob-j)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
</table></div>

- Quindi il numero totale di passi è

    $$
    1+1+1+(\lfloor\log_2 n\rfloor+2)+5(\lfloor\log_2 n\rfloor+1)+1
    =
    6(\lfloor\log_2 n\rfloor+1)+5
    =
    6\lfloor\log_2 n\rfloor+11.
    $$

    Quindi,

    $$
    S(n)=6\lfloor\log_2 n\rfloor+11=\Theta(\log_2 n).
    $$

    In parole, il numero di passi cresce in modo logaritmico nel valore numerico $n$.

- Infatti, per $n>1$,

    $$
    \log_2 n -1
    <
    \lfloor \log_2 n \rfloor
    \le
    \log_2 n.
    $$

    Dividendo per $\log_2 n>0$, otteniamo

    $$
    1-\frac{1}{\log_2 n}
    <
    \frac{\lfloor \log_2 n \rfloor}{\log_2 n}
    \le
    1.
    $$

    Poiché sia $1-\frac{1}{\log_2 n}$ sia $1$ convergono a $1$, per il teorema del confronto (dei due carabinieri),

    $$
    \lim_{n\to\infty}
    \frac{\lfloor \log_2 n \rfloor}{\log_2 n}
    =1.
    $$

    Quindi,

    $$
    \lim_{n\to\infty}
    \frac{6\lfloor\log_2 n\rfloor+11}{\log_2 n}
    =
    \lim_{n\to\infty}
    \left(
    6\,\frac{\lfloor\log_2 n\rfloor}{\log_2 n}
    +
    \frac{11}{\log_2 n}
    \right)
    =
    6\cdot 1+0
    =
    6\in\R_{>0}.
    $$

<a id="box-6-exStepsChangeBase"></a>

!!! esempio "Esempio 12.3: ChangeToBase2 su $n=13$"

    Abbiamo $\lfloor\log_2 13\rfloor+1=4$, quindi viene creato l'array $d[0..3]$ e il ciclo esegue $4$ iterazioni:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>iterazione</th>
    <th><span class="arithmatex">&#92;(n&#92;)</span></th>
    <th><span class="arithmatex">&#92;(q=&#92;lfloor n/2&#92;rfloor&#92;)</span></th>
    <th><span class="arithmatex">&#92;(r=n &#92;bmod 2&#92;)</span></th>
    <th>assegnamento</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(13&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d&#91;0&#93;=1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d&#91;1&#93;=0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d&#91;2&#93;=1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d&#91;3&#93;=1&#92;)</span></td>
    </tr>
    </table></div>

    Dopo la quarta iterazione $n=0$: la condizione della riga [5](#riga-12-tempo-esecuzione-cob-d) viene valutata per la quinta volta, è falsa, e l'algoritmo restituisce le cifre di $13=(1101)_2$. Il numero di passi è

    $$
    S(13)=3+5+5\cdot 4+1=29=6\cdot 3+11.
    $$

### 12.4.2 Tempo di esecuzione in funzione della dimensione dell'input

- Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input $|I|$. Questo è il delicato cambio di variabile.

- L'input non è il valore astratto $n$, ma una rappresentazione di $n$. Poiché $n$ è rappresentato in base $10$, il numero di cifre necessarie per scrivere $n$ è

    $$
    \lfloor\log_{10} n\rfloor+1.
    $$

    Ogni cifra decimale richiede un numero costante di bit. Quindi la dimensione dell'input soddisfa

    $$
    |I|=\Theta(\lfloor\log_{10} n\rfloor+1)=\Theta(\log_{10} n).
    $$

    Poiché il cambio di base di un logaritmo lo modifica solo per un fattore costante ($\log_{10} n=\log_2 n/\log_2 10$), otteniamo

    $$
    |I|=\Theta(\log_2 n),
    $$

    lo stesso ordine di crescita ottenuto nel capitolo «Dimensione dell'input» per un numero scritto in binario. Questo significa che esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    c_1\log_2 n \le |I| \le c_2\log_2 n.
    $$

    Equivalentemente,

    $$
    \frac{1}{c_2}|I| \le \log_2 n \le \frac{1}{c_1}|I|.
    $$

- Poiché $S(n)=\Theta(\log_2 n)$, esistono costanti $a_1,a_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    a_1\log_2 n \le S(n) \le a_2\log_2 n.
    $$

    Usando i limiti su $\log_2 n$ in funzione di $|I|$, otteniamo

    $$
    \frac{a_1}{c_2}|I| \le S(n) \le \frac{a_2}{c_1}|I|,
    $$

    cioè $S(n)=\Theta(|I|)$.

!!! chiave ""

    Il tempo di esecuzione dell'algoritmo <code>ChangeToBase2</code> è

    $$
    T(|I|)=\Theta(|I|).
    $$

    Dunque l'algoritmo è logaritmico nel valore numerico $n$, ma lineare nella dimensione dell'input $|I|$, perché la dimensione dell'input è essa stessa proporzionale a $\log_2 n$.

## 12.5 Test di primalità { #sez-sec-rt-primality }

- L'input dell'ultimo esempio è di nuovo un singolo numero $n$, ma ora il numero di passi cresce come $\sqrt{n}$, molto più rapidamente di $\log_2 n$. Vedremo che questo rende l'algoritmo esponenziale nella dimensione dell'input.

!!! chiave ""

    Dato un numero naturale $n$, consideriamo il problema di determinare se $n$ è un numero primo.

- Questo è lo pseudocodice dell'algoritmo <code>PrimalityTest</code> del capitolo «Algoritmi numerici».

!!! algoritmo "Algoritmo: PrimalityTest"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><code>true</code> se <span class="arithmatex">&#92;(n&#92;)</span> è primo, <code>false</code> altrimenti</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> PrimalityTest(n)</span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &lt; 2&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d := 2&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(d &#92;le &#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;bmod d = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d &#92;leftarrow d + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-12-tempo-esecuzione-pt-h"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>true</code></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/PrimalityTest_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python di PrimalityTest">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/PrimalityTest_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ di PrimalityTest">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap12_tempo_esecuzione/PrimalityTest_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java di PrimalityTest">Java</a></div>

### 12.5.1 Numero di passi

- Sia $S(n)$ il numero di passi eseguiti da <code>PrimalityTest</code> nel caso peggiore, dove $n$ è il valore in input. Assumiamo $n \ge 2$, perché per $n<2$ l'algoritmo si ferma dopo $2$ passi.

- <strong>Il caso peggiore si ha quando $n$ è primo.</strong> In questo caso l'algoritmo non esce mai in anticipo alla riga [8](#riga-12-tempo-esecuzione-pt-f), quindi il ciclo while viene eseguito fino in fondo. La variabile $d$ assume i valori

    $$
    2,3,\dots,\lfloor\sqrt{n}\rfloor,
    $$

    quindi il corpo del ciclo while viene eseguito $\lfloor\sqrt{n}\rfloor-1$ volte. La condizione del ciclo while viene valutata ancora una volta, quando $d=\lfloor\sqrt{n}\rfloor+1$, quindi la riga [6](#riga-12-tempo-esecuzione-pt-d) viene eseguita $\lfloor\sqrt{n}\rfloor$ volte.

- Il numero di volte in cui ciascuna riga di codice viene eseguita nel caso peggiore è:

<div class="tabella" markdown="0"><table>
<tr>
<th>riga</th>
<th>numero di esecuzioni (<span class="arithmatex">&#92;(n&#92;)</span> primo)</th>
</tr>
<tr>
<td>[2](#riga-12-tempo-esecuzione-pt-a)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
<tr>
<td>[3](#riga-12-tempo-esecuzione-pt-b)</td>
<td><span class="arithmatex">&#92;(0&#92;)</span>   (poiché <span class="arithmatex">&#92;(n &#92;ge 2&#92;)</span>)</td>
</tr>
<tr>
<td>[5](#riga-12-tempo-esecuzione-pt-c)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
<tr>
<td>[6](#riga-12-tempo-esecuzione-pt-d)</td>
<td><span class="arithmatex">&#92;(&#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span></td>
</tr>
<tr>
<td>[7](#riga-12-tempo-esecuzione-pt-e)</td>
<td><span class="arithmatex">&#92;(&#92;lfloor&#92;sqrt{n}&#92;rfloor-1&#92;)</span></td>
</tr>
<tr>
<td>[8](#riga-12-tempo-esecuzione-pt-f)</td>
<td><span class="arithmatex">&#92;(0&#92;)</span>   (poiché <span class="arithmatex">&#92;(n&#92;)</span> è primo)</td>
</tr>
<tr>
<td>[10](#riga-12-tempo-esecuzione-pt-g)</td>
<td><span class="arithmatex">&#92;(&#92;lfloor&#92;sqrt{n}&#92;rfloor-1&#92;)</span></td>
</tr>
<tr>
<td>[12](#riga-12-tempo-esecuzione-pt-h)</td>
<td><span class="arithmatex">&#92;(1&#92;)</span></td>
</tr>
</table></div>

- Quindi il numero totale di passi nel caso peggiore è

    $$
    1 + 1 + \lfloor\sqrt{n}\rfloor
    + (\lfloor\sqrt{n}\rfloor-1)
    + (\lfloor\sqrt{n}\rfloor-1)
    + 1
    =
    3\lfloor\sqrt{n}\rfloor + 1.
    $$

- Questo è effettivamente il caso peggiore. Se $n \ge 2$ non è primo, sia $p$ il suo più piccolo divisore maggiore di $1$: allora $p \le \lfloor\sqrt{n}\rfloor$, e l'algoritmo restituisce <code>false</code> alla riga [8](#riga-12-tempo-esecuzione-pt-f) quando $d=p$. La riga [6](#riga-12-tempo-esecuzione-pt-d) viene eseguita $p-1$ volte, la riga [7](#riga-12-tempo-esecuzione-pt-e) $p-1$ volte, la riga [10](#riga-12-tempo-esecuzione-pt-g) $p-2$ volte, e le righe [2](#riga-12-tempo-esecuzione-pt-a), [5](#riga-12-tempo-esecuzione-pt-c), [8](#riga-12-tempo-esecuzione-pt-f) una volta ciascuna, per un totale di

    $$
    3p-1 \;\le\; 3\lfloor\sqrt{n}\rfloor-1 \;<\; 3\lfloor\sqrt{n}\rfloor+1
    $$

    passi.

- Quindi,

    $$
    S(n)=3\lfloor\sqrt{n}\rfloor + 1=\Theta(\sqrt{n}).
    $$

    Dunque $S(n)$ cresce come la radice quadrata di $n$. Infatti,

    $$
    \sqrt{n}-1 < \lfloor\sqrt{n}\rfloor \le \sqrt{n}.
    $$

    Dividendo per $\sqrt{n}>0$, otteniamo

    $$
    1-\frac{1}{\sqrt{n}}
    <
    \frac{\lfloor\sqrt{n}\rfloor}{\sqrt{n}}
    \le
    1.
    $$

    Poiché sia $1-\frac{1}{\sqrt{n}}$ sia $1$ convergono a $1$, per il teorema del confronto (dei due carabinieri),

    $$
    \lim_{n\to\infty}
    \frac{\lfloor\sqrt{n}\rfloor}{\sqrt{n}}
    =1.
    $$

    Quindi,

    $$
    \lim_{n\to\infty}
    \frac{3\lfloor\sqrt{n}\rfloor+1}{\sqrt{n}}
    =
    \lim_{n\to\infty}
    \left(
    3\,\frac{\lfloor\sqrt{n}\rfloor}{\sqrt{n}}
    +
    \frac{1}{\sqrt{n}}
    \right)
    =
    3\cdot 1+0
    =
    3\in\R_{>0}.
    $$

<a id="box-7-exStepsPrimality"></a>

!!! esempio "Esempio 12.4: PrimalityTest su un numero primo e su un numero composto"

    - $n=97$ è primo e $\lfloor\sqrt{97}\rfloor=9$. L'algoritmo prova i divisori $d=2,3,\dots,9$ ($8$ iterazioni), non trova alcun divisore, valuta una nona volta la condizione della riga [6](#riga-12-tempo-esecuzione-pt-d) con $d=10$, e restituisce <code>true</code> dopo

        $$
        S(97)=3\cdot 9+1=28
        $$

        passi.

    - $n=91=7\cdot 13$ non è primo, e il suo più piccolo divisore maggiore di $1$ è $p=7$. L'algoritmo prova $d=2,3,\dots,6$ senza successo, trova $91 \bmod 7=0$, e restituisce <code>false</code> dopo

        $$
        3\cdot 7-1=20
        $$

        passi, anche se $\lfloor\sqrt{91}\rfloor=9$ come per $97$.

### 12.5.2 Tempo di esecuzione in funzione della dimensione dell'input

- Determiniamo ora il tempo di esecuzione nel caso peggiore, esprimendo l'ordine di crescita del numero di passi in funzione della dimensione dell'input $|I|$.

- L'input è un singolo numero naturale $n$. Per rappresentare $n$ in binario servono $\lfloor\log_2 n\rfloor+1$ bit, quindi la dimensione dell'input soddisfa

    $$
    |I| = \Theta(\log_2 n).
    $$

    Questo significa che esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    c_1\log_2 n \le |I| \le c_2\log_2 n.
    $$

    Equivalentemente,

    $$
    \frac{1}{c_2}|I| \le \log_2 n \le \frac{1}{c_1}|I|.
    $$

    La funzione $x \mapsto 2^x$ è strettamente crescente. Quindi, applicare $2^x$ a tutti i termini della disuguaglianza ne preserva l'ordine:

    $$
    2^{\frac{1}{c_2}|I|}
    \le
    2^{\log_2 n}
    \le
    2^{\frac{1}{c_1}|I|}.
    $$

    Poiché $2^{\log_2 n}=n$, otteniamo

    $$
    2^{\frac{1}{c_2}|I|}
    \le
    n
    \le
    2^{\frac{1}{c_1}|I|}.
    $$

    Inoltre, $\sqrt{n}=n^{1/2}$. Estraendo la radice quadrata di tutti i termini, il che di nuovo preserva l'ordine perché tutti i termini sono positivi, e usando $(2^x)^{1/2}=2^{x/2}$, otteniamo

    $$
    2^{\frac{1}{2c_2}|I|}
    \le
    \sqrt{n}
    \le
    2^{\frac{1}{2c_1}|I|}.
    $$

- Poiché $S(n)=\Theta(\sqrt{n})$, esistono costanti $a_1,a_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    a_1\sqrt{n}
    \le
    S(n)
    \le
    a_2\sqrt{n}.
    $$

    Usando i limiti su $\sqrt{n}$ in funzione di $|I|$, otteniamo

    $$
    a_1\, 2^{\frac{1}{2c_2}|I|}
    \le
    S(n)
    \le
    a_2\, 2^{\frac{1}{2c_1}|I|}.
    $$

    Dunque,

    $$
    S(n)=2^{\Theta(|I|)}.
    $$

- Il caso peggiore viene raggiunto sui numeri primi, e ci sono numeri primi di ogni dimensione: per ogni $k \ge 2$ esiste un numero primo con esattamente $k$ cifre binarie, cioè compreso tra $2^{k-1}$ e $2^k$ (postulato di Bertrand). Quindi, per ogni dimensione dell'input, il massimo numero di passi è raggiunto da un primo $n$ e soddisfa i limiti precedenti.

!!! chiave ""

    Il tempo di esecuzione nel caso peggiore dell'algoritmo <code>PrimalityTest</code>, in funzione della dimensione dell'input $|I|$, è

    $$
    T(|I|) = 2^{\Theta(|I|)}.
    $$

    Di conseguenza, l'ordine di crescita del tempo di esecuzione nel caso peggiore dell'algoritmo <code>PrimalityTest</code> è <strong>esponenziale</strong> nella dimensione dell'input.

## 12.6 Riepilogo { #sez-sec-rt-summary }

- La tabella seguente raccoglie i risultati del capitolo. Per i due algoritmi su array, il tempo di esecuzione è dato sotto l'ipotesi che tutti gli elementi usino un numero costante fissato di bit.

<div class="tabella" markdown="0"><table>
<tr>
<th>algoritmo</th>
<th>parametro <span class="arithmatex">&#92;(n&#92;)</span></th>
<th>passi nel caso peggiore <span class="arithmatex">&#92;(S(n)&#92;)</span></th>
<th>dimensione dell'input <span class="arithmatex">&#92;(|I|&#92;)</span></th>
<th>tempo di esecuzione <span class="arithmatex">&#92;(T(|I|)&#92;)</span></th>
</tr>
<tr>
<td><code>FindMaximum</code></td>
<td>elementi dell'array</td>
<td><span class="arithmatex">&#92;(4n=&#92;Theta(n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(|I|)&#92;)</span></td>
</tr>
<tr>
<td><code>InsertionSort</code></td>
<td>elementi dell'array</td>
<td><span class="arithmatex">&#92;(&#92;frac{3n^2+9n-8}{2}=&#92;Theta(n^2)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(|I|^2)&#92;)</span></td>
</tr>
<tr>
<td><code>ChangeToBase2</code></td>
<td>valore del numero</td>
<td><span class="arithmatex">&#92;(6&#92;lfloor&#92;log&#95;2 n&#92;rfloor+11=&#92;Theta(&#92;log&#95;2 n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(&#92;log&#95;2 n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(|I|)&#92;)</span></td>
</tr>
<tr>
<td><code>PrimalityTest</code></td>
<td>valore del numero</td>
<td><span class="arithmatex">&#92;(3&#92;lfloor&#92;sqrt{n}&#92;rfloor+1=&#92;Theta(&#92;sqrt{n})&#92;)</span></td>
<td><span class="arithmatex">&#92;(&#92;Theta(&#92;log&#95;2 n)&#92;)</span></td>
<td><span class="arithmatex">&#92;(2^{&#92;Theta(|I|)}&#92;)</span></td>
</tr>
</table></div>

!!! chiave ""

    <strong>Punti chiave.</strong>

    - Il tempo di esecuzione si misura in <strong>passi</strong> (operazioni elementari, ciascuna eseguita in tempo costante); contiamo un passo per ogni esecuzione di una riga di pseudocodice.

    - Consideriamo il <strong>caso peggiore</strong>: il massimo numero di passi su tutti gli input di una data dimensione. Quando il numero di esecuzioni di una riga dipende dall'input, una funzione ausiliaria $t$ lo descrive, e cerchiamo l'input che massimizza il totale.

    - L'analisi ha <strong>due passi</strong>: prima il numero di passi $S(n)$ in funzione di un parametro naturale $n$, poi il tempo di esecuzione $T(|I|)$ in funzione della dimensione dell'input.

    - Se $n$ è il numero di elementi di un array (con elementi di dimensione fissata), allora $|I|=\Theta(n)$ e l'ordine di crescita non cambia: $S(n)=\Theta(n^k)$ dà $T(|I|)=\Theta(|I|^k)$.

    - Se $n$ è il <strong>valore</strong> del numero in input, allora $|I|=\Theta(\log_2 n)$, cioè $n=2^{\Theta(|I|)}$: un numero di passi $\Theta(\log_2 n)$ è lineare in $|I|$, mentre un numero di passi $\Theta(\sqrt{n})$ o $\Theta(n)$ è <strong>esponenziale</strong> in $|I|$.
