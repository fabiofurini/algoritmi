---
title: "Esercizi · Pseudocodice"
---

# Esercizi · Pseudocodice

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 2** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 2](../algoritmi-di-base/02-pseudocodice.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-algoritmi-di-base.pdf)

</div>

<a id="esercizio-2-1"></a>

!!! esercizio "Esercizio 2.1: Pseudocodice (E1)"

    Dato un array $a[1..n]$ di $n \ge 1$ numeri interi, si consideri il problema di determinare il valore minimo dell'array.

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che trova il valore minimo in un array $a$ di $n$ numeri interi. L'algoritmo deve:

        - ricevere in input un array $a[1..n]$ di $n \ge 1$ numeri interi;

        - restituire il valore minimo $min$ dell'array;

        - usare una sola scansione dell'array.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$;

        - Istanza 2: $a = [15, 7, 22, 4]$ con $n=4$;

        - Istanza 3: $a = [100]$ con $n=1$.

        Per ogni istanza, mostrare lo stato iniziale delle variabili, il loro stato dopo ogni iterazione e il risultato finale.

    3. Scrivere lo pseudocodice di un algoritmo che trova sia il valore massimo sia il valore minimo con una sola scansione dell'array.

??? soluzione "Soluzione"

    1. Pseudocodice per trovare il valore minimo in un array:

        !!! algoritmo "Algoritmo: FindMinimum"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore minimo nell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMinimum(a, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min := a&#91;1&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(min&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Inizializziamo $min$ ad $a[1]$, il primo elemento (esiste, poiché $n \ge 1$).

        - Scorriamo ogni elemento restante dell'array, confrontandolo con il minimo corrente.

        - Se l'elemento corrente è più piccolo, aggiorniamo il minimo.

        - Infine, restituiamo il valore minimo trovato.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $a = [9, 12, 3, 16, 19, 11, 12]$, $n=7$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(min&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(19&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $min = 3$

        <strong>Istanza 2:</strong> $a = [15, 7, 22, 4]$, $n=4$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(min&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(22&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $min = 4$

        <strong>Istanza 3:</strong> $a = [100]$, $n=1$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(min&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        </tr>
        <tr>
        <td colspan="4">nessuna iterazione: il ciclo parte da <span class="arithmatex">&#92;(i = 2 &gt; n = 1&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $min = 100$

    3. Pseudocodice per trovare sia il massimo sia il minimo con una sola scansione:

        !!! algoritmo "Algoritmo: FindMaxMin"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>La coppia <span class="arithmatex">&#92;((max, min)&#92;)</span>, dove <span class="arithmatex">&#92;(max&#92;)</span> è il massimo e <span class="arithmatex">&#92;(min&#92;)</span> è il minimo di <span class="arithmatex">&#92;(a&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMaxMin(a, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max := a&#91;1&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min := a&#91;1&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &lt; min&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(min &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(max&#92;)</span>, <span class="arithmatex">&#92;(min&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Ad esempio, sull'Istanza 1 ($a = [9, 12, 3, 16, 19, 11, 12]$) l'algoritmo restituisce $(19, 3)$.

<a id="esercizio-2-2"></a>

!!! esercizio "Esercizio 2.2: Pseudocodice (E2)"

    Dato un array $a[1..n]$ di $n \ge 1$ numeri interi, si consideri il problema di calcolare la somma dei suoi valori.

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che calcola la somma di tutti gli elementi di un array $a$ di $n$ numeri interi. L'algoritmo deve:

        - ricevere in input un array $a[1..n]$ di $n \ge 1$ numeri interi;

        - restituire la somma $sum$ di tutti gli elementi;

        - inizializzare una variabile $sum$ a $0$ e sommarle ogni elemento.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze:

        - Istanza 1: $a = [5, 12, 3, 8]$ con $n=4$;

        - Istanza 2: $a = [10, 20, 30]$ con $n=3$;

        - Istanza 3: $a = [7]$ con $n=1$.

        Per ogni istanza, mostrare il valore iniziale della somma, il suo valore dopo l'aggiunta di ogni elemento e il risultato finale.

    3. Modificare lo pseudocodice per calcolare sia la somma sia la media $avg = \frac{sum}{n}$ degli elementi, con una sola scansione dell'array.

??? soluzione "Soluzione"

    1. Pseudocodice per calcolare la somma di tutti gli elementi di un array:

        !!! algoritmo "Algoritmo: ArraySum"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>La somma di tutti gli elementi dell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ArraySum(a, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + a&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(sum&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Inizializziamo $sum$ a $0$.

        - Scorriamo ogni elemento dell'array, aggiungendolo alla somma parziale $sum$.

        - Infine, restituiamo la somma totale $sum$.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $a = [5, 12, 3, 8]$, $n=4$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(17&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(28&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $sum = 28$

        <strong>Istanza 2:</strong> $a = [10, 20, 30]$, $n=3$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        <td><span class="arithmatex">&#92;(30&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(30&#92;)</span></td>
        <td><span class="arithmatex">&#92;(60&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $sum = 60$

        <strong>Istanza 3:</strong> $a = [7]$, $n=1$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $sum = 7$

    3. Pseudocodice per calcolare sia la somma sia la media:

        !!! algoritmo "Algoritmo: ArraySumAndAverage"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>La coppia <span class="arithmatex">&#92;((sum, avg)&#92;)</span>, dove <span class="arithmatex">&#92;(sum&#92;)</span> è il totale e <span class="arithmatex">&#92;(avg&#92;)</span> è la media degli elementi</span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ArraySumAndAverage(a, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + a&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(avg := sum / n&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(sum&#92;)</span>, <span class="arithmatex">&#92;(avg&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        La precondizione $n \ge 1$ garantisce che la divisione $sum / n$ sia definita. Ad esempio, sull'Istanza 1 ($a = [5, 12, 3, 8]$, $n=4$) l'algoritmo restituisce $(28, 7)$, poiché la somma è $28$ e la media è $28/4 = 7$.

<a id="esercizio-2-3"></a>

!!! esercizio "Esercizio 2.3: Pseudocodice (E3)"

    Dato un array bidimensionale $b[1..m][1..n]$ di $m \times n$ numeri interi e un valore di soglia $k$, si consideri il problema di contare il numero dei suoi valori strettamente maggiori di $k$.

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che conta quanti elementi di $b$ sono strettamente maggiori della soglia $k$. L'algoritmo deve:

        - ricevere in input un array bidimensionale $b[1..m][1..n]$, le dimensioni $m$ e $n$, e la soglia $k$;

        - restituire il numero di elementi che soddisfano $b[i][j] > k$;

        - scorrere tutte le posizioni dell'array con due cicli annidati.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze, mostrando il valore di $count$ dopo ogni aggiornamento:

        - Istanza 1: $b = \begin{bmatrix} 3 & 7 & 1 \\ 5 & 2 & 8 \end{bmatrix}$, $m=2$, $n=3$, $k=4$;

        - Istanza 2: $b = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$, $m=3$, $n=3$, $k=5$.

    3. Modificare lo pseudocodice in modo che, oltre al conteggio, l'algoritmo restituisca anche un array di coppie $(i, j)$ che elenca le posizioni di tutti gli elementi dell'array bidimensionale maggiori di $k$.

??? soluzione "Soluzione"

    1. Pseudocodice per contare gli elementi maggiori di una soglia:

        !!! algoritmo "Algoritmo: CountGreaterThan"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale <span class="arithmatex">&#92;(b&#91;1..m&#93;&#91;1..n&#93;&#92;)</span>, le dimensioni <span class="arithmatex">&#92;(m&#92;)</span> e <span class="arithmatex">&#92;(n&#92;)</span>, e una soglia <span class="arithmatex">&#92;(k&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero <span class="arithmatex">&#92;(count&#92;)</span> di elementi con <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; k&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> CountGreaterThan(b, m, n, k)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count := 0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; k&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count &#92;leftarrow count + 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(count&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Inizializziamo $count$ a $0$.

        - Il ciclo esterno scorre le righe $i = 1, 2, \dots, m$, il ciclo interno le colonne $j = 1, 2, \dots, n$.

        - Per ogni elemento $b[i][j]$, se supera $k$ incrementiamo $count$.

        - Infine, restituiamo $count$.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $b = \begin{bmatrix} 3 & 7 & 1 \\ 5 & 2 & 8 \end{bmatrix}$, $m=2$, $n=3$, $k=4$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; 4&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(count&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $count = 3$ (elementi $7$, $5$, $8$)

        <strong>Istanza 2:</strong> $b = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$, $m=3$, $n=3$, $k=5$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; 5&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(count&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $count = 4$ (elementi $6$, $7$, $8$, $9$)

    3. Pseudocodice che restituisce anche le posizioni degli elementi maggiori di $k$. L'array $pos$ è dichiarato con $m \cdot n$ elementi, il massimo numero possibile di posizioni; ne vengono usati solo i primi $count$ elementi.

        !!! algoritmo "Algoritmo: CountAndListGreaterThan"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale <span class="arithmatex">&#92;(b&#91;1..m&#93;&#91;1..n&#93;&#92;)</span>, le dimensioni <span class="arithmatex">&#92;(m&#92;)</span> e <span class="arithmatex">&#92;(n&#92;)</span>, e una soglia <span class="arithmatex">&#92;(k&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero <span class="arithmatex">&#92;(count&#92;)</span> e l'array <span class="arithmatex">&#92;(pos&#91;1..count&#93;&#92;)</span> delle coppie <span class="arithmatex">&#92;((i,j)&#92;)</span> con <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; k&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> CountAndListGreaterThan(b, m, n, k)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count := 0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(pos := &#92;text{new array}&#91;1..m &#92;cdot n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &gt; k&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count &#92;leftarrow count + 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(pos&#91;count&#93; &#92;leftarrow (i, j)&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(count&#92;)</span>, <span class="arithmatex">&#92;(pos&#91;1..count&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Per l'Istanza 1, l'algoritmo restituisce $count=3$ e $pos = [(1,2),(2,1),(2,3)]$; per l'Istanza 2, restituisce $count = 4$ e $pos = [(2,3),(3,1),(3,2),(3,3)]$.

<a id="esercizio-2-4"></a>

!!! esercizio "Esercizio 2.4: Pseudocodice (E4)"

    Dato un array bidimensionale $b[1..m][1..n]$ di $m \times n$ numeri interi, con $m \ge 1$ e $n \ge 1$, si consideri il problema di trovare il valore minimo di ciascuna colonna.

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che calcola il minimo di ciascuna colonna dell'array bidimensionale $b$. L'algoritmo deve:

        - ricevere in input un array bidimensionale $b[1..m][1..n]$ e le dimensioni $m$, $n$;

        - restituire un array $colMin[1..n]$, dove l'elemento $colMin[j]$ è il minimo della colonna $j$;

        - scorrere le colonne e le righe con due cicli annidati.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze, mostrando ogni aggiornamento dell'array $colMin$:

        - Istanza 1: $b = \begin{bmatrix} 4 & 9 & 2 \\ 7 & 1 & 6 \\ 3 & 5 & 8 \end{bmatrix}$, $m=3$, $n=3$;

        - Istanza 2: $b = \begin{bmatrix} 8 & 3 \\ 5 & 7 \\ 2 & 4 \end{bmatrix}$, $m=3$, $n=2$.

    3. Modificare lo pseudocodice in modo che, oltre al valore minimo di ciascuna colonna, l'algoritmo restituisca anche l'indice di riga $rowIdx[j]$ della prima posizione in cui si trova il minimo della colonna $j$.

??? soluzione "Soluzione"

    1. Pseudocodice per calcolare i minimi delle colonne:

        !!! algoritmo "Algoritmo: ColumnMinima"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale <span class="arithmatex">&#92;(b&#91;1..m&#93;&#91;1..n&#93;&#92;)</span>, le dimensioni <span class="arithmatex">&#92;(m &#92;ge 1&#92;)</span> e <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un array <span class="arithmatex">&#92;(colMin&#91;1..n&#93;&#92;)</span>, dove <span class="arithmatex">&#92;(colMin&#91;j&#93;&#92;)</span> è il minimo della colonna <span class="arithmatex">&#92;(j&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ColumnMinima(b, m, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin := &#92;text{new array}&#91;1..n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin&#91;j&#93; &#92;leftarrow b&#91;1&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &lt; colMin&#91;j&#93;&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin&#91;j&#93; &#92;leftarrow b&#91;i&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(colMin&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Il ciclo esterno scorre le colonne $j = 1, 2, \dots, n$.

        - Inizializziamo $colMin[j]$ a $b[1][j]$, il primo elemento della colonna $j$.

        - Il ciclo interno scorre le righe $i = 2, 3, \dots, m$, confrontando ogni elemento con il minimo corrente della colonna, e aggiorna $colMin[j]$ quando trova un elemento più piccolo.

        - Infine, restituiamo l'array $colMin$.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $b = \begin{bmatrix} 4 & 9 & 2 \\ 7 & 1 & 6 \\ 3 & 5 & 8 \end{bmatrix}$, $m=3$, $n=3$

        <div class="minipage" style="width:32%" markdown>

        Colonna $j=1$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&lt;&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(colMin&#91;1&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:32%" markdown>

        Colonna $j=2$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&lt;&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(colMin&#91;2&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:32%" markdown>

        Colonna $j=3$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;3&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&lt;&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(colMin&#91;3&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        La colonna $<$? riporta l'esito del confronto $b[i][j] < colMin[j]$.

        <strong>Restituisce:</strong> $colMin = [3, 1, 2]$

        <strong>Istanza 2:</strong> $b = \begin{bmatrix} 8 & 3 \\ 5 & 7 \\ 2 & 4 \end{bmatrix}$, $m=3$, $n=2$

        <div class="minipage" style="width:48%" markdown>

        Colonna $j=1$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;1&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&lt;&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(colMin&#91;1&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>Sì</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <div class="minipage" style="width:48%" markdown>

        Colonna $j=2$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;2&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&lt;&#92;)</span>?</th>
        <th><span class="arithmatex">&#92;(colMin&#91;2&#93;&#92;)</span></th>
        </tr>
        <tr>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>No</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        </div>

        <strong>Restituisce:</strong> $colMin = [2, 3]$

    3. Pseudocodice che restituisce anche l'indice di riga del minimo di ciascuna colonna. L'aggiornamento usa il confronto stretto $<$, quindi in caso di parità viene mantenuta la prima riga.

        !!! algoritmo "Algoritmo: ColumnMinimaWithIndex"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale <span class="arithmatex">&#92;(b&#91;1..m&#93;&#91;1..n&#93;&#92;)</span> e le dimensioni <span class="arithmatex">&#92;(m &#92;ge 1&#92;)</span> e <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>Gli array <span class="arithmatex">&#92;(colMin&#91;1..n&#93;&#92;)</span> e <span class="arithmatex">&#92;(rowIdx&#91;1..n&#93;&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ColumnMinimaWithIndex(b, m, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin := &#92;text{new array}&#91;1..n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(rowIdx := &#92;text{new array}&#91;1..n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin&#91;j&#93; &#92;leftarrow b&#91;1&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(rowIdx&#91;j&#93; &#92;leftarrow 1&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &lt; colMin&#91;j&#93;&#92;)</span> <strong>then</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(colMin&#91;j&#93; &#92;leftarrow b&#91;i&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(rowIdx&#91;j&#93; &#92;leftarrow i&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(colMin&#92;)</span>, <span class="arithmatex">&#92;(rowIdx&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Per l'Istanza 1, l'algoritmo restituisce $colMin = [3,1,2]$ e $rowIdx = [3,2,1]$; per l'Istanza 2, restituisce $colMin = [2, 3]$ e $rowIdx = [3, 1]$.

<a id="esercizio-2-5"></a>

!!! esercizio "Esercizio 2.5: Pseudocodice (E5)"

    Dato un array bidimensionale $b[1..m][1..n]$ di $m \times n$ numeri interi, si consideri il problema di calcolarne l'array bidimensionale trasposto, cioè l'array bidimensionale $c[1..n][1..m]$ con $c[j][i] = b[i][j]$.

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che calcola la trasposta di un array bidimensionale $b[1..m][1..n]$. L'algoritmo deve:

        - ricevere in input un array bidimensionale $b[1..m][1..n]$ e le dimensioni $m$, $n$;

        - allocare un nuovo array bidimensionale $c[1..n][1..m]$ per il risultato;

        - restituire l'array bidimensionale trasposto $c$, tale che $c[j][i] = b[i][j]$.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze, mostrando l'array bidimensionale $c$ che viene riempito elemento per elemento:

        - Istanza 1: $b = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$, $m=2$, $n=3$;

        - Istanza 2: $b = \begin{bmatrix} 7 & 2 \\ 3 & 8 \\ 1 & 5 \end{bmatrix}$, $m=3$, $n=2$.

    3. Per un array bidimensionale quadrato ($m = n$), scrivere lo pseudocodice di un algoritmo che esegue la trasposizione sul posto (senza allocare un nuovo array bidimensionale), scambiando gli elementi $b[i][j]$ e $b[j][i]$ per ogni $i < j$.

??? soluzione "Soluzione"

    1. Pseudocodice per la trasposizione di un array bidimensionale:

        !!! algoritmo "Algoritmo: Transpose"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale <span class="arithmatex">&#92;(b&#91;1..m&#93;&#91;1..n&#93;&#92;)</span>, le dimensioni <span class="arithmatex">&#92;(m&#92;)</span> e <span class="arithmatex">&#92;(n&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array bidimensionale trasposto <span class="arithmatex">&#92;(c&#91;1..n&#93;&#91;1..m&#93;&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Transpose(b, m, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := &#92;text{new array}&#91;1..n&#93;&#91;1..m&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c&#91;j&#93;&#91;i&#93; &#92;leftarrow b&#91;i&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Allochiamo $c$ come un nuovo array bidimensionale $n \times m$.

        - Il ciclo esterno scorre le righe $i = 1, 2, \dots, m$ di $b$, il ciclo interno le colonne $j = 1, 2, \dots, n$ di $b$.

        - Ogni elemento $b[i][j]$ viene copiato nella posizione $c[j][i]$; ogni elemento di $c$ viene assegnato esattamente una volta.

        - Infine, restituiamo l'array bidimensionale trasposto $c$.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $b = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$, $m=2$, $n=3$, quindi $c$ è $3 \times 2$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93;&#92;)</span></th>
        <th>assegnamento</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;1&#93;&#91;1&#93; &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;2&#93;&#91;1&#93; &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;3&#93;&#91;1&#93; &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;1&#93;&#91;2&#93; &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;2&#93;&#91;2&#93; &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;3&#93;&#91;2&#93; &#92;leftarrow 6&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $c = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$

        <strong>Istanza 2:</strong> $b = \begin{bmatrix} 7 & 2 \\ 3 & 8 \\ 1 & 5 \end{bmatrix}$, $m=3$, $n=2$, quindi $c$ è $2 \times 3$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93;&#92;)</span></th>
        <th>assegnamento</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;1&#93;&#91;1&#93; &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;2&#93;&#91;1&#93; &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;1&#93;&#91;2&#93; &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;2&#93;&#91;2&#93; &#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;1&#93;&#91;3&#93; &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(c&#91;2&#93;&#91;3&#93; &#92;leftarrow 5&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $c = \begin{bmatrix} 7 & 3 & 1 \\ 2 & 8 & 5 \end{bmatrix}$

    3. Trasposizione sul posto di un array bidimensionale quadrato ($m = n$):

        !!! algoritmo "Algoritmo: TransposeInPlace"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array bidimensionale quadrato <span class="arithmatex">&#92;(b&#91;1..n&#93;&#91;1..n&#93;&#92;)</span>, la dimensione <span class="arithmatex">&#92;(n&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array bidimensionale <span class="arithmatex">&#92;(b&#92;)</span>, trasposto sul posto</span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> TransposeInPlace(b, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n-1&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := i+1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(tmp := b&#91;i&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &#92;leftarrow b&#91;j&#93;&#91;i&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(b&#91;j&#93;&#91;i&#93; &#92;leftarrow tmp&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(b&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        Il ciclo interno parte da $j = i+1$, in modo che ogni coppia di posizioni simmetriche venga scambiata esattamente una volta (scambiarla due volte ripristinerebbe l'array originale) e gli elementi $b[i][i]$ sulla diagonale non vengano mai spostati. Per $i = n$ il ciclo interno sarebbe vuoto, quindi il ciclo esterno si ferma a $n-1$. Ad esempio, su $b = \begin{bmatrix} 4 & 1 \\ 9 & 6 \end{bmatrix}$ ($n=2$) l'unica iterazione scambia $b[1][2]=1$ e $b[2][1]=9$, dando $b = \begin{bmatrix} 4 & 9 \\ 1 & 6 \end{bmatrix}$.

<a id="esercizio-2-6"></a>

!!! esercizio "Esercizio 2.6: Pseudocodice (E6)"

    Dati un array bidimensionale $a[1..m][1..p]$ di $m \times p$ numeri interi e un array bidimensionale $b[1..p][1..n]$ di $p \times n$ numeri interi, si consideri il problema di calcolarne il prodotto, cioè l'array bidimensionale $c[1..m][1..n]$ con:

    $$
    c[i][j] = \sum_{k=1}^{p} a[i][k] \cdot b[k][j]
    $$

    **Domande**

    1. Scrivere lo pseudocodice di un algoritmo che calcola il prodotto $c = a \cdot b$. L'algoritmo deve:

        - ricevere in input gli array bidimensionali $a[1..m][1..p]$ e $b[1..p][1..n]$, e le dimensioni $m$, $p$, $n$;

        - allocare un nuovo array bidimensionale $c[1..m][1..n]$, inizializzato a zero;

        - usare tre cicli annidati (su $i$, $j$, $k$) per calcolare il prodotto con la formula precedente;

        - restituire l'array bidimensionale prodotto $c$.

    2. Eseguire l'algoritmo passo per passo sulle seguenti istanze, mostrando i valori di $k$ e $c[i][j]$ a ogni passo del ciclo più interno:

        - Istanza 1: $a = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$, $b = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$, $m=p=n=2$;

        - Istanza 2: $a = \begin{bmatrix} 1 & 0 \\ 0 & 1 \\ 2 & 3 \end{bmatrix}$, $b = \begin{bmatrix} 4 & 5 \\ 6 & 7 \end{bmatrix}$, $m=3$, $p=2$, $n=2$.

??? soluzione "Soluzione"

    1. Pseudocodice per il prodotto di due array bidimensionali:

        !!! algoritmo "Algoritmo: MatrixProduct"

            <div class="pseudocodice" markdown="0">
            <div class="pc-io"><span class="pc-kw">Input:</span> <span>Gli array bidimensionali <span class="arithmatex">&#92;(a&#91;1..m&#93;&#91;1..p&#93;&#92;)</span> e <span class="arithmatex">&#92;(b&#91;1..p&#93;&#91;1..n&#93;&#92;)</span>, le dimensioni <span class="arithmatex">&#92;(m&#92;)</span>, <span class="arithmatex">&#92;(p&#92;)</span>, <span class="arithmatex">&#92;(n&#92;)</span></span></div>
            <div class="pc-io"><span class="pc-kw">Output:</span> <span>L'array bidimensionale prodotto <span class="arithmatex">&#92;(c&#91;1..m&#93;&#91;1..n&#93;&#92;)</span></span></div>
            <div class="pc-sep"></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
            <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> MatrixProduct(a, b, m, p, n)</span></span></div>
            <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := &#92;text{new array}&#91;1..m&#93;&#91;1..n&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c&#91;i&#93;&#91;j&#93; &#92;leftarrow 0&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
            <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(k := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(p&#92;)</span> <strong>do</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c&#91;i&#93;&#91;j&#93; &#92;leftarrow c&#91;i&#93;&#91;j&#93; + a&#91;i&#93;&#91;k&#93; &#92;cdot b&#91;k&#93;&#91;j&#93;&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
            <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
            <div class="pc-riga"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
            </div>

        - Allochiamo $c$ come array bidimensionale $m \times n$ e inizializziamo a zero tutti i suoi elementi con due cicli annidati.

        - Il ciclo esterno scorre le righe di $c$, $i = 1, 2, \dots, m$, e il ciclo intermedio le sue colonne, $j = 1, 2, \dots, n$.

        - Il ciclo interno calcola la somma $\sum_{k=1}^{p} a[i][k] \cdot b[k][j]$, aggiungendo un prodotto a ogni iterazione.

        - Infine, restituiamo $c$.

    2. Esecuzione passo per passo sulle istanze.

        <strong>Istanza 1:</strong> $a = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$, $b = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$, $m=p=n=2$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#91;k&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;k&#93;&#91;j&#93;&#92;)</span></th>
        <th>prodotto</th>
        <th><span class="arithmatex">&#92;(c&#91;i&#93;&#91;j&#93;&#92;)</span> (dopo)</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;cdot 5 = 5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;cdot 7 = 14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(19&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;cdot 6 = 6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;cdot 8 = 16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(22&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;cdot 5 = 15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 7 = 28&#92;)</span></td>
        <td><span class="arithmatex">&#92;(43&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;cdot 6 = 18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;cdot 8 = 32&#92;)</span></td>
        <td><span class="arithmatex">&#92;(50&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $c = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$

        <strong>Istanza 2:</strong> $a = \begin{bmatrix} 1 & 0 \\ 0 & 1 \\ 2 & 3 \end{bmatrix}$, $b = \begin{bmatrix} 4 & 5 \\ 6 & 7 \end{bmatrix}$, $m=3$, $p=2$, $n=2$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(j&#92;)</span></th>
        <th><span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#91;k&#93;&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#91;k&#93;&#91;j&#93;&#92;)</span></th>
        <th>prodotto</th>
        <th><span class="arithmatex">&#92;(c&#91;i&#93;&#91;j&#93;&#92;)</span> (dopo)</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(26&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Restituisce:</strong> $c = \begin{bmatrix} 4 & 5 \\ 6 & 7 \\ 26 & 31 \end{bmatrix}$

        Le prime due righe di $a$ formano l'identità, quindi le prime due righe di $c$ coincidono con le due righe di $b$.
