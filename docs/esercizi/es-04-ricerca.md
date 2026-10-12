---
title: "Esercizi · Ricerca lineare e binaria"
---

# Esercizi · Ricerca lineare e binaria

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 4** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 4: Ricerca lineare e binaria](../algoritmi-di-base/04-ricerca.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-algoritmi-di-base.pdf)

</div>

Negli esercizi di questo capitolo le ricerche sono svolte con i due algoritmi del capitolo «Ricerca lineare e ricerca binaria», richiamati di seguito. Gli indici degli array vanno da $1$ a $n$, e viene restituito il valore $-1$ quando il valore cercato $m$ non è nell'array.

!!! algoritmo "Algoritmo: LinearSearch"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali e un valore <span class="arithmatex">&#92;(m&#92;)</span> da cercare</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Indice di <span class="arithmatex">&#92;(m&#92;)</span> in <span class="arithmatex">&#92;(a&#92;)</span>, oppure <span class="arithmatex">&#92;(-1&#92;)</span> se non trovato</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> LinearSearch(a, n, m)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(i&#92;)</span></span><span class="pc-c">// Elemento trovato all'indice <span class="arithmatex">&#92;(i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(-1&#92;)</span></span><span class="pc-c">// Elemento non trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

!!! algoritmo "Algoritmo: BinarySearch"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri naturali ordinato in modo non decrescente e un valore <span class="arithmatex">&#92;(m&#92;)</span> da cercare</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Indice di <span class="arithmatex">&#92;(m&#92;)</span> in <span class="arithmatex">&#92;(a&#92;)</span>, oppure <span class="arithmatex">&#92;(-1&#92;)</span> se non trovato</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> BinarySearch(a, n, m)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(left&#92;)</span> := <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(right&#92;)</span> := <span class="arithmatex">&#92;(n&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(left &#92;le right&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(mid&#92;)</span> := <span class="arithmatex">&#92;(left + &#92;lfloor (right - left) / 2 &#92;rfloor&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(mid&#92;)</span></span><span class="pc-c">// Elemento trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(left&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(mid + 1&#92;)</span></span><span class="pc-c">// Cerca nella metà destra</span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(right&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(mid - 1&#92;)</span></span><span class="pc-c">// Cerca nella metà sinistra</span></span></div>
    <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(-1&#92;)</span></span><span class="pc-c">// Elemento non trovato</span></span></div>
    <div class="pc-riga"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="esercizio-4-1"></a>

!!! esercizio "Esercizio 4.1: Ricerca lineare e ricerca binaria (E1)"

    Consideriamo il seguente array:

    $$
    a = [7, 2, 14, 3, 8, 11, 5, 9]
    $$

    con $n = 8$.

    **Domande**

    1. Applicare l'algoritmo di ricerca lineare (Linear Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 11$

        2. $m = 7$

        3. $m = 9$

        4. $m = 4$

        5. $m = 14$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $i$, $a[i]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 11$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 11 si trova all'indice 6.

    2. Ricerca di $m = 7$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 7 si trova all'indice 1.

    3. Ricerca di $m = 9$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 9 si trova all'indice 8.

    4. Ricerca di $m = 4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>8</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i &gt; n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> il ciclo termina, non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 4 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 14$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>14</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 14 si trova all'indice 3.

<a id="esercizio-4-2"></a>

!!! esercizio "Esercizio 4.2: Ricerca lineare e ricerca binaria (E2)"

    Consideriamo il seguente array:

    $$
    a = [15, 4, 22, 8, 1, 30, 17]
    $$

    con $n = 7$.

    **Domande**

    1. Applicare l'algoritmo di ricerca lineare (Linear Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 22$

        2. $m = 15$

        3. $m = 17$

        4. $m = 10$

        5. $m = 1$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $i$, $a[i]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 22$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>22</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 22 si trova all'indice 3.

    2. Ricerca di $m = 15$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 15 si trova all'indice 1.

    3. Ricerca di $m = 17$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>22</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 17 si trova all'indice 7.

    4. Ricerca di $m = 10$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>22</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>17</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i &gt; n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> il ciclo termina, non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 10 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 1$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>22</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 1 si trova all'indice 5.

<a id="esercizio-4-3"></a>

!!! esercizio "Esercizio 4.3: Ricerca lineare e ricerca binaria (E3)"

    Consideriamo il seguente array:

    $$
    a = [6, 19, 3, 27, 12, 5, 33]
    $$

    con $n = 7$.

    **Domande**

    1. Applicare l'algoritmo di ricerca lineare (Linear Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 27$

        2. $m = 6$

        3. $m = 33$

        4. $m = 15$

        5. $m = 3$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $i$, $a[i]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 27$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>19</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 27 si trova all'indice 4.

    2. Ricerca di $m = 6$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 6 si trova all'indice 1.

    3. Ricerca di $m = 33$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>19</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>12</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>33</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 33 si trova all'indice 7.

    4. Ricerca di $m = 15$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>19</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>12</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>33</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i &gt; n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> il ciclo termina, non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 15 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>19</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 3 si trova all'indice 3.

<a id="esercizio-4-4"></a>

!!! esercizio "Esercizio 4.4: Ricerca lineare e ricerca binaria (E4)"

    Consideriamo il seguente array:

    $$
    a = [50, 25, 75, 10, 40, 60, 5]
    $$

    con $n = 7$.

    **Domande**

    1. Applicare l'algoritmo di ricerca lineare (Linear Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 10$

        2. $m = 50$

        3. $m = 5$

        4. $m = 30$

        5. $m = 75$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $i$, $a[i]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 10$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>75</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 10 si trova all'indice 4.

    2. Ricerca di $m = 50$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 50 si trova all'indice 1.

    3. Ricerca di $m = 5$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>75</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>60</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 5 si trova all'indice 7.

    4. Ricerca di $m = 30$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>75</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>60</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i &gt; n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> il ciclo termina, non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 30 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 75$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>25</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>75</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 75 si trova all'indice 3.

<a id="esercizio-4-5"></a>

!!! esercizio "Esercizio 4.5: Ricerca lineare e ricerca binaria (E5)"

    Consideriamo il seguente array:

    $$
    a = [11, 7, 3, 18, 24, 9, 16, 2]
    $$

    con $n = 8$.

    **Domande**

    1. Applicare l'algoritmo di ricerca lineare (Linear Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 24$

        2. $m = 11$

        3. $m = 2$

        4. $m = 8$

        5. $m = 3$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $i$, $a[i]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 24$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 24 si trova all'indice 5.

    2. Ricerca di $m = 11$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 11 si trova all'indice 1.

    3. Ricerca di $m = 2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>16</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>8</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 2 si trova all'indice 8.

    4. Ricerca di $m = 8$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>5</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td>6</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td>7</td>
        <td>16</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td>8</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(i &gt; n&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> il ciclo termina, non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 8 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>2</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; &#92;neq m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;i&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 3 si trova all'indice 3.

<a id="esercizio-4-6"></a>

!!! esercizio "Esercizio 4.6: Ricerca lineare e ricerca binaria (E6)"

    Consideriamo il seguente array, ordinato in modo non decrescente:

    $$
    a = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78, 89]
    $$

    con $n = 12$.

    **Domande**

    1. Applicare l'algoritmo di ricerca binaria (Binary Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 23$

        2. $m = 2$

        3. $m = 89$

        4. $m = 50$

        5. $m = 1$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $left$, $right$, $mid$, $a[mid]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 23$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>6</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 23 si trova all'indice 6.

    2. Ricerca di $m = 2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>6</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>5</td>
        <td>3</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 2 si trova all'indice 1.

    3. Ricerca di $m = 89$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>6</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>7</td>
        <td>12</td>
        <td>9</td>
        <td>56</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 10&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>10</td>
        <td>12</td>
        <td>11</td>
        <td>78</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 12&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>12</td>
        <td>12</td>
        <td>12</td>
        <td>89</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 89 si trova all'indice 12.

    4. Ricerca di $m = 50$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>6</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>7</td>
        <td>12</td>
        <td>9</td>
        <td>56</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>7</td>
        <td>8</td>
        <td>7</td>
        <td>38</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>8</td>
        <td>8</td>
        <td>8</td>
        <td>45</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 50 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 1$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>12</td>
        <td>6</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>5</td>
        <td>3</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 1 non è presente nell'array (restituisce $-1$).

<a id="esercizio-4-7"></a>

!!! esercizio "Esercizio 4.7: Ricerca lineare e ricerca binaria (E7)"

    Consideriamo il seguente array, ordinato in modo non decrescente:

    $$
    a = [1, 3, 5, 7, 9, 11, 13, 15]
    $$

    con $n = 8$.

    **Domande**

    1. Applicare l'algoritmo di ricerca binaria (Binary Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 7$

        2. $m = 1$

        3. $m = 15$

        4. $m = 10$

        5. $m = 20$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $left$, $right$, $mid$, $a[mid]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 7$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>4</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 7 si trova all'indice 4.

    2. Ricerca di $m = 1$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>4</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>3</td>
        <td>2</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 1 si trova all'indice 1.

    3. Ricerca di $m = 15$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>4</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>7</td>
        <td>8</td>
        <td>7</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>8</td>
        <td>8</td>
        <td>8</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 15 si trova all'indice 8.

    4. Ricerca di $m = 10$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>4</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>5</td>
        <td>5</td>
        <td>5</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>6</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 10 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 20$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>8</td>
        <td>4</td>
        <td>7</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>5</td>
        <td>8</td>
        <td>6</td>
        <td>11</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>7</td>
        <td>8</td>
        <td>7</td>
        <td>13</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>8</td>
        <td>8</td>
        <td>8</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>9</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 20 non è presente nell'array (restituisce $-1$).

<a id="esercizio-4-8"></a>

!!! esercizio "Esercizio 4.8: Ricerca lineare e ricerca binaria (E8)"

    Consideriamo il seguente array, ordinato in modo non decrescente:

    $$
    a = [10, 20, 30, 40, 50, 60]
    $$

    con $n = 6$.

    **Domande**

    1. Applicare l'algoritmo di ricerca binaria (Binary Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 40$

        2. $m = 10$

        3. $m = 60$

        4. $m = 25$

        5. $m = 70$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $left$, $right$, $mid$, $a[mid]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 40$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>40</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 40 si trova all'indice 4.

    2. Ricerca di $m = 10$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 10 si trova all'indice 1.

    3. Ricerca di $m = 60$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>6</td>
        <td>6</td>
        <td>6</td>
        <td>60</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 60 si trova all'indice 6.

    4. Ricerca di $m = 25$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>2</td>
        <td>2</td>
        <td>2</td>
        <td>20</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>3</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 25 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 70$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>50</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>6</td>
        <td>6</td>
        <td>6</td>
        <td>60</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>7</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 70 non è presente nell'array (restituisce $-1$).

<a id="esercizio-4-9"></a>

!!! esercizio "Esercizio 4.9: Ricerca lineare e ricerca binaria (E9)"

    Consideriamo il seguente array, ordinato in modo non decrescente:

    $$
    a = [4, 8, 15, 16, 23, 42]
    $$

    con $n = 6$.

    **Domande**

    1. Applicare l'algoritmo di ricerca binaria (Binary Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 15$

        2. $m = 4$

        3. $m = 42$

        4. $m = 20$

        5. $m = 2$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $left$, $right$, $mid$, $a[mid]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 15$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 15 si trova all'indice 3.

    2. Ricerca di $m = 4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 4 si trova all'indice 1.

    3. Ricerca di $m = 42$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>6</td>
        <td>6</td>
        <td>6</td>
        <td>42</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 42 si trova all'indice 6.

    4. Ricerca di $m = 20$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>4</td>
        <td>6</td>
        <td>5</td>
        <td>23</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>16</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>5</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 20 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>6</td>
        <td>3</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 2&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>1</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>1</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 2 non è presente nell'array (restituisce $-1$).

<a id="esercizio-4-10"></a>

!!! esercizio "Esercizio 4.10: Ricerca lineare e ricerca binaria (E10)"

    Consideriamo il seguente array, ordinato in modo non decrescente:

    $$
    a = [3, 6, 9, 12, 15, 18, 21, 24, 27, 30]
    $$

    con $n = 10$.

    **Domande**

    1. Applicare l'algoritmo di ricerca binaria (Binary Search) all'array $a$ per ciascuno dei seguenti valori cercati:

        1. $m = 18$

        2. $m = 3$

        3. $m = 30$

        4. $m = 10$

        5. $m = 35$

        Per ogni ricerca, mostrare l'esecuzione passo per passo, indicando a ogni iterazione i valori di $left$, $right$, $mid$, $a[mid]$ e il risultato del confronto, e dare il valore restituito dall'algoritmo.

??? soluzione "Soluzione"

    1. Ricerca di $m = 18$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>6</td>
        <td>10</td>
        <td>8</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 7&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>6</td>
        <td>7</td>
        <td>6</td>
        <td>18</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 18 si trova all'indice 6.

    2. Ricerca di $m = 3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>4</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 3 si trova all'indice 1.

    3. Ricerca di $m = 30$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>6</td>
        <td>10</td>
        <td>8</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>9</td>
        <td>10</td>
        <td>9</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 10&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>10</td>
        <td>10</td>
        <td>10</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; = m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 30 si trova all'indice 10.

    4. Ricerca di $m = 10$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>1</td>
        <td>4</td>
        <td>2</td>
        <td>6</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>3</td>
        <td>4</td>
        <td>3</td>
        <td>9</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>12</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &gt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(right &#92;leftarrow 3&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>4</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 10 non è presente nell'array (restituisce $-1$).

    5. Ricerca di $m = 35$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(left&#92;)</span></th>
        <th><span class="arithmatex">&#92;(right&#92;)</span></th>
        <th><span class="arithmatex">&#92;(mid&#92;)</span></th>
        <th><span class="arithmatex">&#92;(a&#91;mid&#93;&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>1</td>
        <td>10</td>
        <td>5</td>
        <td>15</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>6</td>
        <td>10</td>
        <td>8</td>
        <td>24</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 9&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>9</td>
        <td>10</td>
        <td>9</td>
        <td>27</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 10&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>10</td>
        <td>10</td>
        <td>10</td>
        <td>30</td>
        <td><span class="arithmatex">&#92;(a&#91;mid&#93; &lt; m&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <span class="arithmatex">&#92;(left &#92;leftarrow 11&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>11</td>
        <td>10</td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(left &gt; right&#92;)</span> <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> Non trovato!</td>
        </tr>
        </table></div>

        Quindi, l'elemento 35 non è presente nell'array (restituisce $-1$).
