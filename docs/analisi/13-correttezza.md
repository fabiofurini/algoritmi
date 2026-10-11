---
title: "Correttezza"
---

# Correttezza

<div class="info-capitolo" markdown>

**Parte 4 · Analisi degli algoritmi · Capitolo 13** · [:material-file-pdf-box: Dispensa, volume 4 (PDF)](../pdf/dispensa-4-analisi.pdf) · [:material-pencil: Esercizi](../esercizi/es-13-correttezza.md)

</div>

## 13.1 Correttezza di un algoritmo

- I capitoli precedenti hanno misurato quanto costa un algoritmo: la dimensione del suo input e il suo tempo di esecuzione. Prima di chiedersi quanto sia veloce un algoritmo, però, dobbiamo essere sicuri che faccia ciò che promette. Questo capitolo presenta lo strumento standard per dimostrarlo, l'<strong>invariante di ciclo</strong>, e lo applica ad algoritmi già incontrati nei capitoli «Ordinamento», «Ricerca lineare e ricerca binaria» e «Algoritmi numerici»: Find Maximum, Insertion Sort, Binary Search e l'algoritmo di Euclide.

- La prima parte dell'analisi di un algoritmo consiste nel determinarne la <strong>correttezza</strong>, cioè nel dimostrare che calcola l'output corretto per ogni possibile istanza di input.

- Provare un algoritmo su alcune istanze può mostrare che è sbagliato (basta un controesempio), ma non può mai mostrare che è corretto: le istanze di input sono infinite. La correttezza va <strong>dimostrata</strong>.

<a id="box-1-defCorrectAlgorithm"></a>

!!! definizione "Definizione 13.1: algoritmo corretto"

    Un algoritmo è <strong>corretto</strong> se, per ogni istanza di input $I$ del problema, <strong>termina</strong> dopo un numero finito di passi e <strong>restituisce l'output corretto</strong> per $I$.

- Gli algoritmi che consideriamo sono costituiti da sequenze di istruzioni e da cicli. Le sequenze di istruzioni sono facili da analizzare, mentre un ciclo esegue le stesse istruzioni un numero di volte che dipende dall'input.

!!! chiave ""

    La correttezza di un algoritmo si basa sulla correttezza dei suoi cicli. La correttezza di un ciclo si dimostra per mezzo di un <strong>invariante di ciclo</strong>.

### 13.1.1 Invarianti di ciclo

<a id="box-2-defLoopInvariant"></a>

!!! definizione "Definizione 13.2: invariante di ciclo"

    Un <strong>invariante di ciclo</strong> è una proprietà delle variabili di un algoritmo che è vera ogni volta che viene valutata la condizione di un ciclo, cioè prima della prima iterazione del ciclo e dopo ogni iterazione del ciclo.

- Per dimostrare la correttezza di un algoritmo per mezzo di un invariante di ciclo dobbiamo mostrare tre cose:

    1. <strong>Inizializzazione</strong>: l'invariante di ciclo è vero prima della prima iterazione del ciclo.

    2. <strong>Conservazione</strong>: se l'invariante di ciclo è vero prima di un'iterazione del ciclo, allora rimane vero alla fine dell'iterazione, o equivalentemente, è vero prima dell'iterazione successiva.

    3. <strong>Terminazione</strong>: il ciclo termina dopo un numero finito di iterazioni. Quando il ciclo termina, l'invariante di ciclo, insieme al fatto che la condizione del ciclo è falsa, fornisce una proprietà utile che mostra che l'algoritmo è corretto.

- Notiamo la somiglianza con l'<strong>induzione matematica</strong>, dove per dimostrare che una proprietà vale è necessario dimostrare un caso base e un passo induttivo:

    - mostrare che l'invariante vale prima della prima iterazione corrisponde al <strong>caso base</strong>;

    - mostrare che l'invariante vale da un'iterazione alla successiva corrisponde al <strong>passo induttivo</strong>.

    !!! chiave ""

        La proprietà di terminazione differisce dal consueto uso dell'induzione matematica, in cui il passo induttivo viene applicato infinite volte: qui l'“induzione” si ferma quando il ciclo termina.

- Per dimostrare che un ciclo termina, di solito si individua un numero naturale (per esempio $n-i+1$ o la lunghezza di un sotto-array) che diminuisce strettamente a ogni iterazione e che deve essere positivo perché il ciclo continui. Poiché un numero naturale non può diminuire all'infinito, il ciclo termina.

!!! chiave ""

    <strong>Schema di una dimostrazione di correttezza con un invariante di ciclo</strong>

    1. Enunciare l'invariante: una proprietà delle variabili, vera ogni volta che viene valutata la condizione del ciclo.

    2. <strong>Inizializzazione</strong>: verificarlo con i valori assegnati prima del ciclo.

    3. <strong>Conservazione</strong>: assumerlo insieme alla condizione del ciclo, eseguire il corpo una volta, e verificarlo con i nuovi valori.

    4. <strong>Terminazione</strong>: trovare un numero naturale che diminuisce strettamente a ogni iterazione; poi combinare l'invariante con la negazione della condizione del ciclo per ottenere l'output corretto.

## 13.2 Correttezza di Find Maximum

