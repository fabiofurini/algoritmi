---
title: "Esercizi · Ricorsione"
---

# Esercizi · Ricorsione

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 14** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 14](../analisi-ricorsione/14-ricorsione.md) · [:material-file-pdf-box: Eserciziario, volume 4 (PDF)](../pdf/esercizi-4-analisi-ricorsione.pdf)

</div>

Negli esercizi di questo capitolo i passi di un algoritmo ricorsivo si contano con le convenzioni dei capitoli «Tempo di esecuzione» e «Ricorsione», e le equazioni di ricorrenza si risolvono per semplice srotolamento.

!!! nota ""

    - Ogni esecuzione di una riga numerata di pseudocodice è <strong>un passo</strong>; una riga che contiene una chiamata ricorsiva conta come un passo <strong>più</strong> tutti i passi eseguiti da quella chiamata.

    - $C(n)$ indica il numero di <strong>chiamate</strong> (nodi dell'albero delle chiamate ricorsive) e $S(n)$ il numero di <strong>passi</strong>; la <strong>profondità della ricorsione</strong> è il massimo numero di nodi su un cammino dalla radice a una foglia dell'albero, cioè il massimo numero di stack frame simultaneamente in memoria.

    - <strong>Induzione forte</strong>: se $P(n_0)$ è vera e, per ogni $n>n_0$, la verità di $P(k)$ per ogni $k$ con $n_0\le k<n$ implica la verità di $P(n)$, allora $P(n)$ è vera per ogni $n\ge n_0$.

    - <strong>Srotolamento</strong> di un'equazione di ricorrenza $S(n)=S(n-1)+c$ con $c$ costante:

        $$
        S(n)=S(n-1)+c=S(n-2)+2c=\cdots=S(n-k)+k\,c,
        $$

        e il caso base si raggiunge per il valore di $k$ che rende $n-k$ un caso base.

<a id="esercizio-14-1"></a>

!!! esercizio "Esercizio 14.1: Ricorsione (E1)"

    Si consideri il seguente algoritmo ricorsivo.

    !!! algoritmo "Algoritmo: Mystery"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Mystery(n)</span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecone-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 1&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecone-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecone-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> Mystery<span class="arithmatex">&#92;((&#92;lfloor n/2 &#92;rfloor)&#92;)</span> <span class="arithmatex">&#92;(+&#92;)</span> Mystery<span class="arithmatex">&#92;((&#92;lceil n/2 &#92;rceil)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Disegnare l'albero delle chiamate ricorsive di <code>Mystery</code>$(6)$, scrivendo accanto a ogni chiamata il valore che restituisce.

    2. Che cosa calcola l'algoritmo? Dimostrare l'affermazione per induzione forte su $n$.

    3. Sia $C(n)$ il numero di chiamate eseguite da <code>Mystery</code>$(n)$. Scrivere un'equazione di ricorrenza per $C(n)$ e dimostrare che $C(n) = 2n - 1$ per ogni $n \ge 1$. Verificare la formula sull'albero della domanda 1.

    4. Qual è la profondità della ricorsione di <code>Mystery</code>$(6)$, cioè il massimo numero di stack frame simultaneamente in memoria?

??? soluzione "Soluzione"

    1. Si ha $\lfloor 6/2 \rfloor = \lceil 6/2 \rceil = 3$, $\lfloor 3/2 \rfloor = 1$, $\lceil 3/2 \rceil = 2$ e $\lfloor 2/2 \rfloor = \lceil 2/2 \rceil = 1$. L'albero delle chiamate ricorsive (valori restituiti in rosso) è:

        ![Figura 1](../img/es-14-ricorsione/fig01.svg){ .fig loading=lazy  }

        <code>Mystery</code>$(2)$ restituisce $1+1 = 2$, <code>Mystery</code>$(3)$ restituisce $1 + 2 = 3$ e <code>Mystery</code>$(6)$ restituisce $3 + 3 = 6$.

    2. L'algoritmo restituisce $n$ stesso (calcola $n$ come somma di $n$ uni). 

        <strong>Dimostrazione</strong> per induzione forte su $n \ge 1$.

        - <strong>Caso base</strong> ($n=1$): l'algoritmo restituisce $1$ alla riga [3](#riga-es-14-ricorsione-exrecone-b).

        - <strong>Passo induttivo</strong> ($n \ge 2$): supponiamo che <code>Mystery</code>$(k)$ restituisca $k$ per ogni $1 \le k < n$. Per $n \ge 2$ si ha $1 \le \lfloor n/2 \rfloor \le \lceil n/2 \rceil < n$, quindi per ipotesi induttiva la riga [5](#riga-es-14-ricorsione-exrecone-c) restituisce

            $$
            \lfloor n/2 \rfloor + \lceil n/2 \rceil = n.
            $$

        L'induzione forte è necessaria perché le chiamate ricorsive sono su $\lfloor n/2 \rfloor$ e $\lceil n/2 \rceil$, non su $n-1$.

    3. Ogni chiamata con $n \ge 2$ effettua due chiamate ricorsive, quindi

        $$
        C(n) =
        \begin{cases}
        1 & \text{se } n = 1 \\
        1 + C(\lfloor n/2 \rfloor) + C(\lceil n/2 \rceil) & \text{se } n \ge 2
        \end{cases}
        $$

        <strong>Dimostrazione</strong> di $C(n) = 2n - 1$ per induzione forte su $n$.

        - <strong>Caso base</strong> ($n=1$): $C(1) = 1 = 2 \cdot 1 - 1$.

        - <strong>Passo induttivo</strong> ($n \ge 2$): per ipotesi induttiva,

            $$
            C(n) = 1 + \big(2\lfloor n/2 \rfloor - 1\big) + \big(2\lceil n/2 \rceil - 1\big) = 2\big(\lfloor n/2 \rfloor + \lceil n/2 \rceil\big) - 1 = 2n - 1.
            $$

        Per $n = 6$: $C(6) = 11$, e infatti l'albero della domanda 1 ha $11$ nodi. (L'albero ha $n = 6$ foglie, una per ciascun $1$ della somma, e $n - 1 = 5$ nodi interni, uno per ciascuna addizione.)

    4. I cammini più lunghi dalla radice a una foglia sono, per esempio, <code>Mystery</code>$(6)$, <code>Mystery</code>$(3)$, <code>Mystery</code>$(2)$, <code>Mystery</code>$(1)$. Quindi la profondità della ricorsione è $4$: al più $4$ stack frame sono simultaneamente in memoria, benché vengano eseguite $11$ chiamate. (In generale la profondità è $\lceil \log_2 n \rceil + 1$.)

<a id="esercizio-14-2"></a>

!!! esercizio "Esercizio 14.2: Ricorsione (E2)"

    Dato un array $a[1..n]$ di $n$ numeri interi, si considerino i problemi di calcolare

    - la <strong>somma</strong> $a[1] + a[2] + \dots + a[n]$ (uguale a $0$ se $n = 0$);

    - il valore <strong>massimo</strong> $\max\{a[1], a[2], \dots, a[n]\}$ (per $n \ge 1$).

    Per le domande numeriche si usi l'array $a = [3, 8, 1, 6]$.

    **Domande**

    1. Scrivere un algoritmo ricorsivo <code>RecSum</code>$(a, n)$ che calcola la somma di $a[1..n]$ riducendo il problema al sotto-array $a[1..n-1]$ (decremento di uno).

    2. Scrivere un algoritmo ricorsivo <code>RecMax</code>$(a, n)$ che calcola il massimo di $a[1..n]$ riducendo il problema al sotto-array $a[1..n-1]$.

    3. Mostrare la sequenza di chiamate e di ritorni di <code>RecSum</code>$(a, 4)$ e di <code>RecMax</code>$(a, 4)$ per $a = [3, 8, 1, 6]$.

    4. Dimostrare la correttezza di <code>RecMax</code> per induzione su $n$.

    5. Scrivere le equazioni di ricorrenza del numero di passi $S(n)$ dei due algoritmi, risolverle per srotolamento e indicare la profondità della ricorsione.

??? soluzione "Soluzione"

    1. La somma di $a[1..n]$ è la somma di $a[1..n-1]$ più $a[n]$, e la somma di un array vuoto è $0$:

        !!! algoritmo "Algoritmo: RecSum"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 0&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>La somma <span class="arithmatex">&#92;(a&#91;1&#93; + &#92;dots + a&#91;n&#93;&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> RecSum(a, n)</span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 0&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> RecSum<span class="arithmatex">&#92;((a, n-1) + a&#91;n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

    2. Il massimo di $a[1..n]$ è il maggiore tra il massimo di $a[1..n-1]$ e $a[n]$; il massimo di un singolo elemento $a[1]$ è $a[1]$:

        !!! algoritmo "Algoritmo: RecMax"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore massimo in <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> RecMax(a, n)</span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-d"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 1&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-e"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(a&#91;1&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-f"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m :=&#92;)</span> RecMax<span class="arithmatex">&#92;((a, n-1)&#92;)</span></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-g"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;n&#93; &gt; m&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-h"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(a&#91;n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga" id="riga-es-14-ricorsione-exrectwo-i"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(m&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

    3. Per $a = [3, 8, 1, 6]$:

        <strong>RecSum</strong>$(a,4)$: chiamate

        $$
        \texttt{RecSum}(a,4) \to \texttt{RecSum}(a,3) \to \texttt{RecSum}(a,2) \to \texttt{RecSum}(a,1) \to \texttt{RecSum}(a,0),
        $$

        poi i ritorni:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th>restituisce</th>
        </tr>
        <tr>
        <td><code>RecSum</code><span class="arithmatex">&#92;((a,0)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (caso base)</td>
        </tr>
        <tr>
        <td><code>RecSum</code><span class="arithmatex">&#92;((a,1)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0 + a&#91;1&#93; = 0 + 3 = 3&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecSum</code><span class="arithmatex">&#92;((a,2)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 + a&#91;2&#93; = 3 + 8 = 11&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecSum</code><span class="arithmatex">&#92;((a,3)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11 + a&#91;3&#93; = 11 + 1 = 12&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecSum</code><span class="arithmatex">&#92;((a,4)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 + a&#91;4&#93; = 12 + 6 = 18&#92;)</span></td>
        </tr>
        </table></div>

        <strong>RecMax</strong>$(a,4)$: chiamate <code>RecMax</code>$(a,4) \to$ <code>RecMax</code>$(a,3) \to$ <code>RecMax</code>$(a,2) \to$ <code>RecMax</code>$(a,1)$, poi i ritorni:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th>confronto</th>
        <th>restituisce</th>
        </tr>
        <tr>
        <td><code>RecMax</code><span class="arithmatex">&#92;((a,1)&#92;)</span></td>
        <td>– (caso base)</td>
        <td><span class="arithmatex">&#92;(a&#91;1&#93; = 3&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecMax</code><span class="arithmatex">&#92;((a,2)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(m = 3&#92;)</span>, <span class="arithmatex">&#92;(a&#91;2&#93; = 8 &gt; 3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecMax</code><span class="arithmatex">&#92;((a,3)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(m = 8&#92;)</span>, <span class="arithmatex">&#92;(a&#91;3&#93; = 1 &#92;le 8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        <tr>
        <td><code>RecMax</code><span class="arithmatex">&#92;((a,4)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(m = 8&#92;)</span>, <span class="arithmatex">&#92;(a&#91;4&#93; = 6 &#92;le 8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        </table></div>

        La somma è $18$ e il massimo è $8$.

    4. <strong>Affermazione</strong>: per ogni $n \ge 1$, <code>RecMax</code>$(a,n)$ restituisce $\max\{a[1], \dots, a[n]\}$.

        - <strong>Caso base</strong> ($n=1$): l'algoritmo restituisce $a[1] = \max\{a[1]\}$ alla riga [3](#riga-es-14-ricorsione-exrectwo-e).

        - <strong>Passo induttivo</strong> ($n \ge 2$): per ipotesi induttiva, la riga [5](#riga-es-14-ricorsione-exrectwo-f) assegna

            $$
            m = \max\{a[1],\dots,a[n-1]\}.
            $$

            Se $a[n] > m$, allora $a[n]$ è maggiore di tutti gli elementi di $a[1..n-1]$ e l'algoritmo restituisce $a[n] = \max\{a[1],\dots,a[n]\}$ (riga [7](#riga-es-14-ricorsione-exrectwo-h)). Altrimenti $a[n] \le m$ e l'algoritmo restituisce $m = \max\{a[1],\dots,a[n]\}$ (riga [9](#riga-es-14-ricorsione-exrectwo-i)).

    5. <strong>RecSum.</strong> $S(0) = 2$ (righe [2](#riga-es-14-ricorsione-exrectwo-a)–[3](#riga-es-14-ricorsione-exrectwo-b)) e, per $n \ge 1$, le righe [2](#riga-es-14-ricorsione-exrectwo-a) e [5](#riga-es-14-ricorsione-exrectwo-c) più la chiamata ricorsiva:

        $$
        S(n) = S(n-1) + 2 = S(n-2) + 2 \cdot 2 = \dots = S(0) + 2n = 2n + 2 = \Theta(n).
        $$

        <strong>RecMax.</strong> $S(1) = 2$ (righe [2](#riga-es-14-ricorsione-exrectwo-d)–[3](#riga-es-14-ricorsione-exrectwo-e)) e, per $n \ge 2$, le righe [2](#riga-es-14-ricorsione-exrectwo-d), [5](#riga-es-14-ricorsione-exrectwo-f), [6](#riga-es-14-ricorsione-exrectwo-g) e una delle righe [7](#riga-es-14-ricorsione-exrectwo-h), [9](#riga-es-14-ricorsione-exrectwo-i), più la chiamata ricorsiva:

        $$
        S(n) = S(n-1) + 4 = S(n-2) + 2 \cdot 4 = \dots = S(1) + 4(n-1) = 4n - 2 = \Theta(n).
        $$

        Per $n = 4$: $S(4) = 10$ per <code>RecSum</code> e $S(4) = 14$ per <code>RecMax</code>.

        La profondità della ricorsione è $n+1$ per <code>RecSum</code> (chiamate su $n, n-1, \dots, 0$) e $n$ per <code>RecMax</code> (chiamate su $n, \dots, 1$): entrambi usano una memoria $\Theta(n)$ per il call stack, mentre le versioni iterative (come <code>FindMaximum</code> nel capitolo «Tempo di esecuzione») usano memoria costante.

        !!! chiave ""

            Se tutti gli elementi usano un numero costante di bit ($|I| = \Theta(n)$), il tempo di esecuzione nel caso peggiore sia di <code>RecSum</code> sia di <code>RecMax</code> è $T(|I|) = \Theta(|I|)$.

<a id="esercizio-14-3"></a>

!!! esercizio "Esercizio 14.3: Ricorsione (E3)"

    Un array $a[1..n]$ è un <strong>palindromo</strong> se si legge allo stesso modo da sinistra a destra e da destra a sinistra, cioè $a[i] = a[n+1-i]$ per ogni $i \in \{1, 2, \dots, n\}$. Si consideri il seguente algoritmo ricorsivo, chiamato sull'intero array come <code>IsPalindrome</code>$(a, 1, n)$.

    !!! algoritmo "Algoritmo: IsPalindrome"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#92;)</span> e due indici <span class="arithmatex">&#92;(l, r&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span><strong>true</strong> se il sotto-array <span class="arithmatex">&#92;(a&#91;l..r&#93;&#92;)</span> è un palindromo, <strong>false</strong> altrimenti</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> IsPalindrome(a, l, r)</span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecthree-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(l &#92;ge r&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecthree-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>true</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecthree-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;l&#93; &#92;ne a&#91;r&#93;&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecthree-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>false</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-14-ricorsione-exrecthree-e"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> IsPalindrome<span class="arithmatex">&#92;((a, l+1, r-1)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Mostrare la sequenza di chiamate di <code>IsPalindrome</code>$(a,1,5)$ per gli array $a = [1, 2, 3, 2, 1]$ e $a = [1, 2, 3, 3, 1]$.

    2. Dimostrare per induzione sulla lunghezza $k = r - l + 1$ del sotto-array che l'algoritmo è corretto.

    3. Determinare il numero di passi $S(n)$ nel caso peggiore di <code>IsPalindrome</code>$(a,1,n)$ e la sua profondità di ricorsione.

    4. L'algoritmo è ricorsivo in coda? In caso affermativo, scrivere l'algoritmo iterativo equivalente.

    5. Scrivere un algoritmo ricorsivo <code>Reverse</code>$(a, l, r)$ che inverte sul posto il sotto-array $a[l..r]$, e mostrarne l'esecuzione su $a = [5, 7, 2, 9, 4, 6]$ con $l = 1$, $r = 6$.

??? soluzione "Soluzione"

    1. Per $a = [1, 2, 3, 2, 1]$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th><span class="arithmatex">&#92;(a&#91;l&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;r&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><code>IsPalindrome</code><span class="arithmatex">&#92;((a,1,5)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>uguali <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> richiama <code>IsPalindrome</code><span class="arithmatex">&#92;((a,2,4)&#92;)</span></td>
        </tr>
        <tr>
        <td><code>IsPalindrome</code><span class="arithmatex">&#92;((a,2,4)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>uguali <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> richiama <code>IsPalindrome</code><span class="arithmatex">&#92;((a,3,3)&#92;)</span></td>
        </tr>
        <tr>
        <td><code>IsPalindrome</code><span class="arithmatex">&#92;((a,3,3)&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(l &#92;ge r&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> restituisce <strong>true</strong></td>
        </tr>
        </table></div>

        Il valore <strong>true</strong> viene restituito invariato da tutte le chiamate ($3$ chiamate).

        Per $a = [1, 2, 3, 3, 1]$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th><span class="arithmatex">&#92;(a&#91;l&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;r&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><code>IsPalindrome</code><span class="arithmatex">&#92;((a,1,5)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>uguali <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> richiama <code>IsPalindrome</code><span class="arithmatex">&#92;((a,2,4)&#92;)</span></td>
        </tr>
        <tr>
        <td><code>IsPalindrome</code><span class="arithmatex">&#92;((a,2,4)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>diversi <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> restituisce <strong>false</strong></td>
        </tr>
        </table></div>

        Viene restituito il valore <strong>false</strong> ($2$ chiamate).

    2. Sia $k = r - l + 1$ la lunghezza di $a[l..r]$ ($k \le 0$ significa sotto-array vuoto). Dimostriamo per induzione forte su $k$ che l'algoritmo restituisce <strong>true</strong> se e solo se $a[l..r]$ è un palindromo.

        - <strong>Casi base</strong> ($k \le 1$, cioè $l \ge r$): un array vuoto o con un solo elemento è un palindromo, e l'algoritmo restituisce <strong>true</strong> alla riga [3](#riga-es-14-ricorsione-exrecthree-b).

        - <strong>Passo induttivo</strong> ($k \ge 2$): $a[l..r]$ è un palindromo se e solo se $a[l] = a[r]$ <strong>e</strong> il sotto-array interno $a[l+1..r-1]$ è un palindromo. Se $a[l] \ne a[r]$, l'algoritmo restituisce correttamente <strong>false</strong> (riga [6](#riga-es-14-ricorsione-exrecthree-d)). Altrimenti restituisce il risultato della chiamata su $a[l+1..r-1]$, la cui lunghezza è $k-2 < k$; per ipotesi induttiva, questo risultato è <strong>true</strong> se e solo se $a[l+1..r-1]$ è un palindromo, quindi se e solo se $a[l..r]$ è un palindromo.

        La lunghezza diminuisce di $2$ a ogni chiamata, ed è per questo che sia $k=0$ sia $k=1$ devono essere casi base.

    3. Il caso peggiore si ha quando l'array è un palindromo (la ricorsione non viene mai fermata alla riga [6](#riga-es-14-ricorsione-exrecthree-d)). Ogni chiamata con $l < r$ esegue le righe [2](#riga-es-14-ricorsione-exrecthree-a), [5](#riga-es-14-ricorsione-exrecthree-c) e [8](#riga-es-14-ricorsione-exrecthree-e) ($3$ passi), e l'ultima chiamata esegue le righe [2](#riga-es-14-ricorsione-exrecthree-a)–[3](#riga-es-14-ricorsione-exrecthree-b) ($2$ passi). In funzione della lunghezza $k$:

        $$
        S(k) = S(k-2) + 3 \quad (k \ge 2), \qquad S(0) = S(1) = 2.
        $$

        Srotolando, dopo $\lfloor k/2 \rfloor$ passaggi si raggiunge $S(0)$ oppure $S(1)$:

        $$
        S(n) = 3\lfloor n/2 \rfloor + 2 = \Theta(n).
        $$

        L'algoritmo effettua $\lfloor n/2 \rfloor + 1$ chiamate, che è anche la profondità della ricorsione (l'albero è un cammino). Per $n = 5$: $3$ chiamate, come nella domanda 1, e $S(5) = 8$.

    4. Sì: la chiamata ricorsiva alla riga [8](#riga-es-14-ricorsione-exrecthree-e) è l'ultima operazione e il suo risultato viene restituito invariato. Sostituendo la chiamata in coda con l'aggiornamento $(l, r) \leftarrow (l+1, r-1)$ otteniamo:

        !!! algoritmo "Algoritmo: IterativeIsPalindrome"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span><strong>true</strong> se <span class="arithmatex">&#92;(a&#92;)</span> è un palindromo, <strong>false</strong> altrimenti</span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> IterativeIsPalindrome(a, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(l := 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r := n&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(l &lt; r&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;l&#93; &#92;ne a&#91;r&#93;&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>false</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(l &#92;leftarrow l + 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r &#92;leftarrow r - 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>true</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Usa una memoria costante invece di una pila di profondità $\lfloor n/2 \rfloor + 1$.

    5. Per invertire $a[l..r]$: si scambiano i due elementi estremi, poi si inverte il sotto-array interno $a[l+1..r-1]$. Un sotto-array con al più un elemento è già invertito (caso base, non c'è nulla da fare).

        !!! algoritmo "Algoritmo: Reverse"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#92;)</span> e due indici <span class="arithmatex">&#92;(l, r&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il sotto-array <span class="arithmatex">&#92;(a&#91;l..r&#93;&#92;)</span> invertito sul posto</span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Reverse(a, l, r)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(l &lt; r&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">scambia <span class="arithmatex">&#92;(a&#91;l&#93;&#92;)</span> e <span class="arithmatex">&#92;(a&#91;r&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">Reverse<span class="arithmatex">&#92;((a, l+1, r-1)&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Esecuzione su $a = [5, 7, 2, 9, 4, 6]$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th>azione</th>
        <th>array dopo lo scambio della chiamata</th>
        </tr>
        <tr>
        <td><code>Reverse</code><span class="arithmatex">&#92;((a,1,6)&#92;)</span></td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;1&#93;=5&#92;)</span>, <span class="arithmatex">&#92;(a&#91;6&#93;=6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;6, 7, 2, 9, 4, 5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td><code>Reverse</code><span class="arithmatex">&#92;((a,2,5)&#92;)</span></td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;2&#93;=7&#92;)</span>, <span class="arithmatex">&#92;(a&#91;5&#93;=4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;6, 4, 2, 9, 7, 5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td><code>Reverse</code><span class="arithmatex">&#92;((a,3,4)&#92;)</span></td>
        <td>scambia <span class="arithmatex">&#92;(a&#91;3&#93;=2&#92;)</span>, <span class="arithmatex">&#92;(a&#91;4&#93;=9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;6, 4, 9, 2, 7, 5&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td><code>Reverse</code><span class="arithmatex">&#92;((a,4,3)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(l &#92;ge r&#92;)</span>: caso base, nulla da fare</td>
        <td><span class="arithmatex">&#92;(&#91;6, 4, 9, 2, 7, 5&#93;&#92;)</span></td>
        </tr>
        </table></div>

        L'array finale è $[6, 4, 9, 2, 7, 5]$, dopo $\lfloor 6/2 \rfloor + 1 = 4$ chiamate e $3$ scambi. La correttezza segue per induzione su $k = r - l + 1$ esattamente come nella domanda 2.

<a id="esercizio-14-4"></a>

!!! esercizio "Esercizio 14.4: Ricorsione (E4)"

    Si consideri l'algoritmo ricorsivo ingenuo per i numeri di Fibonacci ($F(0) = 0$, $F(1) = 1$, $F(n) = F(n-1) + F(n-2)$ per $n \ge 2$).

    !!! algoritmo "Algoritmo: Fib"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero di Fibonacci <span class="arithmatex">&#92;(F(n)&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Fib(n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;le 1&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(n&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> Fib<span class="arithmatex">&#92;((n-1)&#92;)</span> <span class="arithmatex">&#92;(+&#92;)</span> Fib<span class="arithmatex">&#92;((n-2)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Disegnare l'albero delle chiamate ricorsive di <code>Fib</code>$(6)$ e calcolare il valore restituito.

    2. Contare il numero di chiamate $C(6)$ e verificare la formula $C(n) = 2F(n+1) - 1$.

    3. Quante volte viene chiamata <code>Fib</code>$(k)$, per ogni $k = 0, 1, \dots, 6$, durante il calcolo di <code>Fib</code>$(6)$? Che cosa si osserva?

    4. Confrontare il numero di passi di <code>Fib</code> ($S(n) = 4F(n+1) - 2$) con il numero di passi di <code>IterativeFib</code> ($S(n) = 5n + 1$) per $n = 6$ e per $n = 20$.

    5. Qual è la profondità della ricorsione di <code>Fib</code>$(6)$?

??? soluzione "Soluzione"

    1. L'albero delle chiamate ricorsive di <code>Fib</code>$(6)$ (scriviamo F$k$ per <code>Fib</code>$(k)$):

        ![Figura 2](../img/es-14-ricorsione/fig02.svg){ .fig loading=lazy  }

        Risalendo dalle foglie alla radice: <code>Fib</code>$(2) = 1 + 0 = 1$, <code>Fib</code>$(3) = 1 + 1 = 2$, <code>Fib</code>$(4) = 2 + 1 = 3$, <code>Fib</code>$(5) = 3 + 2 = 5$, <code>Fib</code>$(6) = 5 + 3 = 8$. Quindi $F(6) = 8$.

    2. Contando i nodi dell'albero livello per livello: $1 + 2 + 4 + 8 + 8 + 2 = 25$. La formula dà

        $$
        C(6) = 2F(7) - 1 = 2 \cdot 13 - 1 = 25.
        $$

        Equivalentemente, dall'equazione di ricorrenza $C(n) = C(n-1) + C(n-2) + 1$ con $C(0) = C(1) = 1$: $C(2) = 3$, $C(3) = 5$, $C(4) = 9$, $C(5) = 15$, $C(6) = 15 + 9 + 1 = 25$.

    3. Contando i nodi con la stessa etichetta:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(k&#92;)</span></th>
        <th>6</th>
        <th>5</th>
        <th>4</th>
        <th>3</th>
        <th>2</th>
        <th>1</th>
        <th>0</th>
        <th>totale</th>
        </tr>
        <tr>
        <td>numero di chiamate <code>Fib</code><span class="arithmatex">&#92;((k)&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>5</td>
        <td>8</td>
        <td>5</td>
        <td>25</td>
        </tr>
        </table></div>

        I numeri di chiamate sono essi stessi numeri di Fibonacci: <code>Fib</code>$(k)$ viene chiamata $F(7-k)$ volte per $k \ge 1$ (e <code>Fib</code>$(0)$ viene chiamata $F(5)$ volte, una per ogni chiamata <code>Fib</code>$(2)$). Gli stessi sottoproblemi vengono risolti più e più volte: per esempio $F(2)$ viene calcolato $5$ volte, mentre basterebbe calcolarlo una volta e memorizzarlo. Questa è la motivazione della <strong>Programmazione Dinamica</strong>.

    4. Il numero di chiamate e di passi dei due algoritmi è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th>chiamate <span class="arithmatex">&#92;(C(n) = 2F(n+1)-1&#92;)</span></th>
        <th>passi di <code>Fib</code>: <span class="arithmatex">&#92;(4F(n+1) - 2&#92;)</span></th>
        <th>passi di <code>IterativeFib</code>: <span class="arithmatex">&#92;(5n+1&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;cdot 13 - 1 = 25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 13 - 2 = 50&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;cdot 10946 - 1 = 21891&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 10946 - 2 = 43782&#92;)</span></td>
        <td><span class="arithmatex">&#92;(101&#92;)</span></td>
        </tr>
        </table></div>

        Per $n = 6$ i due algoritmi sono confrontabili, ma per $n = 20$ l'algoritmo ingenuo esegue più di $400$ volte il numero di passi di quello iterativo: il primo cresce esponenzialmente, il secondo linearmente.

    5. Il cammino più lungo dalla radice a una foglia è <code>Fib</code>$(6)$, <code>Fib</code>$(5)$, <code>Fib</code>$(4)$, <code>Fib</code>$(3)$, <code>Fib</code>$(2)$, <code>Fib</code>$(1)$: la profondità della ricorsione è $6$. Benché vengano eseguite $25$ chiamate, al più $6$ stack frame sono simultaneamente in memoria.

<a id="esercizio-14-5"></a>

!!! esercizio "Esercizio 14.5: Ricorsione (E5)"

    Si considerino le Torri di Hanoi con $n = 4$ dischi, numerati $1, 2, 3, 4$ dal più piccolo al più grande, inizialmente sul piolo $A$, da spostare sul piolo $C$ usando il piolo $B$ come piolo ausiliario, con l'algoritmo ricorsivo:

    !!! algoritmo "Algoritmo: Hanoi"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Il numero di dischi <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span>, i pioli <span class="arithmatex">&#92;(from&#92;)</span>, <span class="arithmatex">&#92;(to&#92;)</span>, <span class="arithmatex">&#92;(aux&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>La sequenza di mosse che trasferisce i dischi <span class="arithmatex">&#92;(1,2,&#92;dots,n&#92;)</span> da <span class="arithmatex">&#92;(from&#92;)</span> a <span class="arithmatex">&#92;(to&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Hanoi(n, from, to, aux)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 1&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">sposta il disco <span class="arithmatex">&#92;(1&#92;)</span> da <span class="arithmatex">&#92;(from&#92;)</span> a <span class="arithmatex">&#92;(to&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">Hanoi<span class="arithmatex">&#92;((n-1, from, aux, to)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">sposta il disco <span class="arithmatex">&#92;(n&#92;)</span> da <span class="arithmatex">&#92;(from&#92;)</span> a <span class="arithmatex">&#92;(to&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">Hanoi<span class="arithmatex">&#92;((n-1, aux, to, from)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Elencare, in ordine, tutte le mosse eseguite da <code>Hanoi</code>$(4, A, C, B)$.

    2. Verificare che il numero di mosse è $M(4) = 2^4 - 1$.

    3. Quante volte viene spostato ciascun disco? Dimostrare che, con $n$ dischi, il disco $k$ viene spostato esattamente $2^{n-k}$ volte ($\forall k \in \{1, 2, \dots, n\}$), e verificare che $\sum_{k=1}^{n} 2^{n-k} = 2^n - 1$.

    4. Quante chiamate di <code>Hanoi</code> vengono eseguite per $n = 4$, e qual è la profondità della ricorsione?

    5. Secondo la leggenda, $n = 64$ dischi d'oro vengono spostati alla velocità di una mossa al secondo. Quanto tempo ci vuole?

??? soluzione "Soluzione"

    1. <code>Hanoi</code>$(4, A, C, B)$ esegue <code>Hanoi</code>$(3, A, B, C)$, poi sposta il disco $4$ da $A$ a $C$, poi esegue <code>Hanoi</code>$(3, B, C, A)$. Ogni chiamata con $n = 3$ effettua $7$ mosse (secondo lo stesso schema di <code>Hanoi</code>$(3, A, C, B)$ nel capitolo, con i pioli rinominati):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>mossa</th>
        <th>disco</th>
        <th>da</th>
        <th>a</th>
        <th>mossa</th>
        <th>disco</th>
        <th>da</th>
        <th>a</th>
        </tr>
        <tr>
        <td>1</td>
        <td>1</td>
        <td>A</td>
        <td>B</td>
        <td>9</td>
        <td>1</td>
        <td>B</td>
        <td>C</td>
        </tr>
        <tr>
        <td>2</td>
        <td>2</td>
        <td>A</td>
        <td>C</td>
        <td>10</td>
        <td>2</td>
        <td>B</td>
        <td>A</td>
        </tr>
        <tr>
        <td>3</td>
        <td>1</td>
        <td>B</td>
        <td>C</td>
        <td>11</td>
        <td>1</td>
        <td>C</td>
        <td>A</td>
        </tr>
        <tr>
        <td>4</td>
        <td>3</td>
        <td>A</td>
        <td>B</td>
        <td>12</td>
        <td>3</td>
        <td>B</td>
        <td>C</td>
        </tr>
        <tr>
        <td>5</td>
        <td>1</td>
        <td>C</td>
        <td>A</td>
        <td>13</td>
        <td>1</td>
        <td>A</td>
        <td>B</td>
        </tr>
        <tr>
        <td>6</td>
        <td>2</td>
        <td>C</td>
        <td>B</td>
        <td>14</td>
        <td>2</td>
        <td>A</td>
        <td>C</td>
        </tr>
        <tr>
        <td>7</td>
        <td>1</td>
        <td>A</td>
        <td>B</td>
        <td>15</td>
        <td>1</td>
        <td>B</td>
        <td>C</td>
        </tr>
        <tr>
        <td><strong>8</strong></td>
        <td><strong>4</strong></td>
        <td><strong>A</strong></td>
        <td><strong>C</strong></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        </tr>
        </table></div>

        Le mosse $1$–$7$ trasferiscono i dischi $1,2,3$ da $A$ a $B$ (chiamata <code>Hanoi</code>$(3,A,B,C)$), la mossa $8$ sposta il disco più grande, e le mosse $9$–$15$ trasferiscono i dischi $1,2,3$ da $B$ a $C$ (chiamata <code>Hanoi</code>$(3,B,C,A)$).

    2. Ci sono $15$ mosse e $2^4 - 1 = 15$. Equivalentemente, $M(1) = 1$, $M(2) = 2 \cdot 1 + 1 = 3$, $M(3) = 2 \cdot 3 + 1 = 7$, $M(4) = 2 \cdot 7 + 1 = 15$.

    3. Dalla tabella: il disco $1$ viene spostato $8$ volte, il disco $2$ viene spostato $4$ volte, il disco $3$ viene spostato $2$ volte e il disco $4$ viene spostato una volta; sono $2^{4-1}, 2^{4-2}, 2^{4-3}, 2^{4-4}$.

        <strong>Dimostrazione</strong> per induzione su $n$ che, in <code>Hanoi</code>$(n, \cdot, \cdot, \cdot)$, il disco $k$ viene spostato $2^{n-k}$ volte per ogni $k \in \{1, 2, \dots, n\}$.

        - <strong>Caso base</strong> ($n = 1$): il disco $1$ viene spostato una volta $= 2^{1-1}$.

        - <strong>Passo induttivo</strong> ($n \ge 2$): il disco $n$ viene spostato solo dalla chiamata stessa, una volta $= 2^{n-n}$. Un disco $k \le n-1$ viene spostato solo all'interno delle due chiamate ricorsive con $n-1$ dischi, e per ipotesi induttiva viene spostato $2^{(n-1)-k}$ volte in ciascuna di esse: in totale $2 \cdot 2^{n-1-k} = 2^{n-k}$ volte.

        Sommando su tutti i dischi (somma geometrica),

        $$
        \sum_{k=1}^{n} 2^{n-k} = 2^{n-1} + 2^{n-2} + \dots + 2 + 1 = 2^n - 1 = M(n).
        $$

        Per $n=4$: $8 + 4 + 2 + 1 = 15$.

    4. Ogni chiamata esegue esattamente una mossa (il caso base sposta il disco $1$, le altre chiamate spostano il disco $n$), quindi il numero di chiamate è uguale al numero di mosse: $15$ chiamate. L'albero delle chiamate ricorsive è un albero binario completo con $4$ livelli ($1 + 2 + 4 + 8 = 15$ nodi), quindi la profondità della ricorsione è $4$.

    5. $M(64) = 2^{64} - 1 = 18\,446\,744\,073\,709\,551\,615$ mosse, cioè lo stesso numero di secondi. Un anno ha circa $365.25 \cdot 24 \cdot 3600 = 31\,557\,600$ secondi, quindi il tempo è

        $$
        \frac{2^{64}-1}{31\,557\,600} \approx 5.85 \cdot 10^{11} \text{ anni},
        $$

        circa $585$ miliardi di anni (più di $40$ volte l'età dell'universo). Poiché il numero di mosse di <code>Hanoi</code> è ottimo, nessun algoritmo può fare meglio.

<a id="esercizio-14-6"></a>

!!! esercizio "Esercizio 14.6: Ricorsione (E6)"

    Si considerino i due algoritmi ricorsivi seguenti: <code>FastPower</code> calcola $x^n$ per elevamento al quadrato, <code>ToBinary</code> stampa la rappresentazione binaria di un numero naturale $n$.

    !!! algoritmo "Algoritmo"

        <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> FastPower</div>
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero <span class="arithmatex">&#92;(x&#92;)</span> e un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>La potenza <span class="arithmatex">&#92;(x^n&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FastPower(x, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(y :=&#92;)</span> FastPower<span class="arithmatex">&#92;((x, &#92;lfloor n/2 &#92;rfloor)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;bmod 2 = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(y &#92;cdot y&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(x &#92;cdot y &#92;cdot y&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

        <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> ToBinary</div>
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Le cifre binarie di <span class="arithmatex">&#92;(n&#92;)</span>, stampate a partire dalla più significativa</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ToBinary(n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;le 1&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">stampa <span class="arithmatex">&#92;(n&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">ToBinary<span class="arithmatex">&#92;((&#92;lfloor n/2 &#92;rfloor)&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">stampa <span class="arithmatex">&#92;(n &#92;bmod 2&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Mostrare la sequenza di chiamate di <code>FastPower</code>$(x, 25)$ e contare il numero di moltiplicazioni. Confrontare con l'algoritmo ingenuo, che esegue $n$ moltiplicazioni.

    2. Calcolare il numero di moltiplicazioni e il numero di passi $S(n) = 4\lfloor \log_2 n \rfloor + 6$ di <code>FastPower</code> per $n = 31$, $n = 32$ e $n = 100$.

    3. Uno studente sostituisce la riga $y :=$ <code>FastPower</code>$(x, \lfloor n/2 \rfloor)$ e le righe seguenti con

        $$
        \textbf{return } \texttt{FastPower}(x, \lfloor n/2 \rfloor) \cdot \texttt{FastPower}(x, \lfloor n/2 \rfloor) \quad (\text{per } x \text{ se } n \text{ è dispari}).
        $$

        Scrivere l'equazione di ricorrenza del numero di chiamate $C(n)$ di questa versione, calcolare $C(13)$ e $C(16)$, e mostrare che $C(n) = \Theta(n)$.

    4. Mostrare l'esecuzione di <code>ToBinary</code>$(37)$: chiamate, cifre stampate e numero di chiamate. Perché le cifre vengono stampate nell'ordine corretto, mentre l'algoritmo <code>ChangeOfBase</code> (capitolo «Algoritmi numerici») le produce a partire dalla meno significativa?

    5. Dimostrare per induzione forte che <code>ToBinary</code>$(n)$ stampa la rappresentazione binaria di $n$, e che esegue $\lfloor \log_2 n \rfloor + 1$ chiamate per $n \ge 1$.

??? soluzione "Soluzione"

    1. Gli esponenti delle chiamate sono $25, 12, 6, 3, 1, 0$. Risalendo dal caso base:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th><span class="arithmatex">&#92;(y&#92;)</span></th>
        <th>restituisce</th>
        <th>moltiplicazioni</th>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 0)&#92;)</span></td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (caso base)</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 1)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x &#92;cdot 1 &#92;cdot 1 = x&#92;)</span> (dispari)</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 3)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x &#92;cdot x &#92;cdot x = x^3&#92;)</span> (dispari)</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 6)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x^3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x^3 &#92;cdot x^3 = x^6&#92;)</span> (pari)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 12)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x^6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x^6 &#92;cdot x^6 = x^{12}&#92;)</span> (pari)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><code>FastPower</code><span class="arithmatex">&#92;((x, 25)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x^{12}&#92;)</span></td>
        <td><span class="arithmatex">&#92;(x &#92;cdot x^{12} &#92;cdot x^{12} = x^{25}&#92;)</span> (dispari)</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        </table></div>

        In totale $2 + 2 + 1 + 1 + 2 = 8$ moltiplicazioni, contro $25$ dell'algoritmo ingenuo. Si noti che $25 = (11001)_2$: $5$ cifre binarie, tre delle quali uguali a $1$, e $5 + 3 = 8$.

    2. Il numero di moltiplicazioni è il numero di cifre binarie di $n$ più il numero di cifre uguali a $1$ (ogni chiamata con $n \ge 1$ esegue $1$ moltiplicazione se $n$ è pari, $2$ se $n$ è dispari, e la parità degli esponenti successivi dà le cifre binarie di $n$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th>binario</th>
        <th>moltiplicazioni</th>
        <th><span class="arithmatex">&#92;(S(n) = 4&#92;lfloor &#92;log&#95;2 n &#92;rfloor + 6&#92;)</span></th>
        <th>ingenuo</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11111&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5 + 5 = 10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 4 + 6 = 22&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(32&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100000&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6 + 1 = 7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 5 + 6 = 26&#92;)</span></td>
        <td><span class="arithmatex">&#92;(32&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1100100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7 + 3 = 10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 6 + 6 = 30&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        </tr>
        </table></div>

        Si noti che $x^{32}$ richiede meno moltiplicazioni di $x^{31}$, benché $32 > 31$.

    3. Ogni chiamata con $n \ge 1$ effettua ora <strong>due</strong> chiamate ricorsive su $\lfloor n/2 \rfloor$:

        $$
        C(n) = 2C(\lfloor n/2 \rfloor) + 1 \quad (n \ge 1), \qquad C(0) = 1.
        $$

        Quindi $C(1) = 3$, $C(3) = 7$, $C(6) = 15$, $C(13) = 31$, e $C(2) = 7$, $C(4) = 15$, $C(8) = 31$, $C(16) = 63$.

        L'albero delle chiamate ricorsive è ora un albero binario completo. I suoi livelli corrispondono agli esponenti $n, \lfloor n/2 \rfloor, \dots, 1, 0$, cioè ci sono $L = \lfloor \log_2 n \rfloor + 2$ livelli, con $1, 2, 4, \dots, 2^{L-1}$ nodi. Quindi

        $$
        C(n) = 1 + 2 + \dots + 2^{L-1} = 2^{L} - 1 = 4 \cdot 2^{\lfloor \log_2 n \rfloor} - 1.
        $$

        (Verifica: $C(13) = 4 \cdot 8 - 1 = 31$, $C(16) = 4 \cdot 16 - 1 = 63$.) Poiché $n/2 < 2^{\lfloor \log_2 n \rfloor} \le n$, si ottiene $2n - 1 < C(n) \le 4n - 1$, cioè $C(n) = \Theta(n)$: la versione con due chiamate ricorsive identiche <strong>non è migliore dell'algoritmo ingenuo</strong>. Calcolare il valore una sola volta e memorizzarlo in $y$ è essenziale.

    4. Esecuzione di <code>ToBinary</code>$(37)$:

        <strong>Chiamate</strong>:

        <code>ToBinary</code>$(37) \to$ <code>ToBinary</code>$(18) \to$ <code>ToBinary</code>$(9) \to$<br> <code>ToBinary</code>$(4) \to$ <code>ToBinary</code>$(2) \to$ <code>ToBinary</code>$(1)$

        <strong>Stampe</strong> (nell'ordine in cui le chiamate terminano):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>chiamata</th>
        <th>azione</th>
        <th>stampato finora</th>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((1)&#92;)</span></td>
        <td>caso base, stampa <span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((2)&#92;)</span></td>
        <td>stampa <span class="arithmatex">&#92;(2 &#92;bmod 2 = 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((4)&#92;)</span></td>
        <td>stampa <span class="arithmatex">&#92;(4 &#92;bmod 2 = 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((9)&#92;)</span></td>
        <td>stampa <span class="arithmatex">&#92;(9 &#92;bmod 2 = 1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1001&#92;)</span></td>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((18)&#92;)</span></td>
        <td>stampa <span class="arithmatex">&#92;(18 &#92;bmod 2 = 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10010&#92;)</span></td>
        </tr>
        <tr>
        <td><code>ToBinary</code><span class="arithmatex">&#92;((37)&#92;)</span></td>
        <td>stampa <span class="arithmatex">&#92;(37 &#92;bmod 2 = 1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100101&#92;)</span></td>
        </tr>
        </table></div>

        Quindi $37 = (100101)_2$ (infatti $32 + 4 + 1 = 37$), con $6$ chiamate.

        I resti $n \bmod 2$ vengono calcolati nello stesso ordine di <code>ChangeOfBase</code> (divisioni ripetute: $1, 0, 1, 0, 0, 1$, a partire dalla cifra meno significativa). Tuttavia, ogni chiamata stampa il proprio resto <strong>dopo</strong> che la sua chiamata ricorsiva è terminata, cioè dopo che tutte le cifre più significative sono state stampate: il call stack inverte l'ordine delle cifre, e non serve alcun array.

    5. <strong>Correttezza</strong>, per induzione forte su $n$.

        - <strong>Casi base</strong> ($n \in \{0,1\}$): la rappresentazione binaria di $n$ è la singola cifra $n$, che viene stampata.

        - <strong>Passo induttivo</strong> ($n \ge 2$): si ha $n = 2\lfloor n/2 \rfloor + (n \bmod 2)$ con $1 \le \lfloor n/2 \rfloor < n$. Se $\lfloor n/2 \rfloor = (d_{k-1} \dots d_0)_2$, allora

            $$
            n = 2\sum_{i=0}^{k-1} d_i 2^i + (n \bmod 2) = (d_{k-1} \dots d_0 \; (n \bmod 2))_2,
            $$

            cioè la rappresentazione binaria di $n$ è quella di $\lfloor n/2 \rfloor$ seguita dalla cifra $n \bmod 2$. Per ipotesi induttiva la chiamata ricorsiva stampa $d_{k-1} \dots d_0$, e poi l'algoritmo stampa $n \bmod 2$.

        <strong>Numero di chiamate.</strong> Sia $C(n)$ il numero di chiamate per $n \ge 1$: $C(1) = 1$ e $C(n) = C(\lfloor n/2 \rfloor) + 1$ per $n \ge 2$. Dimostriamo $C(n) = \lfloor \log_2 n \rfloor + 1$ per induzione forte: $C(1) = 1 = \lfloor \log_2 1 \rfloor + 1$; per $n \ge 2$, usando $\lfloor \log_2 \lfloor n/2 \rfloor \rfloor = \lfloor \log_2 n \rfloor - 1$,

        $$
        C(n) = \big(\lfloor \log_2 n \rfloor - 1 + 1\big) + 1 = \lfloor \log_2 n \rfloor + 1.
        $$

        Questo è il numero di cifre binarie di $n$ (una cifra stampata per ogni chiamata). Per $n = 37$: $\lfloor \log_2 37 \rfloor + 1 = 5 + 1 = 6$.
