---
title: "Esercizi · Algoritmi di ordinamento"
---

# Esercizi · Algoritmi di ordinamento

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 3** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 3](../algoritmi-di-base/03-ordinamento.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-algoritmi-di-base.pdf)

</div>

Gli esercizi di questo capitolo usano i tre algoritmi del capitolo «Algoritmi di ordinamento» (Insertion Sort, Exchange Sort e Selection Sort) nella loro versione in pseudocodice, con array indicizzati a partire da $1$. In tutte le soluzioni valgono le seguenti convenzioni.

!!! nota ""

    - In una tabella di traccia, ogni riga mostra lo stato dell'array <em>dopo</em> l'operazione descritta nell'ultima colonna. La chiave corrente di Insertion Sort è evidenziata in <mark style="background:color-mix(in srgb, #e03131 30%, transparent);color:inherit">rosso</mark>; le celle modificate da uno spostamento, da un inserimento o da uno scambio sono evidenziate in <mark style="background:color-mix(in srgb, #1971c2 30%, transparent);color:inherit">blu</mark>.

    - Un <strong>confronto tra chiavi</strong> è la valutazione di un confronto tra due chiavi: $a[j] > \mathit{key}$ in Insertion Sort (valutato solo quando $j \ge 1$), $a[i] > a[j]$ in Exchange Sort, $a[j] < a[\mathit{minIdx}]$ in Selection Sort.

    - Un <strong>passo</strong> è l'esecuzione di una riga dello pseudocodice; la valutazione della condizione di un ciclo <strong>while</strong> conta come un passo ogni volta che viene valutata, compresa l'ultima, quella che termina il ciclo.

    - Per ogni $n \in \Z_{\ge 1}$:

        $$
        \sum_{k=1}^{n-1} k = 1 + 2 + \dots + (n-1) = \frac{n(n-1)}{2}.
        $$

<a id="esercizio-3-1"></a>

!!! esercizio "Esercizio 3.1: Algoritmi di ordinamento (E1)"

    Consideriamo gli array

    $$
    a=[3,1,2] \qquad \text{e} \qquad b=[2,1,2]
    $$

    e i riarrangiamenti di un array, come nella definizione del problema dell'ordinamento.

    **Domande**

    1. Elencare tutti i riarrangiamenti di $a$ e di $b$. Quali di essi sono ordinati in ordine non decrescente?

    2. Spiegare perché l'output del problema dell'ordinamento non è un array qualunque ordinato in ordine non decrescente: fornire un esempio di array ordinato in ordine non decrescente che non è un output corretto per $a$.

    3. Quanti riarrangiamenti ha un array di $n$ elementi distinti? Calcolare il numero per $n=5$, $n=10$ e $n=20$.

    4. Consideriamo l'algoritmo <code>BruteForceSort</code> che genera uno a uno i riarrangiamenti dell'array e si ferma quando ne trova uno ordinato. Quanti riarrangiamenti può esaminare nel caso peggiore per un array di $n$ elementi distinti? Confrontare con i $\frac{n(n-1)}{2}$ spostamenti eseguiti nel caso peggiore da Insertion Sort.

??? soluzione "Soluzione"

    1. L'array $a=[3,1,2]$ ha $3!=6$ riarrangiamenti:

        $$
        [1,2,3],\ [1,3,2],\ [2,1,3],\ [2,3,1],\ [3,1,2],\ [3,2,1].
        $$

        Solo $[1,2,3]$ è ordinato in ordine non decrescente.

        L'array $b=[2,1,2]$ contiene due volte il valore $2$, quindi scambiare i due $2$ dà lo stesso array. I suoi riarrangiamenti distinti sono soltanto $3$:

        $$
        [1,2,2],\ [2,1,2],\ [2,2,1],
        $$

        e solo $[1,2,2]$ è ordinato. In entrambi i casi il riarrangiamento ordinato è <strong>unico</strong>: l'output del problema dell'ordinamento è univocamente determinato dall'input.

    2. L'output deve essere un <strong>riarrangiamento dell'input</strong> ordinato. Ad esempio, gli array $[1,1,1]$ e $[1,2,4]$ sono ordinati, ma non sono un output corretto per $a=[3,1,2]$, perché non contengono gli stessi elementi. Un “algoritmo” che sovrascrive tutte le componenti con $0$ produce un array ordinato, ma non risolve il problema dell'ordinamento. Per questo, quando si dimostra che un algoritmo di ordinamento è corretto, bisogna mostrare anche che l'array finale contiene gli elementi originali.

    3. Un array di $n$ elementi distinti ha

        $$
        n!=n\cdot(n-1)\cdots 2\cdot 1
        $$

        riarrangiamenti: ci sono $n$ scelte per la prima posizione, $n-1$ per la seconda, e così via. Quindi

        $$
        5!=120,\qquad 10!=3\,628\,800,\qquad 20!=2\,432\,902\,008\,176\,640\,000\approx 2.4\cdot 10^{18}.
        $$

    4. Nel caso peggiore il riarrangiamento ordinato è l'ultimo generato, quindi <code>BruteForceSort</code> può esaminare tutti gli $n!$ riarrangiamenti (e verificare ciascuno di essi richiede fino a $n-1$ confronti). Insertion Sort esegue al più $\frac{n(n-1)}{2}$ spostamenti:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n!&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;frac{n(n-1)}{2}&#92;)</span></th>
        </tr>
        <tr>
        <td>5</td>
        <td>120</td>
        <td>10</td>
        </tr>
        <tr>
        <td>10</td>
        <td>3 628 800</td>
        <td>45</td>
        </tr>
        <tr>
        <td>20</td>
        <td>2 432 902 008 176 640 000</td>
        <td>190</td>
        </tr>
        </table></div>

        Poiché $n!\ge 2^{n-1}$ per ogni $n\ge 1$, il numero di riarrangiamenti esaminati dall'approccio a forza bruta cresce almeno in modo esponenziale con $n$, mentre il numero di spostamenti di Insertion Sort cresce solo in modo quadratico. Già per $n=20$, anche esaminando $10^9$ riarrangiamenti al secondo, <code>BruteForceSort</code> potrebbe impiegare

        $$
        \frac{2.43\cdot 10^{18}}{10^{9}} \text{ s} \approx 2.43\cdot 10^{9} \text{ s} \approx 77 \text{ anni}.
        $$

<a id="esercizio-3-2"></a>

!!! esercizio "Esercizio 3.2: Algoritmi di ordinamento (E2)"

    Consideriamo il problema di <strong>verificare</strong> se un array $a[1..n]$ di $n\ge 1$ numeri naturali è ordinato in ordine non decrescente, e il seguente algoritmo.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> IsSorted</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><code>true</code> se <span class="arithmatex">&#92;(a&#91;1&#93;&#92;le a&#91;2&#93;&#92;le&#92;cdots&#92;le a&#91;n&#93;&#92;)</span>, <code>false</code> altrimenti</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> IsSorted(a, n)</span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n-1&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; a&#91;i+1&#93;&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-03-ordinamento-exs2-f"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>true</code></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Applicare <code>IsSorted</code> agli array $[1,3,3,7,9]$, $[2,5,4,8]$, $[9,1,2,3]$ e $[1]$. Per ciascun array indicare l'output e il numero di passi eseguiti.

    2. <code>IsSorted</code> è un algoritmo basato su confronti? Quanti confronti tra chiavi esegue nel caso peggiore?

    3. Sia $S(n)$ il numero di passi eseguiti da <code>IsSorted</code> nel caso peggiore, per un array di $n$ elementi. Calcolare $S(n)$ e confrontare il numero di confronti tra chiavi di <code>IsSorted</code> con il numero di confronti tra chiavi nel caso peggiore degli algoritmi di ordinamento del capitolo.

    4. Dimostrare che <code>IsSorted</code> restituisce <code>true</code> se e solo se l'array $a[1..n]$ è ordinato in ordine non decrescente.

