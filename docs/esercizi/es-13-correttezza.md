---
title: "Esercizi · Correttezza"
---

# Esercizi · Correttezza

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 13** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 13](../analisi-ricorsione/13-correttezza.md) · [:material-file-pdf-box: Eserciziario, volume 4 (PDF)](../pdf/esercizi-4-analisi-ricorsione.pdf)

</div>

Negli esercizi di questo capitolo la correttezza di un ciclo si dimostra con un invariante di ciclo, come nel capitolo «Correttezza», seguendo lo schema seguente.

!!! nota ""

    Un invariante di ciclo è una proprietà delle variabili che è vera ogni volta che viene valutata la condizione del ciclo. Per dimostrare la correttezza del ciclo:

    1. <strong>Inizializzazione</strong>: l'invariante è vero prima della prima iterazione;

    2. <strong>Conservazione</strong>: se l'invariante è vero prima di un'iterazione, è vero prima della successiva;

    3. <strong>Terminazione</strong>: il ciclo termina dopo un numero finito di iterazioni (un numero naturale diminuisce strettamente a ogni iterazione), e l'invariante, insieme alla negazione della condizione del ciclo, fornisce l'output corretto.

    Un sotto-array $a[l..r]$ con $l>r$ è vuoto, e una somma vuota è uguale a $0$. Per mostrare che un algoritmo è <strong>sbagliato</strong> basta un controesempio.

<a id="esercizio-13-1"></a>