!!! chiave ""

    Dato un array $a[1..n]$ di $n$ numeri interi, con $n \ge 1$, consideriamo il problema di determinare il valore massimo dell'array.

- Il primo esempio è il ciclo più semplice: una singola scansione dell'array. Questo è lo pseudocodice dell'algoritmo <code>FindMaximum</code>.

!!! algoritmo "Algoritmo: FindMaximum"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri interi</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore massimo dell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMaximum(a, n)</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max := a&#91;1&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-fm-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(max&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python del capitolo">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ del capitolo">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java del capitolo">Java</a></div>

- L'<strong>invariante di ciclo</strong> del ciclo while di <code>FindMaximum</code> è:

!!! chiave ""

    Ogni volta che viene valutata la condizione alla riga [4](#riga-13-correttezza-line-fm-c), la variabile $max$ è uguale al valore massimo del sotto-array $a[1..i-1]$:

    $$
    max=\max\{a[1],a[2],\dots,a[i-1]\}.
    $$

<a id="box-3-exInvariantFindMax"></a>

!!! esempio "Esempio 13.1: Invariante di ciclo di FindMaximum"

    Consideriamo l'array $a=[9, 12, 3, 16, 19, 11, 12]$ con $n=7$. La tabella mostra i valori di $i$ e $max$ ogni volta che viene valutata la condizione alla riga [4](#riga-13-correttezza-line-fm-c):

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(max&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;1..i-1&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(&#92;max&#92;{a&#91;1&#93;,&#92;dots,a&#91;i-1&#93;&#92;}&#92;)</span></th>
    </tr>
    <tr>
    <td>2</td>
    <td>9</td>
    <td><span class="arithmatex">&#92;(&#91;9&#93;&#92;)</span></td>
    <td>9</td>
    </tr>
    <tr>
    <td>3</td>
    <td>12</td>
    <td><span class="arithmatex">&#92;(&#91;9,12&#93;&#92;)</span></td>
    <td>12</td>
    </tr>
    <tr>
    <td>4</td>
    <td>12</td>
    <td><span class="arithmatex">&#92;(&#91;9,12,3&#93;&#92;)</span></td>
    <td>12</td>
    </tr>
    <tr>
    <td>5</td>
    <td>16</td>
    <td><span class="arithmatex">&#92;(&#91;9,12,3,16&#93;&#92;)</span></td>
    <td>16</td>
    </tr>
    <tr>
    <td>6</td>
    <td>19</td>
    <td><span class="arithmatex">&#92;(&#91;9,12,3,16,19&#93;&#92;)</span></td>
    <td>19</td>
    </tr>
    <tr>
    <td>7</td>
    <td>19</td>
    <td><span class="arithmatex">&#92;(&#91;9,12,3,16,19,11&#93;&#92;)</span></td>
    <td>19</td>
    </tr>
    <tr>
    <td>8</td>
    <td>19</td>
    <td><span class="arithmatex">&#92;(&#91;9,12,3,16,19,11,12&#93;&#92;)</span></td>
    <td>19   (il ciclo termina)</td>
    </tr>
    </table></div>

    A ogni valutazione l'invariante vale. Quando il ciclo termina $i=n+1=8$, e l'algoritmo restituisce $19$, il massimo dell'intero array.

- Usando l'invariante di ciclo possiamo dimostrare la correttezza dell'algoritmo <code>FindMaximum</code>, enunciata dalla seguente osservazione.

<a id="box-4-obsCorrectFindMax"></a>

!!! teorema "Osservazione 13.3"

    Dato un array $a[1..n]$ di $n \ge 1$ numeri interi, l'algoritmo <code>FindMaximum</code> termina e restituisce

    $$
    \max\{a[1],a[2],\dots,a[n]\}.
    $$

??? dimostrazione "Dimostrazione"

    Dimostriamo le tre proprietà dell'invariante di ciclo.

    - <strong>Inizializzazione.</strong> Prima della prima iterazione, le righe [2](#riga-13-correttezza-line-fm-a) e [3](#riga-13-correttezza-line-fm-b) pongono $max=a[1]$ e $i=2$. Il sotto-array $a[1..i-1]=a[1..1]$ è costituito dal solo elemento $a[1]$, il cui massimo è $a[1]=max$. Quindi l'invariante vale.

    - <strong>Conservazione.</strong> Supponiamo che, prima di un'iterazione, $max=\max\{a[1],\dots,a[i-1]\}$. Il corpo del ciclo confronta $a[i]$ con $max$ (riga [5](#riga-13-correttezza-line-fm-d)):

        - se $a[i]>max$, allora la riga [6](#riga-13-correttezza-line-fm-e) pone $max \leftarrow a[i]$, e $a[i]$ è maggiore di tutti gli elementi di $a[1..i-1]$;

        - se $a[i]\le max$, allora $max$ non cambia ed è maggiore o uguale a $a[i]$.

        In entrambi i casi, alla fine del corpo

        $$
        max=\max\{a[1],\dots,a[i-1],a[i]\}.
        $$

        La riga [8](#riga-13-correttezza-line-fm-f) incrementa $i$ di $1$, quindi, con il nuovo valore di $i$, si ha di nuovo $max=\max\{a[1],\dots,a[i-1]\}$. Quindi l'invariante vale prima dell'iterazione successiva.

    - <strong>Terminazione.</strong> La variabile $i$ parte da $2\le n+1$ e aumenta di $1$ a ogni iterazione, quindi il ciclo termina dopo esattamente $n-1$ iterazioni, quando per la prima volta $i=n+1$. Sostituendo $i=n+1$ nell'invariante di ciclo otteniamo

        $$
        max=\max\{a[1],a[2],\dots,a[n]\},
        $$

        che è il valore restituito alla riga [10](#riga-13-correttezza-line-fm-g). Quindi l'algoritmo è corretto.

    <p class="qed-riga"><span class="qed">□</span></p>

## 13.3 Correttezza di Insertion Sort

!!! chiave ""

    Dato un array $a[1..n]$ di $n$ numeri naturali, con $n\ge 1$, consideriamo il problema di riordinare gli elementi dell'array in modo non decrescente:

    $$
    a[1] \le a[2] \le \cdots \le a[n].
    $$

- Con due cicli annidati la dimostrazione richiede due invarianti, uno per ciascun ciclo. Questo è lo pseudocodice dell'algoritmo <code>InsertionSort</code>.

!!! algoritmo "Algoritmo: InsertionSort"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array <span class="arithmatex">&#92;(a&#92;)</span> ordinato in modo non decrescente</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> InsertionSort(a, n)</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(key := a&#91;i&#93;&#92;)</span></span><span class="pc-c">// Elemento da inserire</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := i - 1&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;ge 1&#92;)</span> <strong>and</strong> <span class="arithmatex">&#92;(a&#91;j&#93; &gt; key&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;j+1&#93;&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(a&#91;j&#93;&#92;)</span></span><span class="pc-c">// Sposta l'elemento a destra</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(j - 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;j+1&#93;&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(key&#92;)</span></span><span class="pc-c">// Inserisce key nella posizione corretta</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-is-i"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python del capitolo">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ del capitolo">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java del capitolo">Java</a></div>

- La condizione alla riga [6](#riga-13-correttezza-line-is-e) è valutata da sinistra a destra, e la seconda parte è valutata solo se la prima è vera: quando $j=0$ la condizione è falsa e l'elemento inesistente $a[0]$ non viene mai acceduto.

- L'algoritmo contiene due cicli annidati. Dimostriamo prima che cosa fa una singola esecuzione del ciclo while <strong>interno</strong> (righe [6](#riga-13-correttezza-line-is-e)–[8](#riga-13-correttezza-line-is-g)), e poi usiamo questo risultato per dimostrare la correttezza del ciclo while <strong>esterno</strong> (righe [3](#riga-13-correttezza-line-is-b)–[11](#riga-13-correttezza-line-is-i)).

### 13.3.1 Il ciclo interno

- Consideriamo un'iterazione del ciclo esterno, con un dato valore di $i \in \{2,3,\dots,n\}$. Indichiamo con

    $$
    b[1..i]
    $$

    il contenuto del sotto-array $a[1..i]$ all'inizio di questa iterazione (cioè quando la condizione alla riga [3](#riga-13-correttezza-line-is-b) è vera), e supponiamo che $b[1..i-1]$ sia ordinato in modo non decrescente. Dopo la riga [4](#riga-13-correttezza-line-is-c) si ha $key=b[i]$.

- L'<strong>invariante di ciclo</strong> del ciclo while interno è:

!!! chiave ""

    Ogni volta che viene valutata la condizione alla riga [6](#riga-13-correttezza-line-is-e):

    - **(I1)** $a[1..j]=b[1..j]$ (i primi $j$ elementi non sono stati spostati);

    - **(I2)** $a[j+2..i]=b[j+1..i-1]$ (gli elementi $b[j+1],\dots,b[i-1]$ sono stati spostati di una posizione a destra);

    - **(I3)** ogni elemento di $a[j+2..i]$ è strettamente maggiore di $key$.

    Le componenti $a[i+1..n]$ non vengono mai modificate dal ciclo interno.

- La posizione $j+1$ è il “buco” in cui verrà inserito $key$: il suo contenuto attuale è una copia che verrà sovrascritta. Un sotto-array $a[l..r]$ con $l>r$ è <strong>vuoto</strong>, e qualunque proprietà di tutti i suoi elementi è banalmente vera.

<a id="box-5-exInvariantInsInner"></a>

!!! esempio "Esempio 13.2: Invariante di ciclo del ciclo interno"

    Consideriamo l'array $a=[5,2,4,1,3]$ all'inizio dell'iterazione $i=5$ del ciclo esterno: $b[1..5]=[1,2,4,5,3]$ e $key=3$. La tabella mostra l'array ogni volta che viene valutata la condizione alla riga [6](#riga-13-correttezza-line-is-e).

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(j&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;1..j&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;j+2..5&#93;&#92;)</span></th>
    <th>condizione</th>
    </tr>
    <tr>
    <td>4</td>
    <td>1</td>
    <td>2</td>
    <td>4</td>
    <td>5</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;1,2,4,5&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;&#92; &#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;3&#92;)</span>: vera</td>
    </tr>
    <tr>
    <td>3</td>
    <td>1</td>
    <td>2</td>
    <td>4</td>
    <td>5</td>
    <td class="cella-blu">5</td>
    <td><span class="arithmatex">&#92;(&#91;1,2,4&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;5&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;3&#92;)</span>: vera</td>
    </tr>
    <tr>
    <td>2</td>
    <td>1</td>
    <td>2</td>
    <td>4</td>
    <td class="cella-blu">4</td>
    <td>5</td>
    <td><span class="arithmatex">&#92;(&#91;1,2&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;4,5&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le 3&#92;)</span>: falsa</td>
    </tr>
    </table></div>

    A ogni valutazione $a[1..j]=b[1..j]$, $a[j+2..5]=b[j+1..4]$ e tutti gli elementi di $a[j+2..5]$ sono maggiori di $3$. Quando il ciclo termina $j=2$, e la riga [10](#riga-13-correttezza-line-is-h) pone $a[3]\leftarrow 3$, ottenendo $a[1..5]=[1,2,3,4,5]$.

<a id="box-6-lemInsertionSortInner"></a>

!!! teorema "Lemma 13.4: ciclo interno di Insertion Sort"

    Consideriamo un'iterazione del ciclo esterno di <code>InsertionSort</code> con $i\in\{2,\dots,n\}$, e sia $b[1..i]$ il contenuto di $a[1..i]$ all'inizio dell'iterazione. Se $b[1..i-1]$ è ordinato in modo non decrescente, allora il ciclo while interno termina e, dopo la riga [10](#riga-13-correttezza-line-is-h), il sotto-array $a[1..i]$ contiene gli elementi $b[1],\dots,b[i]$ ordinati in modo non decrescente, mentre $a[i+1..n]$ è invariato.

??? dimostrazione "Dimostrazione"

    Dimostriamo le tre proprietà dell'invariante di ciclo (I1)–(I3).

    - <strong>Inizializzazione.</strong> Prima della prima valutazione della condizione, $j=i-1$ e nulla è stato modificato. Quindi $a[1..i-1]=b[1..i-1]$, cioè (I1) vale. I sotto-array $a[j+2..i]=a[i+1..i]$ e $b[j+1..i-1]=b[i..i-1]$ sono entrambi vuoti, quindi (I2) e (I3) valgono banalmente.

    - <strong>Conservazione.</strong> Supponiamo che (I1)–(I3) valgano e che la condizione alla riga [6](#riga-13-correttezza-line-is-e) sia vera, cioè $j\ge 1$ e $a[j]>key$. Per (I1), $a[j]=b[j]$, quindi $b[j]>key$. La riga [7](#riga-13-correttezza-line-is-f) pone $a[j+1]\leftarrow a[j]=b[j]$; quindi, per (I2),

        $$
        a[j+1..i]=b[j..i-1],
        $$

        e tutti questi elementi sono maggiori di $key$ (per (I3) e $b[j]>key$). Le posizioni $1,\dots,j$ non vengono modificate. La riga [8](#riga-13-correttezza-line-is-g) pone $j\leftarrow j-1$. Indicando con $j'=j-1$ il nuovo valore, si ha $a[1..j']=b[1..j']$, $a[j'+2..i]=a[j+1..i]=b[j..i-1]=b[j'+1..i-1]$, e tutti gli elementi di $a[j'+2..i]$ sono maggiori di $key$. Quindi (I1)–(I3) valgono prima della valutazione successiva della condizione.

    - <strong>Terminazione.</strong> La variabile $j$ parte da $i-1$ e diminuisce di $1$ a ogni iterazione; poiché il ciclo si ferma al più tardi quando $j=0$, il ciclo interno esegue al più $i-1$ iterazioni e termina. Quando termina, si ha $j=0$ oppure $a[j]=b[j]\le key$. Per (I1)–(I3):

        - $a[1..j]=b[1..j]$ è ordinato e, se $j\ge 1$, il suo elemento più grande $b[j]$ è $\le key$;

        - $a[j+2..i]=b[j+1..i-1]$ è ordinato e tutti i suoi elementi sono $>key$.

        La riga [10](#riga-13-correttezza-line-is-h) pone $a[j+1]\leftarrow key=b[i]$. Quindi

        $$
        a[1..i]=\big[\,b[1],\dots,b[j],\ key,\ b[j+1],\dots,b[i-1]\,\big],
        $$

        che contiene esattamente gli elementi $b[1],\dots,b[i]$ ed è ordinato in modo non decrescente, perché $b[1..j]$ è ordinato, $b[j]\le key< b[j+1]$, e $b[j+1..i-1]$ è ordinato. Le posizioni $i+1,\dots,n$ non vengono mai accedute.

    <p class="qed-riga"><span class="qed">□</span></p>

### 13.3.2 Il ciclo esterno

- L'<strong>invariante di ciclo</strong> del ciclo while esterno è:

!!! chiave ""

    Ogni volta che viene valutata la condizione alla riga [3](#riga-13-correttezza-line-is-b), il sotto-array $a[1..i-1]$ è costituito dagli elementi originariamente in $a[1..i-1]$, ma ordinati in modo non decrescente, e il sotto-array $a[i..n]$ è uguale al sotto-array originale $a[i..n]$.

<a id="box-7-exInvariantInsOuter"></a>

!!! esempio "Esempio 13.3: Invariante di ciclo del ciclo esterno"

    Consideriamo l'array $a=[5,2,4,1,3]$ con $n=5$. La tabella mostra l'array ogni volta che viene valutata la condizione alla riga [3](#riga-13-correttezza-line-is-b); il sotto-array ordinato $a[1..i-1]$ è evidenziato in <mark style="background:color-mix(in srgb, #1971c2 30%, transparent);color:inherit">blu</mark>.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;1..i-1&#93;&#92;)</span> originale</th>
    </tr>
    <tr>
    <td>2</td>
    <td class="cella-blu">5</td>
    <td>2</td>
    <td>4</td>
    <td>1</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;5&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td>3</td>
    <td class="cella-blu">2</td>
    <td class="cella-blu">5</td>
    <td>4</td>
    <td>1</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;5,2&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td>4</td>
    <td class="cella-blu">2</td>
    <td class="cella-blu">4</td>
    <td class="cella-blu">5</td>
    <td>1</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;5,2,4&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td>5</td>
    <td class="cella-blu">1</td>
    <td class="cella-blu">2</td>
    <td class="cella-blu">4</td>
    <td class="cella-blu">5</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;5,2,4,1&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td>6</td>
    <td class="cella-blu">1</td>
    <td class="cella-blu">2</td>
    <td class="cella-blu">3</td>
    <td class="cella-blu">4</td>
    <td class="cella-blu">5</td>
    <td><span class="arithmatex">&#92;(&#91;5,2,4,1,3&#93;&#92;)</span>   (il ciclo termina)</td>
    </tr>
    </table></div>

- Usando l'invariante di ciclo e il [Lemma 13.4](#box-6-lemInsertionSortInner) possiamo dimostrare la correttezza dell'algoritmo <code>InsertionSort</code>.

<a id="box-8-obsCorrectInsertionSort"></a>

!!! teorema "Osservazione 13.5"

    Dato un array $a[1..n]$ di $n\ge 1$ numeri naturali, l'algoritmo <code>InsertionSort</code> termina e, alla fine, l'array $a[1..n]$ contiene gli elementi originali riordinati in modo non decrescente:

    $$
    a[1]\le a[2]\le\cdots\le a[n].
    $$

??? dimostrazione "Dimostrazione"

    Dimostriamo le tre proprietà dell'invariante di ciclo del ciclo esterno.

    - <strong>Inizializzazione.</strong> Prima della prima iterazione, $i=2$ (riga [2](#riga-13-correttezza-line-is-a)) e l'array non è stato modificato. Il sotto-array $a[1..i-1]=a[1..1]$ è costituito dal singolo elemento originale $a[1]$, ed è banalmente ordinato. Il sotto-array $a[2..n]$ è quello originale. Quindi l'invariante vale.

    - <strong>Conservazione.</strong> Supponiamo che l'invariante valga e che $i\le n$. Allora $a[1..i-1]$ contiene gli elementi originali di $a[1..i-1]$ ordinati, e $a[i]$ è l'elemento originale $a[i]$. Per il [Lemma 13.4](#box-6-lemInsertionSortInner), dopo la riga [10](#riga-13-correttezza-line-is-h) il sotto-array $a[1..i]$ contiene questi $i$ elementi, cioè gli elementi originali di $a[1..i]$, ordinati in modo non decrescente, e $a[i+1..n]$ è invariato, quindi ancora uguale a quello originale. La riga [11](#riga-13-correttezza-line-is-i) pone $i\leftarrow i+1$, quindi l'invariante vale con il nuovo valore di $i$.

    - <strong>Terminazione.</strong> La variabile $i$ parte da $2\le n+1$ e aumenta di $1$ a ogni iterazione, e ogni ciclo interno termina ([Lemma 13.4](#box-6-lemInsertionSortInner)). Quindi il ciclo esterno termina dopo esattamente $n-1$ iterazioni, quando per la prima volta $i=n+1$. Sostituendo $i=n+1$ nell'invariante di ciclo, il sotto-array $a[1..n]$, cioè l'intero array, è costituito dagli elementi originali ordinati in modo non decrescente. Quindi l'algoritmo è corretto.

    <p class="qed-riga"><span class="qed">□</span></p>

## 13.4 Correttezza di Binary Search

!!! chiave ""

    Dati un array $a[1..n]$ di $n$ numeri naturali ordinato in modo non decrescente e un numero naturale $m$ da cercare, consideriamo il problema di determinare se $m$ è uno degli elementi dell'array.

- Nei due algoritmi precedenti il ciclo viene sempre eseguito finché la sua condizione diventa falsa. La ricerca binaria può invece fermarsi in anticipo, con un <strong>return</strong> dentro il ciclo, e la dimostrazione deve tenere conto di entrambe le uscite. Questo è lo pseudocodice dell'algoritmo <code>BinarySearch</code> (iterativo).

!!! algoritmo "Algoritmo: BinarySearch"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali ordinato in modo non decrescente e un valore <span class="arithmatex">&#92;(m&#92;)</span> da cercare</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Indice di <span class="arithmatex">&#92;(m&#92;)</span> in <span class="arithmatex">&#92;(a&#92;)</span>, oppure <span class="arithmatex">&#92;(-1&#92;)</span> se non trovato</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> BinarySearch(a, n, m)</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(left&#92;)</span> := <span class="arithmatex">&#92;(1&#92;)</span></span><span class="pc-c">// Estremo sinistro</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(right&#92;)</span> := <span class="arithmatex">&#92;(n&#92;)</span></span><span class="pc-c">// Estremo destro</span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(left &#92;le right&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(mid&#92;)</span> := <span class="arithmatex">&#92;(left + &#92;lfloor (right - left) / 2 &#92;rfloor&#92;)</span></span><span class="pc-c">// Indice centrale</span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(mid&#92;)</span></span><span class="pc-c">// Elemento trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-g"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(left&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(mid + 1&#92;)</span></span><span class="pc-c">// Cerca nella metà destra</span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-i"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(right&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(mid - 1&#92;)</span></span><span class="pc-c">// Cerca nella metà sinistra</span></span></div>
    <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-bs-j"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(-1&#92;)</span></span><span class="pc-c">// Elemento non trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python del capitolo">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ del capitolo">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java del capitolo">Java</a></div>

- L'<strong>invariante di ciclo</strong> del ciclo while di <code>BinarySearch</code> è:

!!! chiave ""

    Ogni volta che viene valutata la condizione alla riga [4](#riga-13-correttezza-line-bs-c):

    - **(I1)** $1\le left$ e $right\le n$;

    - **(I2)** se $m$ è in $a$, allora $m$ è in $a[left..right]$, cioè

        $$
        m\in\{a[1],\dots,a[n]\}
        \ \Longrightarrow\
        m\in\{a[left],\dots,a[right]\}.
        $$

- A parole: l'algoritmo non scarta mai una porzione dell'array che può contenere $m$. Il sotto-array $a[left..right]$ è detto <strong>intervallo di ricerca</strong> e contiene $right-left+1$ elementi (è vuoto se $left>right$).

<a id="box-9-exInvariantBinSearch"></a>

!!! esempio "Esempio 13.4: Invariante di ciclo di BinarySearch"

    Ricerca di $m=10$ in $a=[3, 9, 11, 12, 12, 16, 19]$ ($n=7$). La tabella mostra l'intervallo di ricerca ogni volta che viene valutata la condizione alla riga [4](#riga-13-correttezza-line-bs-c).

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(left&#92;)</span></th>
    <th><span class="arithmatex">&#92;(right&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;left..right&#93;&#92;)</span></th>
    <th>azione</th>
    </tr>
    <tr>
    <td>1</td>
    <td>7</td>
    <td><span class="arithmatex">&#92;(&#91;3,9,11,12,12,16,19&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(mid=4&#92;)</span>, <span class="arithmatex">&#92;(a&#91;4&#93;=12&gt;10&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right=3&#92;)</span></td>
    </tr>
    <tr>
    <td>1</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;3,9,11&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(mid=2&#92;)</span>, <span class="arithmatex">&#92;(a&#91;2&#93;=9&lt;10&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left=3&#92;)</span></td>
    </tr>
    <tr>
    <td>3</td>
    <td>3</td>
    <td><span class="arithmatex">&#92;(&#91;11&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(mid=3&#92;)</span>, <span class="arithmatex">&#92;(a&#91;3&#93;=11&gt;10&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right=2&#92;)</span></td>
    </tr>
    <tr>
    <td>3</td>
    <td>2</td>
    <td><span class="arithmatex">&#92;(&#91;&#92; &#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(left&gt;right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> restituisce <span class="arithmatex">&#92;(-1&#92;)</span></td>
    </tr>
    </table></div>

    Poiché $10$ non è in $a$, l'invariante (I2) è banalmente vero; quando l'intervallo diventa vuoto l'algoritmo restituisce correttamente $-1$.

<a id="box-10-obsCorrectBinarySearch"></a>

!!! teorema "Osservazione 13.6"

    Dati un array $a[1..n]$ di $n$ numeri naturali ordinato in modo non decrescente e un numero naturale $m$, l'algoritmo <code>BinarySearch</code> termina; restituisce un indice $k$ tale che $a[k]=m$ se $m$ è in $a$, e restituisce $-1$ altrimenti.

??? dimostrazione "Dimostrazione"

    Dimostriamo le tre proprietà dell'invariante di ciclo.

    - <strong>Inizializzazione.</strong> Le righe [2](#riga-13-correttezza-line-bs-a) e [3](#riga-13-correttezza-line-bs-b) pongono $left=1$ e $right=n$. Allora (I1) vale, e $a[left..right]=a[1..n]$ è l'intero array, quindi (I2) vale.

    - <strong>Conservazione.</strong> Supponiamo che (I1)–(I2) valgano e che $left\le right$. La riga [5](#riga-13-correttezza-line-bs-d) calcola $mid=left+\lfloor(right-left)/2\rfloor$; poiché $0\le \lfloor(right-left)/2\rfloor\le right-left$, si ha

        $$
        1\le left\le mid\le right\le n,
        $$

        quindi $a[mid]$ è una componente valida dell'array. Sono possibili tre casi.

        - $a[mid]=m$: l'algoritmo restituisce $mid$ alla riga [7](#riga-13-correttezza-line-bs-f), che è un output corretto.

        - $a[mid]<m$: poiché l'array è ordinato, per ogni $k\le mid$ si ha $a[k]\le a[mid]<m$. Quindi $m$ non è in $a[left..mid]$, e se $m$ è in $a[left..right]$ allora è in $a[mid+1..right]$. La riga [10](#riga-13-correttezza-line-bs-h) pone $left\leftarrow mid+1\ge 1$, quindi (I1) e (I2) valgono ancora.

        - $a[mid]>m$: poiché l'array è ordinato, per ogni $k\ge mid$ si ha $a[k]\ge a[mid]>m$. Quindi, se $m$ è in $a[left..right]$, allora è in $a[left..mid-1]$. La riga [13](#riga-13-correttezza-line-bs-i) pone $right\leftarrow mid-1\le n$, quindi (I1) e (I2) valgono ancora.

    - <strong>Terminazione.</strong> Consideriamo il numero di elementi dell'intervallo di ricerca, $right-left+1$. Nel secondo caso il nuovo numero è $right-mid\le right-left$, nel terzo caso è $mid-left\le right-left$: in entrambi i casi diminuisce di almeno $1$. Poiché il ciclo continua solo finché $right-left+1\ge 1$, il ciclo termina dopo al più $n$ iterazioni. L'algoritmo finisce in uno di due modi:

        - restituisce $mid$ con $a[mid]=m$, che è corretto;

        - la condizione $left\le right$ è falsa, cioè l'intervallo di ricerca $a[left..right]$ è vuoto. Poiché un sotto-array vuoto non contiene $m$, per (I2) $m$ non è in $a$, e l'algoritmo restituisce correttamente $-1$ alla riga [16](#riga-13-correttezza-line-bs-j).

        Quindi l'algoritmo è corretto.

    <p class="qed-riga"><span class="qed">□</span></p>

## 13.5 Correttezza dell'algoritmo di Euclide

!!! chiave ""

    Dati due numeri naturali $n, m \ge 1$, consideriamo il problema di calcolare il loro massimo comune divisore $\gcd(n,m)$.

- Nell'ultimo esempio l'invariante non è una proprietà di una porzione di un array, ma un'uguaglianza fra due numeri che non cambia mai. Questo è lo pseudocodice dell'algoritmo di Euclide.

!!! algoritmo "Algoritmo: EuclideanAlgorithm"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(n, m &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(&#92;gcd(n, m)&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> EuclideanAlgorithm(<span class="arithmatex">&#92;(n&#92;)</span>, <span class="arithmatex">&#92;(m&#92;)</span>)</span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-eu-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(m &#92;ne 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-eu-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r := n &#92;bmod m&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-eu-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow m&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-eu-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow r&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-13-correttezza-line-eu-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(n&#92;)</span></span><span class="pc-c">// <span class="arithmatex">&#92;(m = 0&#92;)</span>: <span class="arithmatex">&#92;(n&#92;)</span> è il MCD</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<div class="colab-pulsanti" markdown="0"><span class="colab-etichetta">Esegui in Colab:</span><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_python.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Python del capitolo">Python</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_cpp.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook C++ del capitolo">C++</a><a class="colab-pulsante" href="https://colab.research.google.com/github/fabiofurini/algoritmi/blob/main/notebooks/cap13_correttezza_java.ipynb" target="_blank" rel="noopener" title="Apri in Google Colab il notebook Java del capitolo">Java</a></div>

- La dimostrazione si basa sulla seguente proprietà del massimo comune divisore, dimostrata nel capitolo «Algoritmi numerici»:

    $$
    \gcd(n, m) = \gcd(m,\ n \bmod m)\qquad \text{per ogni } n\ge 1,\ m \ge 1.
    $$

- Usiamo anche la convenzione $\gcd(n,0)=n$ per $n\ge 1$: ogni numero naturale divide $0$, quindi i divisori comuni di $n$ e $0$ sono i divisori di $n$, e il più grande di essi è $n$.

- Indichiamo con $n_0$ e $m_0$ i valori di $n$ e $m$ dati in input. L'<strong>invariante di ciclo</strong> del ciclo while è:

!!! chiave ""

    Ogni volta che viene valutata la condizione alla riga [2](#riga-13-correttezza-line-eu-a), $n\ge 1$, $m\ge 0$, e

    $$
    \gcd(n,m)=\gcd(n_0,m_0).
    $$

<a id="box-11-exInvariantEuclid"></a>

!!! esempio "Esempio 13.5: Invariante di ciclo dell'algoritmo di Euclide"

    Consideriamo $n_0=252$ e $m_0=105$. La tabella mostra i valori di $n$ e $m$ ogni volta che viene valutata la condizione alla riga [2](#riga-13-correttezza-line-eu-a):

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(n&#92;)</span></th>
    <th><span class="arithmatex">&#92;(m&#92;)</span></th>
    <th><span class="arithmatex">&#92;(&#92;gcd(n,m)&#92;)</span></th>
    </tr>
    <tr>
    <td>252</td>
    <td>105</td>
    <td>21</td>
    </tr>
    <tr>
    <td>105</td>
    <td>42</td>
    <td>21</td>
    </tr>
    <tr>
    <td>42</td>
    <td>21</td>
    <td>21</td>
    </tr>
    <tr>
    <td>21</td>
    <td>0</td>
    <td>21   (il ciclo termina)</td>
    </tr>
    </table></div>

    Il valore $\gcd(n,m)=21$ non cambia mai, e quando $m=0$ l'algoritmo restituisce $n=21=\gcd(252,105)$.

<a id="box-12-obsCorrectEuclid"></a>

!!! teorema "Osservazione 13.7"

    Dati due numeri naturali $n_0,m_0\ge 1$, l'algoritmo <code>EuclideanAlgorithm</code> termina e restituisce $\gcd(n_0,m_0)$.

??? dimostrazione "Dimostrazione"

    Dimostriamo le tre proprietà dell'invariante di ciclo.

    - <strong>Inizializzazione.</strong> Prima della prima iterazione $n=n_0\ge 1$ e $m=m_0\ge 1$, quindi banalmente $\gcd(n,m)=\gcd(n_0,m_0)$.

    - <strong>Conservazione.</strong> Supponiamo che l'invariante valga e che $m\ne 0$, cioè $m\ge 1$. La riga [3](#riga-13-correttezza-line-eu-b) calcola $r=n\bmod m$, con $0\le r<m$. Le righe [4](#riga-13-correttezza-line-eu-c)–[5](#riga-13-correttezza-line-eu-d) sostituiscono la coppia $(n,m)$ con $(m,r)$. Il nuovo valore di $n$ è $m\ge 1$, il nuovo valore di $m$ è $r\ge 0$, e, poiché $n,m\ge 1$,

        $$
        \gcd(m,r)=\gcd(m,\ n\bmod m)=\gcd(n,m)=\gcd(n_0,m_0).
        $$

        Quindi l'invariante vale prima dell'iterazione successiva.

    - <strong>Terminazione.</strong> A ogni iterazione il valore di $m$ viene sostituito da $r<m$, quindi $m$ è un numero naturale che diminuisce strettamente. Quindi il ciclo termina dopo al più $m_0$ iterazioni, quando $m=0$. Sostituendo $m=0$ nell'invariante di ciclo otteniamo

        $$
        \gcd(n_0,m_0)=\gcd(n,0)=n,
        $$

        che è il valore restituito alla riga [7](#riga-13-correttezza-line-eu-e). Quindi l'algoritmo è corretto.

    <p class="qed-riga"><span class="qed">□</span></p>

- La dimostrazione non usa l'ipotesi $n_0\ge m_0$: se $n_0<m_0$, allora $n_0\bmod m_0=n_0$ e la prima iterazione si limita a scambiare i due numeri.

- Il limite “al più $m_0$ iterazioni” basta a dimostrare la terminazione, ma è molto pessimistico: il numero di iterazioni è in realtà $O(\log_2 m_0)$ (nell'esempio, $3$ iterazioni per $m_0=105$).

## 13.6 Correttezza degli algoritmi ricorsivi

- Gli invarianti di ciclo sono lo strumento per dimostrare la correttezza degli algoritmi <strong>iterativi</strong>, cioè basati su cicli.

- Un algoritmo <strong>ricorsivo</strong> risolve un'istanza di un problema chiamando se stesso su una o più istanze più piccole. La sua correttezza si dimostra direttamente per <strong>induzione matematica</strong> sulla dimensione dell'istanza:

    - <strong>caso base</strong>: l'algoritmo restituisce l'output corretto sulle istanze più piccole, che sono risolte senza chiamate ricorsive;

    - <strong>passo induttivo</strong>: sotto l'ipotesi induttiva che le chiamate ricorsive restituiscano l'output corretto sulle istanze più piccole, l'algoritmo ne combina i risultati nell'output corretto per l'istanza corrente.

- La terminazione segue dal fatto che ogni chiamata ricorsiva è fatta su un'istanza strettamente più piccola, quindi prima o poi si raggiunge il caso base.

!!! chiave ""

    La correttezza degli algoritmi ricorsivi si dimostra per induzione sulla dimensione dell'input. Questa tecnica viene applicata insieme allo studio degli algoritmi ricorsivi.

!!! chiave ""

    <strong>Punti chiave del capitolo</strong>

    - Un algoritmo è corretto se, per ogni istanza di input, termina e restituisce l'output corretto; i test possono solo mostrare che un algoritmo è sbagliato.

    - La correttezza di un ciclo si dimostra con un invariante di ciclo: inizializzazione, conservazione e terminazione.

    - L'invariante, insieme alla negazione della condizione del ciclo, fornisce l'output: $i=n+1$ per Find Maximum e Insertion Sort, un intervallo di ricerca vuoto per Binary Search, $m=0$ per l'algoritmo di Euclide.

    - I cicli annidati richiedono un invariante per ciascun ciclo (Insertion Sort); un <strong>return</strong> dentro il ciclo è una seconda uscita che va dimostrata corretta (Binary Search).

    - Gli algoritmi ricorsivi si dimostrano corretti per induzione sulla dimensione dell'input.

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

## Laboratorio interattivo { #laboratorio-interattivo }

L'algoritmo del capitolo, un passo alla volta: muovi i cursori e premi ▶.
Lo stesso grafico a tutta pagina, con gli altri del corso, è nel [laboratorio interattivo](../laboratorio/invariante.md).

<div class="gi" data-grafico="invariante"></div>