??? soluzione "Soluzione"

    1. Executions:

        - $[1,3,3,7,9]$ ($n=5$): i confronti $1\le 3$, $3\le 3$, $3\le 7$, $7\le 9$ sono tutti soddisfatti; il ciclo termina quando $i=5$ e l'output è <code>true</code>. Passi: riga [2](#riga-es-03-ordinamento-exs2-a) una volta, riga [3](#riga-es-03-ordinamento-exs2-b) $5$ volte, righe [4](#riga-es-03-ordinamento-exs2-c) e [7](#riga-es-03-ordinamento-exs2-e) $4$ volte ciascuna, riga [9](#riga-es-03-ordinamento-exs2-f) una volta:

            $$
            1+5+4+4+1=15.
            $$

        - $[2,5,4,8]$ ($n=4$): $a[1]=2\le 5$; poi $a[2]=5>a[3]=4$, quindi l'output è <code>false</code> per $i=2$. Passi: riga [2](#riga-es-03-ordinamento-exs2-a) una volta, riga [3](#riga-es-03-ordinamento-exs2-b) due volte, riga [4](#riga-es-03-ordinamento-exs2-c) due volte, riga [7](#riga-es-03-ordinamento-exs2-e) una volta, riga [5](#riga-es-03-ordinamento-exs2-d) una volta:

            $$
            1+2+2+1+1=7.
            $$

        - $[9,1,2,3]$ ($n=4$): $a[1]=9>a[2]=1$, quindi l'output è <code>false</code> per $i=1$. Passi: le righe [2](#riga-es-03-ordinamento-exs2-a), [3](#riga-es-03-ordinamento-exs2-b), [4](#riga-es-03-ordinamento-exs2-c), [5](#riga-es-03-ordinamento-exs2-d) una volta ciascuna:

            $$
            1+1+1+1=4.
            $$

        - $[1]$ ($n=1$): la condizione $1\le 0$ è falsa e l'output è <code>true</code>. Passi: le righe [2](#riga-es-03-ordinamento-exs2-a), [3](#riga-es-03-ordinamento-exs2-b), [9](#riga-es-03-ordinamento-exs2-f) una volta ciascuna:

            $$
            1+1+1=3.
            $$

    2. Sì: l'algoritmo accede alle chiavi soltanto per confrontarne due (riga [4](#riga-es-03-ordinamento-exs2-c)); non le modifica mai e non esegue mai operazioni aritmetiche su di esse. Nel caso peggiore esegue $n-1$ confronti tra chiavi, uno per ogni coppia di posizioni consecutive.

    3. Il caso peggiore è quello in cui l'algoritmo non ritorna mai alla riga [5](#riga-es-03-ordinamento-exs2-d), cioè quando l'array <strong>è</strong> ordinato. Il numero di volte in cui ciascuna riga viene eseguita è:

        - la riga [2](#riga-es-03-ordinamento-exs2-a) viene eseguita $1$ volta;

        - la riga [3](#riga-es-03-ordinamento-exs2-b) viene eseguita $n$ volte;

        - la riga [4](#riga-es-03-ordinamento-exs2-c) viene eseguita $n-1$ volte;

        - la riga [5](#riga-es-03-ordinamento-exs2-d) non viene eseguita;

        - la riga [7](#riga-es-03-ordinamento-exs2-e) viene eseguita $n-1$ volte;

        - la riga [9](#riga-es-03-ordinamento-exs2-f) viene eseguita $1$ volta.

        Quindi

        $$
        S(n)=1+n+(n-1)+(n-1)+1=3n,
        $$

        in accordo con il punto 1 ($15=3\cdot 5$ per l'array ordinato di $5$ elementi, $3=3\cdot 1$ per $n=1$).

        !!! chiave ""

            Verificare se un array è ordinato richiede al più $n-1$ confronti tra chiavi, un numero che cresce linearmente con $n$, mentre Insertion Sort, Exchange Sort e Selection Sort eseguono $\frac{n(n-1)}{2}$ confronti tra chiavi nel caso peggiore, un numero che cresce quadraticamente con $n$. Per $n=100$: $99$ confronti contro $4\,950$.

    4. L'algoritmo restituisce <code>false</code> soltanto alla riga [5](#riga-es-03-ordinamento-exs2-d), e soltanto dopo aver trovato un indice $i$ con $a[i] > a[i+1]$: in questo caso l'array non è ordinato, perché due elementi consecutivi sono nell'ordine sbagliato. Quindi, se l'array è ordinato, l'algoritmo non restituisce mai <code>false</code>; poiché $i$ aumenta di $1$ a ogni iterazione, il ciclo termina dopo $n-1$ iterazioni e l'algoritmo restituisce <code>true</code> alla riga [9](#riga-es-03-ordinamento-exs2-f).

        Viceversa, se l'algoritmo restituisce <code>true</code>, il ciclo è stato completato, quindi il confronto alla riga [4](#riga-es-03-ordinamento-exs2-c) era falso per ogni $i \in \{1, 2, \dots, n-1\}$:

        $$
        a[1] \le a[2], \quad a[2] \le a[3], \quad \dots, \quad a[n-1] \le a[n].
        $$

        Concatenando queste disuguaglianze, $a[1] \le a[2] \le \dots \le a[n]$: l'array è ordinato. Dunque <code>IsSorted</code> restituisce <code>true</code> se e solo se l'array è ordinato in ordine non decrescente.

<a id="esercizio-3-3"></a>

!!! esercizio "Esercizio 3.3: Algoritmi di ordinamento (E3)"

    Consideriamo l'array di record $(\mathit{key},\ \mathit{label})$, in cui si confrontano solo le chiavi,

    $$
    a=[(3,A),\ (1,B),\ (3,C),\ (2,D),\ (1,E)],
    $$

    e gli algoritmi Insertion Sort e Selection Sort del capitolo (Insertion Sort sposta $a[j]$ a destra finché $a[j]>\mathit{key}$; Selection Sort scambia $a[i]$ con il minimo di $a[i..n]$, scegliendo il primo minimo trovato).

    **Domande**

    1. Applicare Insertion Sort ad $a$, mostrando l'array dopo ogni iterazione del ciclo esterno. Il risultato è stabile?

    2. Applicare Selection Sort ad $a$, mostrando l'array dopo ogni iterazione del ciclo esterno. Il risultato è stabile?

    3. Uno studente sostituisce la condizione $a[j]>\mathit{key}$ di Insertion Sort con $a[j]\ge \mathit{key}$. Il nuovo algoritmo è ancora corretto? È stabile?

    4. Insertion Sort e Selection Sort sono in-place? Descrivere un metodo di ordinamento che non è in-place.

??? soluzione "Soluzione"

    1. Insertion Sort (la chiave inserita è evidenziata in <mark style="background:color-mix(in srgb, #e03131 30%, transparent);color:inherit">rosso</mark>):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>iniziale</td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa"><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td class="cella-rossa"><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td class="cella-rossa"><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td class="cella-rossa"><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        </tr>
        </table></div>

        Per $i=3$, $a[2]=(3,A)$ non è $>3$, quindi $(3,C)$ resta dopo $(3,A)$; per $i=5$, gli spostamenti si fermano in $(1,B)$, perché $1>1$ è falso. Nell'output $B$ precede $E$ e $A$ precede $C$, come nell'input: il risultato è <strong>stabile</strong>. In generale, Insertion Sort è stabile, perché una chiave non viene mai spostata prima di una chiave uguale (la condizione di spostamento è una disuguaglianza stretta).

    2. Selection Sort (le due posizioni scambiate sono evidenziate in <mark style="background:color-mix(in srgb, #1971c2 30%, transparent);color:inherit">blu</mark>):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        </tr>
        <tr>
        <td>iniziale</td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td></td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu"><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td>2</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td>5</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td>4</td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;((1,B)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((1,E)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((2,D)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,C)&#92;)</span></td>
        <td><span class="arithmatex">&#92;((3,A)&#92;)</span></td>
        <td>4 (nessuno scambio)</td>
        </tr>
        </table></div>

        Le chiavi sono ordinate, ma $(3,C)$ precede $(3,A)$, mentre nell'input $A$ precedeva $C$: il risultato <strong>non è stabile</strong>. Lo scambio per $i=2$ ha spostato $(3,A)$ dalla posizione $2$ alla posizione $5$, “saltando” $(3,C)$. Quindi Selection Sort non è stabile (un controesempio ancora più piccolo è $[(2,A),(2,B),(1,C)]$, che diventa $[(1,C),(2,B),(2,A)]$).

    3. Con $a[j]\ge \mathit{key}$ l'algoritmo è ancora <strong>corretto</strong>: le chiavi sono ancora ordinate, perché $\mathit{key}$ viene inserita dopo tutti gli elementi $<\mathit{key}$ e prima di tutti gli elementi $\ge \mathit{key}$. Tuttavia <strong>non è stabile</strong>, perché $\mathit{key}$ viene spostata prima delle chiavi uguali. Su $a$:

        $$
        [(3,A),(1,B),(3,C),(2,D),(1,E)]\ \longrightarrow\ [(1,E),(1,B),(2,D),(3,C),(3,A)],
        $$

        dove entrambe le coppie di chiavi uguali sono invertite. Inoltre esegue più spostamenti del necessario quando ci sono chiavi uguali.

    4. Entrambi gli algoritmi sono <strong>in-place</strong>: riarrangiano gli elementi all'interno dell'array $a$ e usano soltanto un numero costante di variabili ausiliarie ($i$, $j$, $\mathit{key}$ per Insertion Sort; $i$, $j$, $\mathit{minIdx}$, $\mathit{tmp}$ per Selection Sort), indipendentemente da $n$.

        Un metodo che <strong>non</strong> è in-place: creare un nuovo array $b[1..n]$; per $k \in \{1, 2, \dots, n\}$, trovare il minimo tra gli elementi di $a$ non ancora copiati, copiarlo in $b[k]$ e marcarlo come usato (ad esempio con un array di $n$ flag booleani); infine restituire $b$. Questo metodo usa memoria aggiuntiva proporzionale a $n$ (l'array $b$ e i flag), quindi non è in-place.

<a id="esercizio-3-4"></a>

!!! esercizio "Esercizio 3.4: Algoritmi di ordinamento (E4)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [5, 2, 4, 6, 1, 3]$

    2. $a = [8, 3, 7, 4, 9, 2]$

    3. $a = [6, 5, 4, 3, 2, 1]$

    4. $a = [1, 2, 3, 4, 5, 6]$

    5. $a = [10, 5, 15, 3]$

    **Domande**

    1. Applicare l'algoritmo <code>InsertionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare la chiave da inserire, ogni spostamento eseguito dal ciclo interno e lo stato dell'array dopo l'inserimento.

    2. Per ciascun array, contare i confronti tra chiavi $a[j] > \mathit{key}$ e gli spostamenti eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [5, 2, 4, 6, 1, 3]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">2</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>4</td>
        <td>2</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">6</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>5</td>
        <td class="cella-rossa">3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;6&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le 3&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>inserisci 4 tra 2 e 5</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">6</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>6 già al suo posto</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>3</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        <tr>
        <td>6</td>
        <td class="cella-rossa">3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>inserisci 3 tra 2 e 4</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 12 confronti tra chiavi e 9 spostamenti, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    2. Array $a = [8, 3, 7, 4, 9, 2]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">3</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=8&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">7</td>
        <td>3</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=7&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>7</td>
        <td>3</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=8&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td>8</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le 7&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>3</td>
        <td>7</td>
        <td>8</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>8</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">9</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=9&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td class="cella-blu">9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&#92;le 9&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>5</td>
        <td class="cella-rossa">2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;6&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">7</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">8</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>inserisci 7 tra 3 e 8</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">4</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">8</td>
        <td>9</td>
        <td>2</td>
        <td>inserisci 4 tra 3 e 7</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">9</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>2</td>
        <td>9 già al suo posto</td>
        </tr>
        <tr>
        <td>6</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">9</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 12 confronti tra chiavi e 9 spostamenti, e l'array ordinato è

        $$
        [2, 3, 4, 7, 8, 9].
        $$

    3. Array $a = [6, 5, 4, 3, 2, 1]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">5</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=6&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td>5</td>
        <td>6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>5</td>
        <td class="cella-rossa">1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;6&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">5</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>inserisci 5 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>inserisci 4 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>2</td>
        <td>1</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>1</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        <tr>
        <td>6</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 15 spostamenti, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    4. Array $a = [1, 2, 3, 4, 5, 6]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le 2&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le 3&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le 5&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>5</td>
        <td class="cella-rossa">6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;6&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>2 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>3 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>4 già al suo posto</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>5 già al suo posto</td>
        </tr>
        <tr>
        <td>6</td>
        <td class="cella-rossa">6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>6 già al suo posto</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 5 confronti tra chiavi e 0 spostamenti, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    5. Array $a = [10, 5, 15, 3]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">5</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>5</td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=10&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 10&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">15</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=15&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>5</td>
        <td>10</td>
        <td class="cella-blu">15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;le 15&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 15&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 15&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 10&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">5</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td>3</td>
        <td>inserisci 5 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">15</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>3</td>
        <td>15 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 5 confronti tra chiavi e 4 spostamenti, e l'array ordinato è

        $$
        [3, 5, 10, 15].
        $$

<a id="esercizio-3-5"></a>

!!! esercizio "Esercizio 3.5: Algoritmi di ordinamento (E5)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [7, 2, 9, 4]$

    2. $a = [15, 10, 5]$

    3. $a = [3, 1, 4, 1, 5, 9, 2, 6]$

    4. $a = [20, 18, 16, 14]$

    5. $a = [11, 11, 11]$

    **Domande**

    1. Applicare l'algoritmo <code>InsertionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare la chiave da inserire, ogni spostamento eseguito dal ciclo interno e lo stato dell'array dopo l'inserimento.

    2. Per ciascun array, contare i confronti tra chiavi $a[j] > \mathit{key}$ e gli spostamenti eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [7, 2, 9, 4]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">2</td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=7&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">9</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=9&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>2</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;le 9&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>4</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>4</td>
        <td>2</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">9</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td>9 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td>inserisci 4 tra 2 e 7</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 5 confronti tra chiavi e 3 spostamenti, e l'array ordinato è

        $$
        [2, 4, 7, 9].
        $$

    2. Array $a = [15, 10, 5]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">10</td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=10&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>10</td>
        <td>15</td>
        <td class="cella-blu">15</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=15&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 15&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 10&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">5</td>
        <td>10</td>
        <td>15</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=15&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 15&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>5</td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=10&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 10&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">10</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td>5</td>
        <td>inserisci 10 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">5</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td>inserisci 5 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 spostamenti, e l'array ordinato è

        $$
        [5, 10, 15].
        $$

    3. Array $a = [3, 1, 4, 1, 5, 9, 2, 6]$ ($n=8$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">1</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le 1&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le 5&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>5</td>
        <td class="cella-rossa">9</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;6&#93;=9&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;le 9&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td>7</td>
        <td>6</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;7&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;7&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&#92;le 2&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>8</td>
        <td>7</td>
        <td class="cella-rossa">6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;8&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=9&gt;6&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;8&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=5&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;7&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>4 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">1</td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>inserisci 1 tra 1 e 3</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>5 già al suo posto</td>
        </tr>
        <tr>
        <td>6</td>
        <td class="cella-rossa">9</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>9 già al suo posto</td>
        </tr>
        <tr>
        <td>7</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td>inserisci 2 tra 1 e 3</td>
        </tr>
        <tr>
        <td>8</td>
        <td class="cella-rossa">6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td>inserisci 6 tra 5 e 9</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 14 confronti tra chiavi e 8 spostamenti, e l'array ordinato è

        $$
        [1, 1, 2, 3, 4, 5, 6, 9].
        $$

    4. Array $a = [20, 18, 16, 14]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">18</td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=18&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>18</td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;18&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 20&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>18</td>
        <td class="cella-blu">18</td>
        <td>20</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 18&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">16</td>
        <td>18</td>
        <td>20</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=16&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=20&gt;16&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 20&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>16</td>
        <td>18</td>
        <td class="cella-blu">18</td>
        <td>20</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=18&gt;16&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 18&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>16</td>
        <td class="cella-blu">16</td>
        <td>18</td>
        <td>20</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 16&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=14&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=20&gt;14&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 20&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td class="cella-blu">18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=18&gt;14&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 18&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>14</td>
        <td>16</td>
        <td class="cella-blu">16</td>
        <td>18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=16&gt;14&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 16&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td class="cella-blu">14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 14&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">18</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td>16</td>
        <td>14</td>
        <td>inserisci 18 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">16</td>
        <td class="cella-blu">16</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td>14</td>
        <td>inserisci 16 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">14</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">16</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td>inserisci 14 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 spostamenti, e l'array ordinato è

        $$
        [14, 16, 18, 20].
        $$

    5. Array $a = [11, 11, 11]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">11</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=11&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td class="cella-blu">11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=11&#92;le 11&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 11&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">11</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=11&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td class="cella-blu">11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&#92;le 11&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 11&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">11</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>11 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">11</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>11 già al suo posto</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 2 confronti tra chiavi e 0 spostamenti, e l'array ordinato è

        $$
        [11, 11, 11].
        $$

<a id="esercizio-3-6"></a>

!!! esercizio "Esercizio 3.6: Algoritmi di ordinamento (E6)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [9, 3, 7, 2]$

    2. $a = [12, 4, 18, 6, 10]$

    3. $a = [5, 4, 3, 2, 1]$

    4. $a = [100, 50, 25]$

    5. $a = [8]$

    **Domande**

    1. Applicare l'algoritmo <code>InsertionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare la chiave da inserire, ogni spostamento eseguito dal ciclo interno e lo stato dell'array dopo l'inserimento.

    2. Per ciascun array, contare i confronti tra chiavi $a[j] > \mathit{key}$ e gli spostamenti eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [9, 3, 7, 2]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">3</td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=9&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">7</td>
        <td>3</td>
        <td>9</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=7&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>7</td>
        <td>3</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=9&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le 7&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">9</td>
        <td>7</td>
        <td>2</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">7</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td>2</td>
        <td>inserisci 7 tra 3 e 9</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 5 spostamenti, e l'array ordinato è

        $$
        [2, 3, 7, 9].
        $$

    2. Array $a = [12, 4, 18, 6, 10]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">4</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>4</td>
        <td>12</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=12&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 12&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">18</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=18&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>18</td>
        <td>4</td>
        <td>12</td>
        <td class="cella-blu">18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=12&#92;le 18&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 18&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">6</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>6</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td class="cella-blu">18</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=18&gt;6&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 18&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>6</td>
        <td>4</td>
        <td>12</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=12&gt;6&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 12&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>12</td>
        <td>18</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">10</td>
        <td>4</td>
        <td>6</td>
        <td>12</td>
        <td>18</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=10&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>10</td>
        <td>4</td>
        <td>6</td>
        <td>12</td>
        <td>18</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=18&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 18&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>10</td>
        <td>4</td>
        <td>6</td>
        <td>12</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=12&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 12&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td>12</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;le 10&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 10&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>inserisci 4 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">18</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>18 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">6</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">18</td>
        <td>10</td>
        <td>inserisci 6 tra 4 e 12</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">10</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">18</td>
        <td>inserisci 10 tra 6 e 12</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 8 confronti tra chiavi e 5 spostamenti, e l'array ordinato è

        $$
        [4, 6, 10, 12, 18].
        $$

    3. Array $a = [5, 4, 3, 2, 1]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">4</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">3</td>
        <td>4</td>
        <td>5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 5&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 4&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>inserisci 4 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>2</td>
        <td>1</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>1</td>
        <td>inserisci 2 all'inizio</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 10 spostamenti, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5].
        $$

    4. Array $a = [100, 50, 25]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">50</td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=50&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>50</td>
        <td>100</td>
        <td class="cella-blu">100</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=100&gt;50&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 100&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>50</td>
        <td class="cella-blu">50</td>
        <td>100</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 50&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">25</td>
        <td>50</td>
        <td>100</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=25&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>25</td>
        <td>50</td>
        <td>100</td>
        <td class="cella-blu">100</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=100&gt;25&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 100&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>25</td>
        <td>50</td>
        <td class="cella-blu">50</td>
        <td>100</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=50&gt;25&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 50&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td>100</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 25&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">50</td>
        <td class="cella-blu">50</td>
        <td class="cella-blu">100</td>
        <td>25</td>
        <td>inserisci 50 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">25</td>
        <td class="cella-blu">25</td>
        <td class="cella-blu">50</td>
        <td class="cella-blu">100</td>
        <td>inserisci 25 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 spostamenti, e l'array ordinato è

        $$
        [25, 50, 100].
        $$

    5. Array $a = [8]$ ($n=1$).

        L'array ha un solo elemento: il ciclo esterno non viene eseguito e l'array è già ordinato.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td>8</td>
        <td>stato iniziale: <span class="arithmatex">&#92;(n=1&#92;)</span>, il ciclo esterno non viene eseguito</td>
        </tr>
        </table></div>

        L'array ordinato è $[8]$, ottenuto senza alcun confronto tra chiavi e senza alcuno spostamento.

<a id="esercizio-3-7"></a>

!!! esercizio "Esercizio 3.7: Algoritmi di ordinamento (E7)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [6, 1, 8, 2, 5]$

    2. $a = [13, 11, 9, 7]$

    3. $a = [2, 8, 4, 6]$

    4. $a = [30, 20, 10]$

    5. $a = [5, 10, 15, 20]$

    **Domande**

    1. Applicare l'algoritmo <code>InsertionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare la chiave da inserire, ogni spostamento eseguito dal ciclo interno e lo stato dell'array dopo l'inserimento.

    2. Per ciascun array, contare i confronti tra chiavi $a[j] > \mathit{key}$ e gli spostamenti eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [6, 1, 8, 2, 5]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">1</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=6&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">8</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=8&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>1</td>
        <td>6</td>
        <td class="cella-blu">8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;le 8&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>6</td>
        <td>8</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le 2&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>2</td>
        <td>6</td>
        <td>8</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=5&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>6</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;5&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le 5&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 5&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">8</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>8 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td>5</td>
        <td>inserisci 2 tra 1 e 6</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td>inserisci 5 tra 2 e 6</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 8 confronti tra chiavi e 5 spostamenti, e l'array ordinato è

        $$
        [1, 2, 5, 6, 8].
        $$

    2. Array $a = [13, 11, 9, 7]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">11</td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=11&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>11</td>
        <td>13</td>
        <td class="cella-blu">13</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=13&gt;11&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 13&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td class="cella-blu">11</td>
        <td>13</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 11&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">9</td>
        <td>11</td>
        <td>13</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=9&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td class="cella-blu">13</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=13&gt;9&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 13&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>9</td>
        <td>11</td>
        <td class="cella-blu">11</td>
        <td>13</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=11&gt;9&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 11&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td>11</td>
        <td>13</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=7&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td class="cella-blu">13</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=13&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 13&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td class="cella-blu">11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 11&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td>11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=9&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 7&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">11</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td>9</td>
        <td>7</td>
        <td>inserisci 11 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">9</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td>7</td>
        <td>inserisci 9 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">7</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td>inserisci 7 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 spostamenti, e l'array ordinato è

        $$
        [7, 9, 11, 13].
        $$

    3. Array $a = [2, 8, 4, 6]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">8</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=8&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>2</td>
        <td class="cella-blu">8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le 8&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=4&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>4</td>
        <td>2</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=8&gt;4&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le 4&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">6</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>6</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;6&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 8&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">8</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>8 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td>inserisci 4 tra 2 e 8</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">6</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td>inserisci 6 tra 4 e 8</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 5 confronti tra chiavi e 2 spostamenti, e l'array ordinato è

        $$
        [2, 4, 6, 8].
        $$

    4. Array $a = [30, 20, 10]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">20</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=20&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>20</td>
        <td>30</td>
        <td class="cella-blu">30</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=30&gt;20&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 30&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>30</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 20&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">10</td>
        <td>20</td>
        <td>30</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=10&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=30&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 30&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>10</td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 20&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>20</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 10&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">20</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td>10</td>
        <td>inserisci 20 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">10</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td>inserisci 10 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 spostamenti, e l'array ordinato è

        $$
        [10, 20, 30].
        $$

    5. Array $a = [5, 10, 15, 20]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">10</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=10&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;le 10&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 10&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">15</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=15&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>5</td>
        <td>10</td>
        <td class="cella-blu">15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;le 15&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 15&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">20</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=20&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;le 20&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 20&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">10</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>10 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">15</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>15 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">20</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>20 già al suo posto</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 0 spostamenti, e l'array ordinato è

        $$
        [5, 10, 15, 20].
        $$

<a id="esercizio-3-8"></a>

!!! esercizio "Esercizio 3.8: Algoritmi di ordinamento (E8)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [14, 7, 21, 3, 18]$

    2. $a = [40, 30, 20, 10]$

    3. $a = [3, 6, 1, 9, 2]$

    4. $a = [25, 12, 50]$

    5. $a = [17, 17, 17, 17]$

    **Domande**

    1. Applicare l'algoritmo <code>InsertionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare la chiave da inserire, ogni spostamento eseguito dal ciclo interno e lo stato dell'array dopo l'inserimento.

    2. Per ciascun array, contare i confronti tra chiavi $a[j] > \mathit{key}$ e gli spostamenti eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [14, 7, 21, 3, 18]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">7</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=7&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=14&gt;7&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 14&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">21</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=21&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>21</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=14&#92;le 21&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 21&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=3&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=21&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 21&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=14&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 14&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=7&gt;3&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 7&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">18</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=18&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>18</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td class="cella-blu">21</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=21&gt;18&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 21&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>18</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td>21</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=14&#92;le 18&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 18&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">7</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>inserisci 7 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">21</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>21 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">3</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td>inserisci 3 all'inizio</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">18</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">21</td>
        <td>inserisci 18 tra 14 e 21</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 7 confronti tra chiavi e 5 spostamenti, e l'array ordinato è

        $$
        [3, 7, 14, 18, 21].
        $$

    2. Array $a = [40, 30, 20, 10]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">30</td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=30&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>30</td>
        <td>40</td>
        <td class="cella-blu">40</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=40&gt;30&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 40&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td class="cella-blu">30</td>
        <td>40</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 30&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">20</td>
        <td>30</td>
        <td>40</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=20&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td class="cella-blu">40</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=40&gt;20&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 40&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>20</td>
        <td>30</td>
        <td class="cella-blu">30</td>
        <td>40</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=30&gt;20&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 30&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>30</td>
        <td>40</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 20&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=10&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td class="cella-blu">40</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=40&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 40&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td class="cella-blu">30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=30&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 30&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>10</td>
        <td>20</td>
        <td class="cella-blu">20</td>
        <td>30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;10&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 20&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td class="cella-blu">10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 10&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">30</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td>20</td>
        <td>10</td>
        <td>inserisci 30 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">20</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td>10</td>
        <td>inserisci 20 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">10</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td>inserisci 10 all'inizio</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 spostamenti, e l'array ordinato è

        $$
        [10, 20, 30, 40].
        $$

    3. Array $a = [3, 6, 1, 9, 2]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">6</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=6&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>3</td>
        <td class="cella-blu">6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le 6&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">1</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=1&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;1&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">9</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=9&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td class="cella-blu">9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&#92;le 9&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>4</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;5&#93;=2&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftarrow 9&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 6&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;2&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 3&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le 2&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 2&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">6</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>6 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td>2</td>
        <td>inserisci 1 all'inizio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">9</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td>9 già al suo posto</td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-rossa">2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td>inserisci 2 tra 1 e 3</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 8 confronti tra chiavi e 5 spostamenti, e l'array ordinato è

        $$
        [1, 2, 3, 6, 9].
        $$

    4. Array $a = [25, 12, 50]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">12</td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=12&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>0</td>
        <td>12</td>
        <td>25</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=25&gt;12&#92;)</span>: sposta <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 25&#92;)</span>; <span class="arithmatex">&#92;(j&#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td class="cella-blu">12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(j=0&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftarrow 12&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">50</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=50&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>50</td>
        <td>12</td>
        <td>25</td>
        <td class="cella-blu">50</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=25&#92;le 50&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 50&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">12</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td>inserisci 12 all'inizio</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">50</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td>50 già al suo posto</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 2 confronti tra chiavi e 1 spostamento, e l'array ordinato è

        $$
        [12, 25, 50].
        $$

    5. Array $a = [17, 17, 17, 17]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;2&#93;=17&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td class="cella-blu">17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=17&#92;le 17&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftarrow 17&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;3&#93;=17&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td class="cella-blu">17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=17&#92;le 17&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftarrow 17&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{key} &#92;leftarrow a&#91;4&#93;=17&#92;)</span>; <span class="arithmatex">&#92;(j &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td class="cella-blu">17</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=17&#92;le 17&#92;)</span>: esci; inserisci <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftarrow 17&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{key}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17 già al suo posto</td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17 già al suo posto</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-rossa">17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17 già al suo posto</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 0 spostamenti, e l'array ordinato è

        $$
        [17, 17, 17, 17].
        $$

<a id="esercizio-3-9"></a>

!!! esercizio "Esercizio 3.9: Algoritmi di ordinamento (E9)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [5, 2, 4, 6, 1, 3]$

    2. $a = [8, 3, 7, 4, 9, 2]$

    3. $a = [6, 5, 4, 3, 2, 1]$

    4. $a = [1, 2, 3, 4, 5, 6]$

    5. $a = [10, 5, 15, 3]$

    **Domande**

    1. Applicare l'algoritmo <code>ExchangeSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni confronto, dire se viene eseguito uno scambio e indicare lo stato dell'array dopo il confronto.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [5, 2, 4, 6, 1, 3]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;a&#91;2&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;3&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td class="cella-blu">1</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;a&#91;5&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;6&#93;=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;a&#91;3&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>5</td>
        <td>6</td>
        <td class="cella-blu">4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;a&#91;5&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;6&#93;=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;a&#91;5&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;a&#91;6&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&gt;a&#91;5&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;a&#91;6&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&gt;a&#91;6&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">5</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td class="cella-blu">4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 9 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    2. Array $a = [8, 3, 7, 4, 9, 2]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=8&gt;a&#91;2&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;3&#93;=7&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;4&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;5&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td class="cella-blu">2</td>
        <td>8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;6&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">8</td>
        <td>4</td>
        <td>9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=8&gt;a&#91;3&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>8</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;a&#91;4&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td>7</td>
        <td>9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&#92;le a&#91;5&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>8</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;a&#91;6&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">8</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;a&#91;4&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;le a&#91;5&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>8</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&gt;a&#91;6&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>8</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&#92;le a&#91;5&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&gt;a&#91;6&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&gt;a&#91;6&#93;=8&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">8</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=2&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=3&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=4&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=7&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=8&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 9 scambi, e l'array ordinato è

        $$
        [2, 3, 4, 7, 8, 9].
        $$

    3. Array $a = [6, 5, 4, 3, 2, 1]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=6&gt;a&#91;2&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;a&#91;3&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td class="cella-blu">2</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;5&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;a&#91;6&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;a&#91;3&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;a&#91;4&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;a&#91;5&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;a&#91;6&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;a&#91;4&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;a&#91;5&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;a&#91;6&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&gt;a&#91;5&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;a&#91;6&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&gt;a&#91;6&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span> (5 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span> (4 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 15 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    4. Array $a = [1, 2, 3, 4, 5, 6]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;2&#93;=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;3&#93;=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;4&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;6&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;3&#93;=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;4&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;6&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le a&#91;4&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le a&#91;6&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le a&#91;6&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;le a&#91;6&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span> (0 scambi)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    5. Array $a = [10, 5, 15, 3]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=10&gt;a&#91;2&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;le a&#91;3&#93;=15&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>10</td>
        <td>15</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>3</td>
        <td>10</td>
        <td>15</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;le a&#91;3&#93;=15&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>15</td>
        <td class="cella-blu">10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&gt;a&#91;4&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&gt;a&#91;4&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">10</td>
        <td>15</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=3&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>15</td>
        <td class="cella-blu">10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=5&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=10&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 4 scambi, e l'array ordinato è

        $$
        [3, 5, 10, 15].
        $$

<a id="esercizio-3-10"></a>

!!! esercizio "Esercizio 3.10: Algoritmi di ordinamento (E10)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [7, 2, 9, 4]$

    2. $a = [15, 10, 5]$

    3. $a = [3, 1, 4, 1, 5, 9, 2, 6]$

    4. $a = [20, 18, 16, 14]$

    5. $a = [11, 11, 11]$

    **Domande**

    1. Applicare l'algoritmo <code>ExchangeSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni confronto, dire se viene eseguito uno scambio e indicare lo stato dell'array dopo il confronto.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [7, 2, 9, 4]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=7&gt;a&#91;2&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;3&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;4&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;le a&#91;3&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;a&#91;4&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&gt;a&#91;4&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=4&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=7&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [2, 4, 7, 9].
        $$

    2. Array $a = [15, 10, 5]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=15&gt;a&#91;2&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>15</td>
        <td class="cella-blu">10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=10&gt;a&#91;3&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=15&gt;a&#91;3&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">15</td>
        <td class="cella-blu">10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=5&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=10&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [5, 10, 15].
        $$

    3. Array $a = [3, 1, 4, 1, 5, 9, 2, 6]$ ($n=8$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;2&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;3&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;4&#93;=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;6&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;7&#93;=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;le a&#91;3&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;a&#91;4&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&#92;le a&#91;6&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&#92;le a&#91;7&#93;=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;le a&#91;6&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&gt;a&#91;7&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>3</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=2&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>3</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>3</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;le a&#91;6&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&gt;a&#91;7&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;le a&#91;6&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&gt;a&#91;7&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>9</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=4&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>6</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&gt;a&#91;7&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=5&#92;le a&#91;8&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>7</td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=9&gt;a&#91;8&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;7&#93;&#92;leftrightarrow a&#91;8&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..8&#93;)=1&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..8&#93;)=1&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..8&#93;)=2&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..8&#93;)=3&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..8&#93;)=4&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=&#92;min(a&#91;6..8&#93;)=5&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=&#92;min(a&#91;7..8&#93;)=6&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 28 confronti tra chiavi e 8 scambi, e l'array ordinato è

        $$
        [1, 1, 2, 3, 4, 5, 6, 9].
        $$

    4. Array $a = [20, 18, 16, 14]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;a&#91;2&#93;=18&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">16</td>
        <td>20</td>
        <td class="cella-blu">18</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=18&gt;a&#91;3&#93;=16&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">14</td>
        <td>20</td>
        <td>18</td>
        <td class="cella-blu">16</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=16&gt;a&#91;4&#93;=14&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td>16</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=20&gt;a&#91;3&#93;=18&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>14</td>
        <td class="cella-blu">16</td>
        <td>20</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=18&gt;a&#91;4&#93;=16&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>14</td>
        <td>16</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=20&gt;a&#91;4&#93;=18&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">16</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=14&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>14</td>
        <td class="cella-blu">16</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=16&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>14</td>
        <td>16</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=18&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 scambi, e l'array ordinato è

        $$
        [14, 16, 18, 20].
        $$

    5. Array $a = [11, 11, 11]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=11&#92;le a&#91;2&#93;=11&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=11&#92;le a&#91;3&#93;=11&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&#92;le a&#91;3&#93;=11&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=11&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=11&#92;)</span> (0 scambi)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [11, 11, 11].
        $$

<a id="esercizio-3-11"></a>

!!! esercizio "Esercizio 3.11: Algoritmi di ordinamento (E11)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [9, 3, 7, 2]$

    2. $a = [12, 4, 18, 6, 10]$

    3. $a = [5, 4, 3, 2, 1]$

    4. $a = [100, 50, 25]$

    5. $a = [8]$

    **Domande**

    1. Applicare l'algoritmo <code>ExchangeSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni confronto, dire se viene eseguito uno scambio e indicare lo stato dell'array dopo il confronto.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [9, 3, 7, 2]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">9</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=9&gt;a&#91;2&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>9</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;3&#93;=7&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">2</td>
        <td>9</td>
        <td>7</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;4&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=9&gt;a&#91;3&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&gt;a&#91;4&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">9</td>
        <td>7</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=3&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=7&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 5 scambi, e l'array ordinato è

        $$
        [2, 3, 7, 9].
        $$

    2. Array $a = [12, 4, 18, 6, 10]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=12&gt;a&#91;2&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&#92;le a&#91;3&#93;=18&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&#92;le a&#91;5&#93;=10&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=12&#92;le a&#91;3&#93;=18&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>18</td>
        <td class="cella-blu">12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=12&gt;a&#91;4&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>18</td>
        <td>12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;le a&#91;5&#93;=10&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">18</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=18&gt;a&#91;4&#93;=12&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td>18</td>
        <td class="cella-blu">12</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=12&gt;a&#91;5&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=18&gt;a&#91;5&#93;=12&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=4&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>18</td>
        <td class="cella-blu">12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=6&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">12</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=10&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=12&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 5 scambi, e l'array ordinato è

        $$
        [4, 6, 10, 12, 18].
        $$

    3. Array $a = [5, 4, 3, 2, 1]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&gt;a&#91;2&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=4&gt;a&#91;3&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">2</td>
        <td>5</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;4&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td class="cella-blu">1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&gt;a&#91;5&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&gt;a&#91;3&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>5</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;a&#91;5&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&gt;a&#91;4&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&gt;a&#91;5&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=5&gt;a&#91;5&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span> (4 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=3&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=4&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 10 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5].
        $$

    4. Array $a = [100, 50, 25]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">50</td>
        <td class="cella-blu">100</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=100&gt;a&#91;2&#93;=50&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">25</td>
        <td>100</td>
        <td class="cella-blu">50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=50&gt;a&#91;3&#93;=25&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>25</td>
        <td class="cella-blu">50</td>
        <td class="cella-blu">100</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=100&gt;a&#91;3&#93;=50&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">25</td>
        <td class="cella-blu">100</td>
        <td class="cella-blu">50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=25&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>25</td>
        <td class="cella-blu">50</td>
        <td class="cella-blu">100</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=50&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [25, 50, 100].
        $$

    5. Array $a = [8]$ ($n=1$).

        L'array ha un solo elemento: il ciclo esterno non viene eseguito e l'array è già ordinato.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td>8</td>
        <td>stato iniziale: <span class="arithmatex">&#92;(n=1&#92;)</span>, il ciclo esterno non viene eseguito</td>
        </tr>
        </table></div>

        L'array ordinato è $[8]$, ottenuto senza alcun confronto tra chiavi e senza alcuno scambio.

<a id="esercizio-3-12"></a>

!!! esercizio "Esercizio 3.12: Algoritmi di ordinamento (E12)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [6, 1, 8, 2, 5]$

    2. $a = [13, 11, 9, 7]$

    3. $a = [2, 8, 4, 6]$

    4. $a = [30, 20, 10]$

    5. $a = [5, 10, 15, 20]$

    **Domande**

    1. Applicare l'algoritmo <code>ExchangeSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni confronto, dire se viene eseguito uno scambio e indicare lo stato dell'array dopo il confronto.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [6, 1, 8, 2, 5]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=6&gt;a&#91;2&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;3&#93;=8&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;4&#93;=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;le a&#91;3&#93;=8&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>8</td>
        <td class="cella-blu">6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;a&#91;4&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;le a&#91;5&#93;=5&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;a&#91;4&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td>8</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;a&#91;5&#93;=5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=8&gt;a&#91;5&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>8</td>
        <td class="cella-blu">6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=5&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=6&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 5 scambi, e l'array ordinato è

        $$
        [1, 2, 5, 6, 8].
        $$

    2. Array $a = [13, 11, 9, 7]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=13&gt;a&#91;2&#93;=11&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">9</td>
        <td>13</td>
        <td class="cella-blu">11</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=11&gt;a&#91;3&#93;=9&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td>13</td>
        <td>11</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=9&gt;a&#91;4&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=13&gt;a&#91;3&#93;=11&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td>13</td>
        <td class="cella-blu">11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&gt;a&#91;4&#93;=9&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=13&gt;a&#91;4&#93;=11&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">13</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=7&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">13</td>
        <td class="cella-blu">11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=9&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td class="cella-blu">11</td>
        <td class="cella-blu">13</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=11&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 scambi, e l'array ordinato è

        $$
        [7, 9, 11, 13].
        $$

    3. Array $a = [2, 8, 4, 6]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;2&#93;=8&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;3&#93;=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=8&gt;a&#91;3&#93;=4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&#92;le a&#91;4&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&gt;a&#91;4&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=4&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=6&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [2, 4, 6, 8].
        $$

    4. Array $a = [30, 20, 10]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=30&gt;a&#91;2&#93;=20&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">10</td>
        <td>30</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;a&#91;3&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=30&gt;a&#91;3&#93;=20&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=10&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=20&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [10, 20, 30].
        $$

    5. Array $a = [5, 10, 15, 20]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;le a&#91;2&#93;=10&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;le a&#91;3&#93;=15&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;le a&#91;4&#93;=20&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;le a&#91;3&#93;=15&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;le a&#91;4&#93;=20&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;le a&#91;4&#93;=20&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=5&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=10&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=15&#92;)</span> (0 scambi)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [5, 10, 15, 20].
        $$

<a id="esercizio-3-13"></a>

!!! esercizio "Esercizio 3.13: Algoritmi di ordinamento (E13)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [14, 7, 21, 3, 18]$

    2. $a = [40, 30, 20, 10]$

    3. $a = [3, 6, 1, 9, 2]$

    4. $a = [25, 12, 50]$

    5. $a = [17, 17, 17, 17]$

    **Domande**

    1. Applicare l'algoritmo <code>ExchangeSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni confronto, dire se viene eseguito uno scambio e indicare lo stato dell'array dopo il confronto.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [14, 7, 21, 3, 18]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=14&gt;a&#91;2&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=7&#92;le a&#91;3&#93;=21&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>14</td>
        <td>21</td>
        <td class="cella-blu">7</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=7&gt;a&#91;4&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>14</td>
        <td>21</td>
        <td>7</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;5&#93;=18&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>3</td>
        <td>14</td>
        <td>21</td>
        <td>7</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=14&#92;le a&#91;3&#93;=21&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td>21</td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=14&gt;a&#91;4&#93;=7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;le a&#91;5&#93;=18&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=21&gt;a&#91;4&#93;=14&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=14&#92;le a&#91;5&#93;=18&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">21</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=21&gt;a&#91;5&#93;=18&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">14</td>
        <td>21</td>
        <td class="cella-blu">7</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=3&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">7</td>
        <td>21</td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=7&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=14&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">21</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=18&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 5 scambi, e l'array ordinato è

        $$
        [3, 7, 14, 18, 21].
        $$

    2. Array $a = [40, 30, 20, 10]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=40&gt;a&#91;2&#93;=30&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">20</td>
        <td>40</td>
        <td class="cella-blu">30</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=30&gt;a&#91;3&#93;=20&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td class="cella-blu">10</td>
        <td>40</td>
        <td>30</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=20&gt;a&#91;4&#93;=10&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>10</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=40&gt;a&#91;3&#93;=30&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td>40</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=30&gt;a&#91;4&#93;=20&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>10</td>
        <td>20</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=40&gt;a&#91;4&#93;=30&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">40</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=10&#92;)</span> (3 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">40</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=20&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>10</td>
        <td>20</td>
        <td class="cella-blu">30</td>
        <td class="cella-blu">40</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=30&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 6 scambi, e l'array ordinato è

        $$
        [10, 20, 30, 40].
        $$

    3. Array $a = [3, 6, 1, 9, 2]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;le a&#91;2&#93;=6&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=3&gt;a&#91;3&#93;=1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;4&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;le a&#91;5&#93;=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&gt;a&#91;3&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;le a&#91;4&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>6</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&gt;a&#91;5&#93;=2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>6</td>
        <td>9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&#92;le a&#91;4&#93;=9&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&gt;a&#91;5&#93;=3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&gt;a&#91;5&#93;=6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">6</td>
        <td>9</td>
        <td class="cella-blu">3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span> (2 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=3&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=6&#92;)</span> (1 scambio)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 5 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 6, 9].
        $$

    4. Array $a = [25, 12, 50]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=25&gt;a&#91;2&#93;=12&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=12&#92;le a&#91;3&#93;=50&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=25&#92;le a&#91;3&#93;=50&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=12&#92;)</span> (1 scambio)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=25&#92;)</span> (0 scambi)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [12, 25, 50].
        $$

    5. Array $a = [17, 17, 17, 17]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=17&#92;le a&#91;2&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=17&#92;le a&#91;3&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=17&#92;le a&#91;4&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=17&#92;le a&#91;3&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=17&#92;le a&#91;4&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=17&#92;le a&#91;4&#93;=17&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=17&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=17&#92;)</span> (0 scambi)</td>
        </tr>
        <tr>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=17&#92;)</span> (0 scambi)</td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [17, 17, 17, 17].
        $$

<a id="esercizio-3-14"></a>

!!! esercizio "Esercizio 3.14: Algoritmi di ordinamento (E14)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [5, 2, 4, 6, 1, 3]$

    2. $a = [8, 3, 7, 4, 9, 2]$

    3. $a = [6, 5, 4, 3, 2, 1]$

    4. $a = [1, 2, 3, 4, 5, 6]$

    5. $a = [10, 5, 15, 3]$

    **Domande**

    1. Applicare l'algoritmo <code>SelectionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare l'indice $\mathit{minIdx}$ del minimo trovato dal ciclo interno e dire se viene eseguito uno scambio.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [5, 2, 4, 6, 1, 3]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&lt;a&#91;1&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=1&lt;a&#91;2&#93;=2&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=3&#92;ge a&#91;5&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=3&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;3&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;3&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=3&lt;a&#91;3&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=6&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&lt;a&#91;4&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=4&lt;a&#91;5&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=6&#92;ne 4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=5&#92;)</span> (<span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;5&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>5</td>
        <td class="cella-blu">1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">5</td>
        <td>3</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>3</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td>6</td>
        <td>5</td>
        <td class="cella-blu">4</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>6</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    2. Array $a = [8, 3, 7, 4, 9, 2]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=8&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&lt;a&#91;1&#93;=8&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=2&lt;a&#91;2&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=6&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=8&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&lt;a&#91;3&#93;=7&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=8&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;ge a&#91;4&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=8&#92;ge a&#91;4&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=5&#92;)</span> (<span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=8&lt;a&#91;5&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=6&#92;ne 5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>6</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td class="cella-blu">8</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>4</td>
        <td>9</td>
        <td>8</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>8</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td>9</td>
        <td>8</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=7&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>7</td>
        <td class="cella-blu">8</td>
        <td class="cella-blu">9</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=8&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [2, 3, 4, 7, 8, 9].
        $$

    3. Array $a = [6, 5, 4, 3, 2, 1]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&lt;a&#91;1&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&lt;a&#91;2&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;3&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=2&lt;a&#91;4&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>6</td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=1&lt;a&#91;5&#93;=2&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=6&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&lt;a&#91;2&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;3&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=2&lt;a&#91;4&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;5&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;3&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=5&#92;)</span> (<span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;5&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>6</td>
        <td class="cella-blu">1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;6&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>4</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    4. Array $a = [1, 2, 3, 4, 5, 6]$ ($n=6$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=1&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;ge a&#91;1&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;ge a&#91;1&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;1&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;1&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;1&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=2&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=5&#92;)</span> (<span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;ge a&#91;5&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..6&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..6&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..6&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..6&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..6&#93;)=5&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 15 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5, 6].
        $$

    5. Array $a = [10, 5, 15, 3]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=10&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=5&lt;a&#91;1&#93;=10&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;ge a&#91;2&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;2&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>15</td>
        <td class="cella-blu">10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;ge a&#91;2&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=10&#92;ge a&#91;2&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=10&lt;a&#91;3&#93;=15&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td>3</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>15</td>
        <td class="cella-blu">10</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>15</td>
        <td>10</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=5&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">15</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=10&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [3, 5, 10, 15].
        $$

<a id="esercizio-3-15"></a>

!!! esercizio "Esercizio 3.15: Algoritmi di ordinamento (E15)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [7, 2, 9, 4]$

    2. $a = [15, 10, 5]$

    3. $a = [3, 1, 4, 1, 5, 9, 2, 6]$

    4. $a = [20, 18, 16, 14]$

    5. $a = [11, 11, 11]$

    **Domande**

    1. Applicare l'algoritmo <code>SelectionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare l'indice $\mathit{minIdx}$ del minimo trovato dal ciclo interno e dire se viene eseguito uno scambio.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [7, 2, 9, 4]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=2&lt;a&#91;1&#93;=7&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;2&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&#92;ge a&#91;2&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>2</td>
        <td>7</td>
        <td>9</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&lt;a&#91;2&#93;=7&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>2</td>
        <td>4</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=7&lt;a&#91;3&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>2</td>
        <td>9</td>
        <td>4</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">2</td>
        <td class="cella-blu">7</td>
        <td>9</td>
        <td>4</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">7</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td class="cella-blu">9</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=7&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [2, 4, 7, 9].
        $$

    2. Array $a = [15, 10, 5]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=15&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&lt;a&#91;1&#93;=15&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=5&lt;a&#91;2&#93;=10&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">5</td>
        <td>10</td>
        <td class="cella-blu">15</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;ge a&#91;2&#93;=10&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>15</td>
        <td>10</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">5</td>
        <td>10</td>
        <td class="cella-blu">15</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=5&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=10&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [5, 10, 15].
        $$

    3. Array $a = [3, 1, 4, 1, 5, 9, 2, 6]$ ($n=8$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&lt;a&#91;1&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=1&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=2&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=1&lt;a&#91;2&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;ge a&#91;4&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=2&#92;ge a&#91;4&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>4</td>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;4&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;3&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=2&lt;a&#91;4&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;7&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=7&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=4&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=5&#92;)</span> (<span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;ge a&#91;5&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=4&lt;a&#91;5&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;7&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=7&#92;ne 5&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>9</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=6&#92;)</span> (<span class="arithmatex">&#92;(a&#91;6&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>7</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>9</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;7&#93;=5&lt;a&#91;6&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>9</td>
        <td>5</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&#92;ge a&#91;7&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=7&#92;ne 6&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>7</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=7&#92;)</span> (<span class="arithmatex">&#92;(a&#91;7&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;8&#93;=6&lt;a&#91;7&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=8&#92;ne 7&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;7&#93;&#92;leftrightarrow a&#91;8&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;6&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;7&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;8&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">3</td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..8&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>5</td>
        <td>9</td>
        <td>2</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..8&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td class="cella-blu">4</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..8&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>9</td>
        <td>4</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..8&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>9</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;5&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;5&#93;=&#92;min(a&#91;5..8&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>6</td>
        <td>7</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td class="cella-blu">5</td>
        <td class="cella-blu">9</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;6&#93;&#92;leftrightarrow a&#91;7&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;6&#93;=&#92;min(a&#91;6..8&#93;)=5&#92;)</span></td>
        </tr>
        <tr>
        <td>7</td>
        <td>8</td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;7&#93;&#92;leftrightarrow a&#91;8&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;7&#93;=&#92;min(a&#91;7..8&#93;)=6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 28 confronti tra chiavi e 6 scambi, e l'array ordinato è

        $$
        [1, 1, 2, 3, 4, 5, 6, 9].
        $$

    4. Array $a = [20, 18, 16, 14]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=20&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=18&lt;a&#91;1&#93;=20&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=16&lt;a&#91;2&#93;=18&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=14&lt;a&#91;3&#93;=16&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td>16</td>
        <td class="cella-blu">20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>14</td>
        <td>18</td>
        <td>16</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=18&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>14</td>
        <td>18</td>
        <td>16</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=16&lt;a&#91;2&#93;=18&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>14</td>
        <td>18</td>
        <td>16</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=20&#92;ge a&#91;3&#93;=16&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td class="cella-blu">16</td>
        <td class="cella-blu">18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=18&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=20&#92;ge a&#91;3&#93;=18&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>20</td>
        <td>18</td>
        <td>16</td>
        <td>14</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td>16</td>
        <td class="cella-blu">20</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=14&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>14</td>
        <td class="cella-blu">16</td>
        <td class="cella-blu">18</td>
        <td>20</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=16&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>14</td>
        <td>16</td>
        <td>18</td>
        <td>20</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=18&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [14, 16, 18, 20].
        $$

    5. Array $a = [11, 11, 11]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=11&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&#92;ge a&#91;1&#93;=11&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=11&#92;ge a&#91;1&#93;=11&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=11&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=11&#92;ge a&#91;2&#93;=11&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=11&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>11</td>
        <td>11</td>
        <td>11</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=11&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [11, 11, 11].
        $$

<a id="esercizio-3-16"></a>

!!! esercizio "Esercizio 3.16: Algoritmi di ordinamento (E16)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [9, 3, 7, 2]$

    2. $a = [12, 4, 18, 6, 10]$

    3. $a = [5, 4, 3, 2, 1]$

    4. $a = [100, 50, 25]$

    5. $a = [8]$

    **Domande**

    1. Applicare l'algoritmo <code>SelectionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare l'indice $\mathit{minIdx}$ del minimo trovato dal ciclo interno e dire se viene eseguito uno scambio.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [9, 3, 7, 2]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&lt;a&#91;1&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=2&lt;a&#91;2&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;ge a&#91;2&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;ge a&#91;3&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>3</td>
        <td>7</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=7&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [2, 3, 7, 9].
        $$

    2. Array $a = [12, 4, 18, 6, 10]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=12&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&lt;a&#91;1&#93;=12&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=18&#92;ge a&#91;2&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;2&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=10&#92;ge a&#91;2&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=12&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=18&#92;ge a&#91;2&#93;=12&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&lt;a&#91;2&#93;=12&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>4</td>
        <td>12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=10&#92;ge a&#91;4&#93;=6&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>18</td>
        <td class="cella-blu">12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>4</td>
        <td>6</td>
        <td>18</td>
        <td>12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=18&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>18</td>
        <td>12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=12&lt;a&#91;3&#93;=18&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td>18</td>
        <td>12</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=10&lt;a&#91;4&#93;=12&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td>12</td>
        <td class="cella-blu">18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td>12</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=12&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td>12</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=18&#92;ge a&#91;4&#93;=12&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td>12</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>4</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">12</td>
        <td>18</td>
        <td>6</td>
        <td>10</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td>18</td>
        <td class="cella-blu">12</td>
        <td>10</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=6&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>5</td>
        <td>4</td>
        <td>6</td>
        <td class="cella-blu">10</td>
        <td>12</td>
        <td class="cella-blu">18</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=10&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>6</td>
        <td>10</td>
        <td>12</td>
        <td>18</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=12&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [4, 6, 10, 12, 18].
        $$

    3. Array $a = [5, 4, 3, 2, 1]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=4&lt;a&#91;1&#93;=5&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&lt;a&#91;2&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=2&lt;a&#91;3&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=1&lt;a&#91;4&#93;=2&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&lt;a&#91;2&#93;=4&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=2&lt;a&#91;3&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=4&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>5</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td class="cella-blu">4</td>
        <td>5</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=4&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 4, 5].
        $$

    4. Array $a = [100, 50, 25]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=100&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=50&lt;a&#91;1&#93;=100&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=25&lt;a&#91;2&#93;=50&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td class="cella-blu">100</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>25</td>
        <td>50</td>
        <td>100</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=50&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>25</td>
        <td>50</td>
        <td>100</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=100&#92;ge a&#91;2&#93;=50&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>50</td>
        <td>100</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>100</td>
        <td>50</td>
        <td>25</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td class="cella-blu">100</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=25&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>25</td>
        <td>50</td>
        <td>100</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=50&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [25, 50, 100].
        $$

    5. Array $a = [8]$ ($n=1$).

        L'array ha un solo elemento: il ciclo esterno non viene eseguito e l'array è già ordinato.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td>8</td>
        <td>stato iniziale: <span class="arithmatex">&#92;(n=1&#92;)</span>, il ciclo esterno non viene eseguito</td>
        </tr>
        </table></div>

        L'array ordinato è $[8]$, ottenuto senza alcun confronto tra chiavi e senza alcuno scambio.

<a id="esercizio-3-17"></a>

!!! esercizio "Esercizio 3.17: Algoritmi di ordinamento (E17)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [6, 1, 8, 2, 5]$

    2. $a = [13, 11, 9, 7]$

    3. $a = [2, 8, 4, 6]$

    4. $a = [30, 20, 10]$

    5. $a = [5, 10, 15, 20]$

    **Domande**

    1. Applicare l'algoritmo <code>SelectionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare l'indice $\mathit{minIdx}$ del minimo trovato dal ciclo interno e dire se viene eseguito uno scambio.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [6, 1, 8, 2, 5]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=1&lt;a&#91;1&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=2&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;2&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=8&#92;ge a&#91;2&#93;=6&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=2&lt;a&#91;2&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&#92;ge a&#91;4&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>8</td>
        <td class="cella-blu">6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=8&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&lt;a&#91;3&#93;=8&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=5&lt;a&#91;4&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=8&#92;ge a&#91;4&#93;=6&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>1</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">6</td>
        <td>8</td>
        <td>2</td>
        <td>5</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>8</td>
        <td class="cella-blu">6</td>
        <td>5</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">5</td>
        <td>6</td>
        <td class="cella-blu">8</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=5&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>5</td>
        <td>6</td>
        <td>8</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [1, 2, 5, 6, 8].
        $$

    2. Array $a = [13, 11, 9, 7]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=13&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=11&lt;a&#91;1&#93;=13&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&lt;a&#91;2&#93;=11&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=7&lt;a&#91;3&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">7</td>
        <td>11</td>
        <td>9</td>
        <td class="cella-blu">13</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>7</td>
        <td>11</td>
        <td>9</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=11&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>7</td>
        <td>11</td>
        <td>9</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=9&lt;a&#91;2&#93;=11&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>11</td>
        <td>9</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=13&#92;ge a&#91;3&#93;=9&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=11&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=13&#92;ge a&#91;3&#93;=11&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>13</td>
        <td>11</td>
        <td>9</td>
        <td>7</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">7</td>
        <td>11</td>
        <td>9</td>
        <td class="cella-blu">13</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=7&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">9</td>
        <td class="cella-blu">11</td>
        <td>13</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=9&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>7</td>
        <td>9</td>
        <td>11</td>
        <td>13</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=11&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [7, 9, 11, 13].
        $$

    3. Array $a = [2, 8, 4, 6]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=2&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=8&#92;ge a&#91;1&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&#92;ge a&#91;1&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;1&#93;=2&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=8&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=4&lt;a&#91;2&#93;=8&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&#92;ge a&#91;3&#93;=4&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=8&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td>8</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=6&lt;a&#91;3&#93;=8&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>8</td>
        <td>4</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>2</td>
        <td class="cella-blu">4</td>
        <td class="cella-blu">8</td>
        <td>6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=4&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">8</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [2, 4, 6, 8].
        $$

    4. Array $a = [30, 20, 10]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=30&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=20&lt;a&#91;1&#93;=30&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=10&lt;a&#91;2&#93;=20&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">10</td>
        <td>20</td>
        <td class="cella-blu">30</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=20&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=30&#92;ge a&#91;2&#93;=20&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">10</td>
        <td>20</td>
        <td class="cella-blu">30</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=10&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=20&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [10, 20, 30].
        $$

    5. Array $a = [5, 10, 15, 20]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;ge a&#91;1&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;ge a&#91;1&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=20&#92;ge a&#91;1&#93;=5&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;ge a&#91;2&#93;=10&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=20&#92;ge a&#91;2&#93;=10&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=15&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=20&#92;ge a&#91;3&#93;=15&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=5&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=10&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>5</td>
        <td>10</td>
        <td>15</td>
        <td>20</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=15&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [5, 10, 15, 20].
        $$

<a id="esercizio-3-18"></a>

!!! esercizio "Esercizio 3.18: Algoritmi di ordinamento (E18)"

    Consideriamo i seguenti array di numeri naturali:

    1. $a = [14, 7, 21, 3, 18]$

    2. $a = [40, 30, 20, 10]$

    3. $a = [3, 6, 1, 9, 2]$

    4. $a = [25, 12, 50]$

    5. $a = [17, 17, 17, 17]$

    **Domande**

    1. Applicare l'algoritmo <code>SelectionSort</code> a ciascun array, per ordinarlo in ordine non decrescente. Mostrare l'esecuzione passo per passo: per ogni iterazione del ciclo esterno, indicare l'indice $\mathit{minIdx}$ del minimo trovato dal ciclo interno e dire se viene eseguito uno scambio.

    2. Per ciascun array, contare i confronti tra chiavi e gli scambi eseguiti dall'algoritmo.

??? soluzione "Soluzione"

    Le tabelle di traccia seguono le convenzioni enunciate nell'introduzione agli esercizi di questo capitolo. Ogni punto risponde a entrambe le domande.

    1. Array $a = [14, 7, 21, 3, 18]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=14&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=7&lt;a&#91;1&#93;=14&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=21&#92;ge a&#91;2&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&lt;a&#91;2&#93;=7&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=18&#92;ge a&#91;4&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">3</td>
        <td>7</td>
        <td>21</td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=21&#92;ge a&#91;2&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=14&#92;ge a&#91;2&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=18&#92;ge a&#91;2&#93;=7&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=21&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=14&lt;a&#91;3&#93;=21&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=18&#92;ge a&#91;4&#93;=14&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 3&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=21&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td>21</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=18&lt;a&#91;4&#93;=21&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">21</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>14</td>
        <td>7</td>
        <td>21</td>
        <td>3</td>
        <td>18</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">3</td>
        <td>7</td>
        <td>21</td>
        <td class="cella-blu">14</td>
        <td>18</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>7</td>
        <td>21</td>
        <td>14</td>
        <td>18</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=7&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>4</td>
        <td>3</td>
        <td>7</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">21</td>
        <td>18</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=14&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>3</td>
        <td>7</td>
        <td>14</td>
        <td class="cella-blu">18</td>
        <td class="cella-blu">21</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=18&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [3, 7, 14, 18, 21].
        $$

    2. Array $a = [40, 30, 20, 10]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=40&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=30&lt;a&#91;1&#93;=40&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=20&lt;a&#91;2&#93;=30&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>4</td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=10&lt;a&#91;3&#93;=20&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">10</td>
        <td>30</td>
        <td>20</td>
        <td class="cella-blu">40</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=4&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>10</td>
        <td>30</td>
        <td>20</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=30&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>10</td>
        <td>30</td>
        <td>20</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=20&lt;a&#91;2&#93;=30&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>10</td>
        <td>30</td>
        <td>20</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=40&#92;ge a&#91;3&#93;=20&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=30&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=40&#92;ge a&#91;3&#93;=30&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>40</td>
        <td>30</td>
        <td>20</td>
        <td>10</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td class="cella-blu">10</td>
        <td>30</td>
        <td>20</td>
        <td class="cella-blu">40</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;4&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=10&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td>10</td>
        <td class="cella-blu">20</td>
        <td class="cella-blu">30</td>
        <td>40</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=20&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>10</td>
        <td>20</td>
        <td>30</td>
        <td>40</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=30&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 2 scambi, e l'array ordinato è

        $$
        [10, 20, 30, 40].
        $$

    3. Array $a = [3, 6, 1, 9, 2]$ ($n=5$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;ge a&#91;1&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=1&lt;a&#91;1&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;ge a&#91;3&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=2&#92;ge a&#91;3&#93;=1&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=6&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=3&lt;a&#91;2&#93;=6&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>9</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=2&lt;a&#91;3&#93;=3&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>9</td>
        <td class="cella-blu">6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 2&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=3&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&#92;ge a&#91;3&#93;=3&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=4&#92;)</span> (<span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=6&lt;a&#91;4&#93;=9&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=5&#92;ne 4&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>6</td>
        <td>1</td>
        <td>9</td>
        <td>2</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>3</td>
        <td class="cella-blu">1</td>
        <td>6</td>
        <td class="cella-blu">3</td>
        <td>9</td>
        <td>2</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;3&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..5&#93;)=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>5</td>
        <td>1</td>
        <td class="cella-blu">2</td>
        <td>3</td>
        <td>9</td>
        <td class="cella-blu">6</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..5&#93;)=2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>9</td>
        <td>6</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..5&#93;)=3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>5</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td class="cella-blu">6</td>
        <td class="cella-blu">9</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;4&#93;&#92;leftrightarrow a&#91;5&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;4&#93;=&#92;min(a&#91;4..5&#93;)=6&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 10 confronti tra chiavi e 3 scambi, e l'array ordinato è

        $$
        [1, 2, 3, 6, 9].
        $$

    4. Array $a = [25, 12, 50]$ ($n=3$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=25&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>2</td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=12&lt;a&#91;1&#93;=25&#92;)</span>: <span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=50&#92;ge a&#91;2&#93;=12&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;ne 1&#92;)</span>: scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=25&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=50&#92;ge a&#91;2&#93;=25&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>25</td>
        <td>12</td>
        <td>50</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td class="cella-blu">12</td>
        <td class="cella-blu">25</td>
        <td>50</td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;&#92;leftrightarrow a&#91;2&#93;&#92;)</span>: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..3&#93;)=12&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>12</td>
        <td>25</td>
        <td>50</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..3&#93;)=25&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 3 confronti tra chiavi e 1 scambio, e l'array ordinato è

        $$
        [12, 25, 50].
        $$

    5. Array $a = [17, 17, 17, 17]$ ($n=4$).

        <div class="minipage" style="width:100%" markdown>

        <em>Traccia dettagliata:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=1&#92;)</span> (<span class="arithmatex">&#92;(a&#91;1&#93;=17&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=17&#92;ge a&#91;1&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=17&#92;ge a&#91;1&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=17&#92;ge a&#91;1&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=1&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=2&#92;)</span> (<span class="arithmatex">&#92;(a&#91;2&#93;=17&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=17&#92;ge a&#91;2&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=17&#92;ge a&#91;2&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=2&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}:=3&#92;)</span> (<span class="arithmatex">&#92;(a&#91;3&#93;=17&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=17&#92;ge a&#91;3&#93;=17&#92;)</span>: nessun aggiornamento</td>
        </tr>
        <tr>
        <td></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(&#92;mathit{minIdx}=3&#92;)</span>: nessuno scambio</td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:100%" markdown>

        <em>Array dopo ogni iterazione del ciclo esterno:</em>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;mathit{minIdx}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th>Azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>stato iniziale</td>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;1&#93;=&#92;min(a&#91;1..4&#93;)=17&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;2&#93;=&#92;min(a&#91;2..4&#93;)=17&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>17</td>
        <td>nessuno scambio: <span class="arithmatex">&#92;(a&#91;3&#93;=&#92;min(a&#91;3..4&#93;)=17&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        L'algoritmo esegue 6 confronti tra chiavi e 0 scambi, e l'array ordinato è

        $$
        [17, 17, 17, 17].
        $$