!!! esercizio "Esercizio 13.1: Correttezza (E1)"

    Consideriamo il seguente algoritmo, che calcola il valore minimo di un array $a[1..n]$ di $n\ge 1$ numeri naturali.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> FindMinimum</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore minimo dell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMinimum(a, n)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min := a&#91;1&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc1-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(min&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Enunciare un invariante di ciclo per il ciclo while di <code>FindMinimum</code>.

    2. Verificare l'invariante di ciclo sull'array $a=[7,3,9,2,5,2]$, mostrando i valori di $i$ e $min$ ogni volta che viene valutata la condizione alla riga [4](#riga-es-13-correttezza-exc1-c).

    3. Dimostrare la correttezza di <code>FindMinimum</code> (inizializzazione, conservazione, terminazione).

    4. Uno studente sostituisce la riga [2](#riga-es-13-correttezza-exc1-a) con $min := 0$. Mostrare, con un controesempio, che il nuovo algoritmo è sbagliato, e indicare quale proprietà dell'invariante di ciclo non vale.

??? soluzione "Soluzione"

    1. Invariante di ciclo:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [4](#riga-es-13-correttezza-exc1-c),

            $$
            min=\min\{a[1],a[2],\dots,a[i-1]\}.
            $$

    2. For $a=[7,3,9,2,5,2]$ ($n=6$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(min&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1..i-1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;min&#92;{a&#91;1&#93;,&#92;dots,a&#91;i-1&#93;&#92;}&#92;)</span></th>
        </tr>
        <tr>
        <td>2</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(&#91;7&#93;&#92;)</span></td>
        <td>7</td>
        </tr>
        <tr>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#91;7,3&#93;&#92;)</span></td>
        <td>3</td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#91;7,3,9&#93;&#92;)</span></td>
        <td>3</td>
        </tr>
        <tr>
        <td>5</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#91;7,3,9,2&#93;&#92;)</span></td>
        <td>2</td>
        </tr>
        <tr>
        <td>6</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#91;7,3,9,2,5&#93;&#92;)</span></td>
        <td>2</td>
        </tr>
        <tr>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#91;7,3,9,2,5,2&#93;&#92;)</span></td>
        <td>2   (il ciclo termina)</td>
        </tr>
        </table></div>

        L'invariante vale a ogni valutazione, e l'algoritmo restituisce $2$.

    3. Dimostrazione di correttezza.

        - <strong>Inizializzazione.</strong> Prima della prima iterazione $min=a[1]$ e $i=2$. Il sotto-array $a[1..1]$ ha il solo elemento $a[1]$, il cui minimo è $a[1]=min$.

        - <strong>Conservazione.</strong> Supponiamo $min=\min\{a[1],\dots,a[i-1]\}$ e $i\le n$. Se $a[i]<min$, la riga [6](#riga-es-13-correttezza-exc1-e) pone $min\leftarrow a[i]$, che è minore di tutti gli elementi di $a[1..i-1]$; altrimenti $min\le a[i]$ e $min$ non cambia. In entrambi i casi $min=\min\{a[1],\dots,a[i]\}$. La riga [8](#riga-es-13-correttezza-exc1-f) pone $i\leftarrow i+1$, quindi l'invariante vale con il nuovo valore di $i$.

        - <strong>Terminazione.</strong> La variabile $i$ parte da $2\le n+1$ e aumenta di $1$ a ogni iterazione, quindi il ciclo termina dopo $n-1$ iterazioni, quando $i=n+1$. Sostituendo $i=n+1$ nell'invariante:

            $$
            min=\min\{a[1],\dots,a[n]\},
            $$

            che è restituito alla riga [10](#riga-es-13-correttezza-exc1-g). Quindi l'algoritmo è corretto.

    4. Con $min:=0$, consideriamo $a=[3,5]$. Poiché nessun elemento è minore di $0$, la riga [6](#riga-es-13-correttezza-exc1-e) non viene mai eseguita e l'algoritmo restituisce $0$, mentre l'output corretto è $3$. Quindi l'algoritmo è sbagliato.

        La proprietà che non vale è l'<strong>inizializzazione</strong>: prima della prima iterazione $i=2$ e $min=0$, mentre $\min\{a[1]\}=a[1]=3\neq 0$. La conservazione è ancora vera (se l'invariante valesse, continuerebbe a valere), ma poiché è falso all'inizio, l'argomento di terminazione non può essere applicato. In effetti, poiché le componenti sono numeri naturali, l'algoritmo restituisce sempre $\min\{0,a[2],\dots,a[n]\}=0$, che è corretto solo se almeno una componente dell'array è uguale a $0$.

<a id="esercizio-13-2"></a>

!!! esercizio "Esercizio 13.2: Correttezza (E2)"

    Consideriamo il seguente algoritmo.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> ArraySum</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;ge 1&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(s&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ArraySum(a, n)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s := 0&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s &#92;leftarrow s + a&#91;i&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc2-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Che cosa calcola l'algoritmo? Enunciare un invariante di ciclo per il suo ciclo while.

    2. Verificare l'invariante di ciclo sull'array $a=[4,1,7,3]$, mostrando i valori di $i$ e $s$ ogni volta che viene valutata la condizione alla riga [4](#riga-es-13-correttezza-exc2-c).

    3. Dimostrare la correttezza di <code>ArraySum</code>.

    4. Uno studente modifica la riga [3](#riga-es-13-correttezza-exc2-b) in $i:=0$ e la riga [4](#riga-es-13-correttezza-exc2-c) in “<strong>while</strong> $i<n$”, mantenendo $a[i]$ alla riga [5](#riga-es-13-correttezza-exc2-d). Il nuovo algoritmo è corretto?

??? soluzione "Soluzione"

    1. L'algoritmo calcola la somma degli elementi dell'array:

        $$
        s=\sum_{k=1}^{n}a[k].
        $$

        Invariante di ciclo:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [4](#riga-es-13-correttezza-exc2-c),

            $$
            s=\sum_{k=1}^{i-1}a[k],
            $$

            dove una somma vuota ($i=1$) è uguale a $0$.

    2. For $a=[4,1,7,3]$ ($n=4$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(s&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;sum&#95;{k=1}^{i-1}a&#91;k&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>1</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (somma vuota)</td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(4+1=5&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>12</td>
        <td><span class="arithmatex">&#92;(4+1+7=12&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(4+1+7+3=15&#92;)</span>   (il ciclo termina)</td>
        </tr>
        </table></div>

        L'algoritmo restituisce $15$.

    3. Dimostrazione di correttezza.

        - <strong>Inizializzazione.</strong> Prima della prima iterazione $s=0$ e $i=1$; la somma $\sum_{k=1}^{0}a[k]$ è vuota, quindi uguale a $0=s$.

        - <strong>Conservazione.</strong> Supponiamo $s=\sum_{k=1}^{i-1}a[k]$ e $i\le n$. La riga [5](#riga-es-13-correttezza-exc2-d) dà

            $$
            s+a[i]=\sum_{k=1}^{i-1}a[k]+a[i]=\sum_{k=1}^{i}a[k],
            $$

            e la riga [6](#riga-es-13-correttezza-exc2-e) incrementa $i$ di $1$, quindi l'invariante vale con il nuovo valore di $i$.

        - <strong>Terminazione.</strong> La variabile $i$ parte da $1$ e aumenta di $1$ a ogni iterazione, quindi il ciclo termina dopo $n$ iterazioni, quando $i=n+1$. Sostituendo $i=n+1$ nell'invariante si ottiene $s=\sum_{k=1}^{n}a[k]$, che è restituito alla riga [8](#riga-es-13-correttezza-exc2-f). Quindi l'algoritmo è corretto.

    4. No. Con $i:=0$ la prima iterazione accede ad $a[0]$, che non esiste in un array $a[1..n]$; inoltre, la condizione $i<n$ ferma il ciclo quando $i=n$, quindi $a[n]$ non viene mai sommato. In termini di invariante, l'invariante naturale del nuovo ciclo è $s=\sum_{k=0}^{i-1}a[k]$, e alla terminazione ($i=n$) dà $s=\sum_{k=0}^{n-1}a[k]\neq\sum_{k=1}^{n}a[k]$: il passo di terminazione non fornisce la proprietà richiesta. Per esempio, su $a=[4,1,7,3]$ l'elemento $a[4]=3$ non viene mai sommato, quindi anche ignorando l'accesso non valido il risultato non può essere $15$. Questo è un errore tipico che si ottiene mescolando codice con indici da $0$ (come in C++) e pseudocodice con indici da $1$.

<a id="esercizio-13-3"></a>

!!! esercizio "Esercizio 13.3: Correttezza (E3)"

    Consideriamo l'algoritmo <code>SelectionSort</code>, che ordina in modo non decrescente un array $a[1..n]$ di $n\ge 1$ numeri naturali.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> SelectionSort</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array <span class="arithmatex">&#92;(a&#92;)</span> ordinato in modo non decrescente</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> SelectionSort(a, n)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n-1&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(&#92;mathit{minIdx} := i&#92;)</span></span><span class="pc-c">// indice del minimo in <span class="arithmatex">&#92;(a&#91;i..n&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := i+1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;j&#93; &lt; a&#91;&#92;mathit{minIdx}&#93;&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(&#92;mathit{minIdx} &#92;leftarrow j&#92;)</span></span><span class="pc-c">// trovato un nuovo minimo</span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-i"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(&#92;mathit{minIdx} &#92;neq i&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-j"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(&#92;mathit{tmp} &#92;leftarrow a&#91;i&#93;&#92;)</span></span><span class="pc-c">// scambia <span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span> e <span class="arithmatex">&#92;(a&#91;&#92;mathit{minIdx}&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-k"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;i&#93; &#92;leftarrow a&#91;&#92;mathit{minIdx}&#93;&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-l"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;&#92;mathit{minIdx}&#93; &#92;leftarrow &#92;mathit{tmp}&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc3-m"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">18</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">19</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Enunciare un invariante di ciclo per il ciclo while interno (riga [6](#riga-es-13-correttezza-exc3-e)) e dimostrarlo.

    2. Enunciare un invariante di ciclo per il ciclo while esterno (riga [3](#riga-es-13-correttezza-exc3-b)).

    3. Verificare l'invariante del ciclo esterno sull'array $a=[29,10,14,37,13]$.

    4. Dimostrare la correttezza di <code>SelectionSort</code>.

??? soluzione "Soluzione"

    1. Consideriamo un'iterazione del ciclo esterno con un dato valore di $i$. Il ciclo interno non modifica l'array. Il suo invariante è:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [6](#riga-es-13-correttezza-exc3-e), $i\le \mathit{minIdx}\le j-1$ e

            $$
            a[\mathit{minIdx}]=\min\{a[i],a[i+1],\dots,a[j-1]\}.
            $$

        - <strong>Inizializzazione.</strong> Le righe [4](#riga-es-13-correttezza-exc3-c)–[5](#riga-es-13-correttezza-exc3-d) pongono $\mathit{minIdx}=i$ e $j=i+1$: il sotto-array $a[i..j-1]=a[i..i]$ ha il solo elemento $a[i]=a[\mathit{minIdx}]$.

        - <strong>Conservazione.</strong> Supponiamo l'invariante e $j\le n$. Se $a[j]<a[\mathit{minIdx}]$, allora $a[j]$ è minore di tutti gli elementi di $a[i..j-1]$ e la riga [8](#riga-es-13-correttezza-exc3-g) pone $\mathit{minIdx}\leftarrow j$; altrimenti $a[\mathit{minIdx}]\le a[j]$. In entrambi i casi $a[\mathit{minIdx}]=\min\{a[i],\dots,a[j]\}$ e $i\le\mathit{minIdx}\le j$. La riga [10](#riga-es-13-correttezza-exc3-h) pone $j\leftarrow j+1$, quindi l'invariante vale con il nuovo $j$.

        - <strong>Terminazione.</strong> $j$ aumenta di $1$ a partire da $i+1\le n$, quindi il ciclo si ferma quando $j=n+1$. Allora $a[\mathit{minIdx}]=\min\{a[i],\dots,a[n]\}$: $\mathit{minIdx}$ è l'indice di un elemento minimo di $a[i..n]$.

    2. Invariante del ciclo esterno:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [3](#riga-es-13-correttezza-exc3-b):

            - **(P1)** l'array $a[1..n]$ contiene gli elementi originali (è un riordinamento dell'input);

            - **(P2)** il sotto-array $a[1..i-1]$ è ordinato in modo non decrescente;

            - **(P3)** ogni elemento di $a[1..i-1]$ è $\le$ ogni elemento di $a[i..n]$.

    3. Per $a=[29,10,14,37,13]$ ($n=5$); il prefisso ordinato $a[1..i-1]$ è evidenziato in <mark style="background:color-mix(in srgb, #1971c2 30%, transparent);color:inherit">blu</mark>:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;4&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;5&#93;&#92;)</span></th>
        <th>minimo di <span class="arithmatex">&#92;(a&#91;i..n&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>1</td>
        <td>29</td>
        <td>10</td>
        <td>14</td>
        <td>37</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=10&#92;)</span>: scambio di <span class="arithmatex">&#92;(a&#91;1&#93;,a&#91;2&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td class="cella-blu">10</td>
        <td>29</td>
        <td>14</td>
        <td>37</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=13&#92;)</span>: scambio di <span class="arithmatex">&#92;(a&#91;2&#93;,a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">13</td>
        <td>14</td>
        <td>37</td>
        <td>29</td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=14&#92;)</span>: nessuno scambio</td>
        </tr>
        <tr>
        <td>4</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">13</td>
        <td class="cella-blu">14</td>
        <td>37</td>
        <td>29</td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=29&#92;)</span>: scambio di <span class="arithmatex">&#92;(a&#91;4&#93;,a&#91;5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td class="cella-blu">10</td>
        <td class="cella-blu">13</td>
        <td class="cella-blu">14</td>
        <td class="cella-blu">29</td>
        <td>37</td>
        <td>il ciclo termina (<span class="arithmatex">&#92;(i=n&#92;)</span>)</td>
        </tr>
        </table></div>

        A ogni riga il prefisso blu è ordinato, e ogni elemento blu è $\le$ ogni elemento non blu: per esempio, per $i=4$, $\max\{10,13,14\}=14\le\min\{37,29\}=29$.

    4. Dimostrazione di correttezza.

        - <strong>Inizializzazione.</strong> Prima della prima iterazione $i=1$ e nulla è stato modificato: (P1) vale, e $a[1..0]$ è vuoto, quindi (P2) e (P3) valgono banalmente.

        - <strong>Conservazione.</strong> Supponiamo (P1)–(P3) e $i\le n-1$. Per il punto 1, dopo il ciclo interno

            $$
            a[\mathit{minIdx}]=\min\{a[i],\dots,a[n]\}.
            $$

            Le righe [12](#riga-es-13-correttezza-exc3-i)–[15](#riga-es-13-correttezza-exc3-l) scambiano $a[i]$ e $a[\mathit{minIdx}]$ (se sono posizioni diverse). Uno scambio si limita a scambiare due elementi, quindi (P1) vale ancora. Ora $a[i]$ è il minimo di $a[i..n]$, quindi:

            - per (P3), $a[i]\ge$ ogni elemento di $a[1..i-1]$, e poiché $a[1..i-1]$ è ordinato (P2), $a[1..i]$ è ordinato;

            - $a[i]\le$ ogni elemento di $a[i+1..n]$, perché $a[i]$ è il minimo di $a[i..n]$ e lo scambio riordina solo i valori nelle posizioni $i..n$; per lo stesso motivo, per (P3) ogni elemento di $a[1..i-1]$ è $\le$ ogni elemento di $a[i+1..n]$. Quindi ogni elemento di $a[1..i]$ è $\le$ ogni elemento di $a[i+1..n]$.

            La riga [17](#riga-es-13-correttezza-exc3-m) pone $i\leftarrow i+1$, quindi (P1)–(P3) valgono con il nuovo valore di $i$.

        - <strong>Terminazione.</strong> Il ciclo interno termina sempre (punto 1), e $i$ aumenta di $1$ a partire da $1$; il ciclo esterno si ferma quando $i=n$ per la prima volta (dopo $n-1$ iterazioni; se $n=1$ non viene mai eseguito e $i=1=n$). Sostituendo $i=n$: $a[1..n-1]$ è ordinato (P2) e ogni elemento di $a[1..n-1]$ è $\le a[n]$ (P3); quindi l'intero array $a[1..n]$ è ordinato e, per (P1), contiene gli elementi originali. Quindi l'algoritmo è corretto.

        Notiamo che il ciclo esterno richiede solo $n-1$ iterazioni: quando le prime $n-1$ posizioni sono corrette, l'ultimo elemento è automaticamente nella sua posizione corretta.

<a id="esercizio-13-4"></a>

!!! esercizio "Esercizio 13.4: Correttezza (E4)"

    Consideriamo l'algoritmo <code>LinearSearch</code>, che determina se un valore $m$ è uno degli elementi di un array $a[1..n]$ di $n$ numeri naturali (non necessariamente ordinato).

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> LinearSearch</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali e un valore <span class="arithmatex">&#92;(m&#92;)</span> da cercare</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Indice di <span class="arithmatex">&#92;(m&#92;)</span> in <span class="arithmatex">&#92;(a&#92;)</span>, oppure <span class="arithmatex">&#92;(-1&#92;)</span> se non trovato</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> LinearSearch(a, n, m)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(i&#92;)</span></span><span class="pc-c">// Elemento trovato all'indice <span class="arithmatex">&#92;(i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc4-f"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(-1&#92;)</span></span><span class="pc-c">// Elemento non trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Enunciare un invariante di ciclo per il ciclo while di <code>LinearSearch</code>.

    2. Verificare l'invariante di ciclo sull'array $a=[8,3,6,3,9]$ per $m=6$ e per $m=5$.

    3. Dimostrare che <code>LinearSearch</code> è corretto. Dimostrare anche che, quando $m$ è nell'array, l'indice restituito è il <strong>più piccolo</strong> indice $k$ tale che $a[k]=m$.

    4. Uno studente scambia le righe [4](#riga-es-13-correttezza-exc4-c)–[5](#riga-es-13-correttezza-exc4-d) e la riga [7](#riga-es-13-correttezza-exc4-e), cioè il corpo del ciclo prima incrementa $i$ e poi controlla se $a[i]=m$. Trovare un controesempio che mostri che il nuovo algoritmo è sbagliato, e indicare quale proprietà dell'invariante di ciclo non vale.

??? soluzione "Soluzione"

    1. Invariante di ciclo:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [3](#riga-es-13-correttezza-exc4-b), $1\le i\le n+1$ e $m$ <strong>non</strong> è nel sotto-array $a[1..i-1]$:

            $$
            a[k]\neq m\qquad \text{per ogni } k\in\{1, 2, \dots, i-1\}.
            $$

    2. Per $a=[8,3,6,3,9]$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(m&#92;)</span></th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;1..i-1&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td>6</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#91;&#92; &#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=8&#92;neq 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#91;8&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;neq 6&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#91;8,3&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6=m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> restituisce <span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(&#91;&#92; &#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93;=8&#92;neq 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#91;8&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;2&#93;=3&#92;neq 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(&#91;8,3&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;3&#93;=6&#92;neq 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#91;8,3,6&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;4&#93;=3&#92;neq 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(&#91;8,3,6,3&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(a&#91;5&#93;=9&#92;neq 5&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(&#91;8,3,6,3,9&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i&gt;n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> restituisce <span class="arithmatex">&#92;(-1&#92;)</span></td>
        </tr>
        </table></div>

        A ogni valutazione, $m$ non compare in $a[1..i-1]$.

    3. Dimostrazione di correttezza.

        - <strong>Inizializzazione.</strong> Prima della prima iterazione $i=1$ e $a[1..0]$ è vuoto, quindi non contiene $m$.

        - <strong>Conservazione.</strong> Supponiamo l'invariante e $i\le n$. Se $a[i]=m$, l'algoritmo restituisce $i$ (riga [5](#riga-es-13-correttezza-exc4-d)), che è un output corretto. Altrimenti $a[i]\neq m$, quindi $m$ non è in $a[1..i]$; la riga [7](#riga-es-13-correttezza-exc4-e) pone $i\leftarrow i+1$ e l'invariante vale con il nuovo valore di $i$.

        - <strong>Terminazione.</strong> $i$ aumenta di $1$ a partire da $1$, quindi il ciclo esegue al più $n$ iterazioni. L'algoritmo finisce in uno di due modi:

            - restituisce $i$ con $a[i]=m$: corretto. Inoltre, per l'invariante $a[k]\neq m$ per ogni $k<i$, quindi $i$ è il più piccolo indice con $a[i]=m$;

            - la condizione alla riga [3](#riga-es-13-correttezza-exc4-b) è falsa, cioè $i=n+1$: per l'invariante $m$ non è in $a[1..n]$, e l'algoritmo restituisce correttamente $-1$.

            Quindi l'algoritmo è corretto.

    4. Il nuovo corpo è: $i\leftarrow i+1$; <strong>if</strong> $a[i]=m$ <strong>then return</strong> $i$. Consideriamo $a=[6,3]$ e $m=6$. Nella prima iterazione $i$ diventa $2$ e $a[2]=3\neq 6$; nella seconda iterazione $i$ diventa $3$ e l'algoritmo accede ad $a[3]$, che è fuori dall'array; in ogni caso $a[1]=6$ non viene <strong>mai</strong> controllato, quindi l'algoritmo non può restituire $1$.

        La proprietà che non vale è la <strong>conservazione</strong>: se $m$ non è in $a[1..i-1]$ all'inizio dell'iterazione, dopo il corpo sappiamo solo che $m$ non è in $a[1..i-1]$ e che $a[i+1]\neq m$, ma non sappiamo nulla su $a[i]$. Con il nuovo valore $i+1$, l'invariante richiederebbe che $m$ non sia in $a[1..i]$, cosa che non è garantita: nell'esempio, prima della seconda valutazione della condizione $i=2$ e $a[1]=6=m$.

<a id="esercizio-13-5"></a>

!!! esercizio "Esercizio 13.5: Correttezza (E5)"

    Consideriamo i due algoritmi seguenti, che dovrebbero calcolare $x^n$ per due numeri naturali $x\ge 1$ e $n\ge 0$ (ricordiamo che $x^0=1$).

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> Power</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(x&#92;ge 1&#92;)</span> e <span class="arithmatex">&#92;(n&#92;ge 0&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(x^n&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Power(x, n)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p &#92;leftarrow p &#92;cdot x&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(p&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> WrongPower</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(x&#92;ge 1&#92;)</span> e <span class="arithmatex">&#92;(n&#92;ge 0&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(x^n&#92;)</span> (?)</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> WrongPower(x, n)</span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p := x&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p &#92;leftarrow p &#92;cdot x&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-13-correttezza-exc5w-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(p&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Enunciare un invariante di ciclo per il ciclo while di <code>Power</code> e verificarlo per $x=3$, $n=4$.

    2. Dimostrare la correttezza di <code>Power</code>, incluso il caso $n=0$.

    3. Mostrare che lo stesso invariante <strong>non</strong> è un invariante di ciclo di <code>WrongPower</code>: quale delle tre proprietà non vale? Dare un controesempio che mostri che <code>WrongPower</code> è sbagliato, con una traccia per $x=2$, $n=3$.

    4. Trovare l'invariante di ciclo corretto di <code>WrongPower</code> e usarlo per determinare esattamente che cosa calcola <code>WrongPower</code>. Per quali input il suo output è corretto?

??? soluzione "Soluzione"

    1. Invariante di ciclo di <code>Power</code>:

        !!! chiave ""

            Ogni volta che viene valutata la condizione alla riga [4](#riga-es-13-correttezza-exc5-c), $1\le i\le n+1$ e

            $$
            p=x^{\,i-1}.
            $$

        Per $x=3$, $n=4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(p&#92;)</span></th>
        <th><span class="arithmatex">&#92;(x^{i-1}&#92;)</span></th>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(3^0=1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(3^1=3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(3^2=9&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(3^3=27&#92;)</span></td>
        </tr>
        <tr>
        <td>5</td>
        <td>81</td>
        <td><span class="arithmatex">&#92;(3^4=81&#92;)</span>   (il ciclo termina)</td>
        </tr>
        </table></div>

        L'algoritmo restituisce $81=3^4$.

    2. Dimostrazione di correttezza di <code>Power</code>.

        - <strong>Inizializzazione.</strong> Prima della prima iterazione $p=1$ e $i=1$, quindi $p=x^0=x^{i-1}$; inoltre $1\le i\le n+1$ poiché $n\ge 0$.

        - <strong>Conservazione.</strong> Supponiamo $p=x^{i-1}$ e $i\le n$. La riga [5](#riga-es-13-correttezza-exc5-d) dà $p\cdot x=x^{i-1}\cdot x=x^{i}$, e la riga [6](#riga-es-13-correttezza-exc5-e) pone $i\leftarrow i+1\le n+1$. Con il nuovo valore di $i$, $p=x^{i-1}$.

        - <strong>Terminazione.</strong> $i$ aumenta di $1$ a partire da $1\le n+1$, quindi il ciclo termina dopo esattamente $n$ iterazioni, quando $i=n+1$. Sostituendo $i=n+1$: $p=x^{n}$, che è restituito alla riga [8](#riga-es-13-correttezza-exc5-f).

        Se $n=0$, la condizione $1\le 0$ è falsa alla prima valutazione, il ciclo non viene mai eseguito e l'algoritmo restituisce $p=1=x^0$, in accordo con la dimostrazione (inizializzazione e terminazione coincidono, con $i=1=n+1$).

    3. Per <code>WrongPower</code>, l'<strong>inizializzazione</strong> non vale: prima della prima iterazione $i=1$ e $p=x$, mentre $x^{i-1}=x^0=1$. Quindi $p\neq x^{i-1}$ ogni volta che $x\ge 2$. (La conservazione è ancora vera: se valesse $p=x^{i-1}$, il corpo la preserverebbe; ma l'“induzione” non ha un caso base valido.)

        Controesempio: $x=2$, $n=3$, per cui $x^n=8$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(p&#92;)</span></th>
        <th><span class="arithmatex">&#92;(x^{i-1}&#92;)</span></th>
        <th><span class="arithmatex">&#92;(x^{i}&#92;)</span></th>
        </tr>
        <tr>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        </tr>
        <tr>
        <td>2</td>
        <td>4</td>
        <td>2</td>
        <td>4</td>
        </tr>
        <tr>
        <td>3</td>
        <td>8</td>
        <td>4</td>
        <td>8</td>
        </tr>
        <tr>
        <td>4</td>
        <td>16</td>
        <td>8</td>
        <td>16   (il ciclo termina)</td>
        </tr>
        </table></div>

        <code>WrongPower</code> restituisce $16\neq 8=2^3$, quindi è sbagliato.

    4. La tabella suggerisce l'invariante $p=x^{\,i}$, che è un invariante di ciclo corretto di <code>WrongPower</code>:

        - <strong>Inizializzazione:</strong> $p=x=x^1=x^i$ con $i=1$;

        - <strong>Conservazione:</strong> se $p=x^i$ e $i\le n$, dopo il corpo $p=x^{i+1}$ e $i$ è incrementato di $1$;

        - <strong>Terminazione:</strong> il ciclo termina con $i=n+1$, quindi $p=x^{n+1}$.

        Quindi <code>WrongPower</code> calcola $x^{n+1}$. Il suo output è corretto, cioè $x^{n+1}=x^n$, se e solo se $x^n(x-1)=0$, ovvero (poiché $x\ge 1$) se e solo se $x=1$. Per ogni $x\ge 2$ e ogni $n\ge 0$ è sbagliato: basta un controesempio per mostrare che un algoritmo non è corretto.
