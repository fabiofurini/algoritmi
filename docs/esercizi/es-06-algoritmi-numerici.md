---
title: "Esercizi · Algoritmi numerici"
---

# Esercizi · Algoritmi numerici

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 6** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 6](../fondamenti/06-algoritmi-numerici.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-fondamenti.pdf)

</div>

Gli esercizi di questo capitolo applicano i quattro algoritmi del capitolo «Algoritmi numerici»: ChangeOfBase, BasicPrimalityTest e PrimalityTest, SieveOfEratosthenes, EuclideanAlgorithm. Nelle soluzioni si usano i seguenti fatti del capitolo.

!!! nota ""

    <strong>Divisione con resto.</strong> Per ogni numero naturale $n$ e ogni numero naturale $b \ge 1$:

    $$
    n = \lfloor n/b \rfloor \; b + (n \bmod b) \qquad \text{con} \qquad 0 \le n \bmod b < b .
    $$

    <strong>Cambio di base.</strong> Se $n = (d_{k-1} \dots d_1 d_0)_b$, allora $n \bmod b = d_0$ e $\lfloor n/b \rfloor = (d_{k-1} \dots d_1)_b$; il numero di cifre è $\lfloor \log_b n \rfloor + 1$. ChangeOfBase memorizza la cifra $d_{k-1}$ nell'elemento $d[k]$.

!!! nota ""

    <strong>Primalità.</strong> Un numero naturale $n \ge 2$ è primo se e solo se nessun numero naturale in $\{2, 3, \dots, \lfloor \sqrt{n} \rfloor\}$ è un divisore di $n$.

    <strong>Crivello.</strong> La marcatura dei multipli di un primo $p$ parte da $p^2$, e il ciclo esterno si ferma a $\lfloor \sqrt{n} \rfloor$. Nelle tabelle di esecuzione le celle blu sono gli elementi appena posti a $0$ e le celle rosse il valore corrente di $p$.

!!! nota ""

    <strong>Massimo comun divisore.</strong> Per ogni coppia di numeri naturali $n, m \ge 1$:

    $$
    \gcd(n, m) = \gcd(m,\ n \bmod m) \qquad \text{e} \qquad \gcd(n, 0) = n .
    $$

    Due numeri naturali sono coprimi se e solo se il loro massimo comun divisore è $1$.

<a id="esercizio-6-1"></a>

!!! esercizio "Esercizio 6.1: Algoritmi numerici (E1)"

    Consideriamo il seguente numero naturale, scritto come sequenza di cifre in base dieci:

    $$
    (16)_{10}
    $$

    **Domande**

    1. Convertire il numero in base $b=2$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    2. Convertire il numero in base $b=3$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    3. Convertire il numero in base $b=4$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    4. Convertire il numero in base $b=5$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    5. Convertire il numero in base $b=6$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

??? soluzione "Soluzione"

    1. Conversione di $16$ in base $b=2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $16$ in base $2$ è $(10000)_{2}$, con $nd = \lfloor \log_{2} 16 \rfloor + 1 = 5$ cifre.

    2. Conversione di $16$ in base $b=3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $16$ in base $3$ è $(121)_{3}$, con $nd = \lfloor \log_{3} 16 \rfloor + 1 = 3$ cifre.

    3. Conversione di $16$ in base $b=4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $16$ in base $4$ è $(100)_{4}$, con $nd = \lfloor \log_{4} 16 \rfloor + 1 = 3$ cifre.

    4. Conversione di $16$ in base $b=5$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $16$ in base $5$ è $(31)_{5}$, con $nd = \lfloor \log_{5} 16 \rfloor + 1 = 2$ cifre.

    5. Conversione di $16$ in base $b=6$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(16/6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2/6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $16$ in base $6$ è $(24)_{6}$, con $nd = \lfloor \log_{6} 16 \rfloor + 1 = 2$ cifre.

<a id="esercizio-6-2"></a>

!!! esercizio "Esercizio 6.2: Algoritmi numerici (E2)"

    Consideriamo il seguente numero naturale, scritto come sequenza di cifre in base dieci:

    $$
    (25)_{10}
    $$

    **Domande**

    1. Convertire il numero in base $b=2$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    2. Convertire il numero in base $b=3$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    3. Convertire il numero in base $b=4$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    4. Convertire il numero in base $b=5$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    5. Convertire il numero in base $b=7$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

??? soluzione "Soluzione"

    1. Conversione di $25$ in base $b=2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $25$ in base $2$ è $(11001)_{2}$, con $nd = \lfloor \log_{2} 25 \rfloor + 1 = 5$ cifre.

    2. Conversione di $25$ in base $b=3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $25$ in base $3$ è $(221)_{3}$, con $nd = \lfloor \log_{3} 25 \rfloor + 1 = 3$ cifre.

    3. Conversione di $25$ in base $b=4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $25$ in base $4$ è $(121)_{4}$, con $nd = \lfloor \log_{4} 25 \rfloor + 1 = 3$ cifre.

    4. Conversione di $25$ in base $b=5$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $25$ in base $5$ è $(100)_{5}$, con $nd = \lfloor \log_{5} 25 \rfloor + 1 = 3$ cifre.

    5. Conversione di $25$ in base $b=7$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $25$ in base $7$ è $(34)_{7}$, con $nd = \lfloor \log_{7} 25 \rfloor + 1 = 2$ cifre.

<a id="esercizio-6-3"></a>

!!! esercizio "Esercizio 6.3: Algoritmi numerici (E3)"

    Consideriamo il seguente numero naturale, scritto come sequenza di cifre in base dieci:

    $$
    (42)_{10}
    $$

    **Domande**

    1. Convertire il numero in base $b=2$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    2. Convertire il numero in base $b=3$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    3. Convertire il numero in base $b=5$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    4. Convertire il numero in base $b=6$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    5. Convertire il numero in base $b=8$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

??? soluzione "Soluzione"

    1. Conversione di $42$ in base $b=2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;6&#93; = d&#95;{5}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $42$ in base $2$ è $(101010)_{2}$, con $nd = \lfloor \log_{2} 42 \rfloor + 1 = 6$ cifre.

    2. Conversione di $42$ in base $b=3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(14/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $42$ in base $3$ è $(1120)_{3}$, con $nd = \lfloor \log_{3} 42 \rfloor + 1 = 4$ cifre.

    3. Conversione di $42$ in base $b=5$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $42$ in base $5$ è $(132)_{5}$, con $nd = \lfloor \log_{5} 42 \rfloor + 1 = 3$ cifre.

    4. Conversione di $42$ in base $b=6$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42/6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7/6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $42$ in base $6$ è $(110)_{6}$, con $nd = \lfloor \log_{6} 42 \rfloor + 1 = 3$ cifre.

    5. Conversione di $42$ in base $b=8$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $42$ in base $8$ è $(52)_{8}$, con $nd = \lfloor \log_{8} 42 \rfloor + 1 = 2$ cifre.

<a id="esercizio-6-4"></a>

!!! esercizio "Esercizio 6.4: Algoritmi numerici (E4)"

    Consideriamo il seguente numero naturale, scritto come sequenza di cifre in base dieci:

    $$
    (63)_{10}
    $$

    **Domande**

    1. Convertire il numero in base $b=2$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    2. Convertire il numero in base $b=4$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    3. Convertire il numero in base $b=7$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    4. Convertire il numero in base $b=8$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    5. Convertire il numero in base $b=9$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

??? soluzione "Soluzione"

    1. Conversione di $63$ in base $b=2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31&#92;)</span></td>
        <td><span class="arithmatex">&#92;(31/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;6&#93; = d&#95;{5}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $63$ in base $2$ è $(111111)_{2}$, con $nd = \lfloor \log_{2} 63 \rfloor + 1 = 6$ cifre.

    2. Conversione di $63$ in base $b=4$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $63$ in base $4$ è $(333)_{4}$, con $nd = \lfloor \log_{4} 63 \rfloor + 1 = 3$ cifre.

    3. Conversione di $63$ in base $b=7$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63/7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9/7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $63$ in base $7$ è $(120)_{7}$, con $nd = \lfloor \log_{7} 63 \rfloor + 1 = 3$ cifre.

    4. Conversione di $63$ in base $b=8$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $63$ in base $8$ è $(77)_{8}$, con $nd = \lfloor \log_{8} 63 \rfloor + 1 = 2$ cifre.

    5. Conversione di $63$ in base $b=9$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63&#92;)</span></td>
        <td><span class="arithmatex">&#92;(63/9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7/9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $63$ in base $9$ è $(70)_{9}$, con $nd = \lfloor \log_{9} 63 \rfloor + 1 = 2$ cifre.

<a id="esercizio-6-5"></a>

!!! esercizio "Esercizio 6.5: Algoritmi numerici (E5)"

    Consideriamo il seguente numero naturale, scritto come sequenza di cifre in base dieci:

    $$
    (100)_{10}
    $$

    **Domande**

    1. Convertire il numero in base $b=2$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    2. Convertire il numero in base $b=3$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    3. Convertire il numero in base $b=5$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    4. Convertire il numero in base $b=8$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

    5. Convertire il numero in base $b=16$ con l'algoritmo ChangeOfBase, mostrando il quoziente e il resto di ogni divisione.

??? soluzione "Soluzione"

    1. Conversione di $100$ in base $b=2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(50&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(50&#92;)</span></td>
        <td><span class="arithmatex">&#92;(50/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(25/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;6&#93; = d&#95;{5}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;7&#93; = d&#95;{6}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $100$ in base $2$ è $(1100100)_{2}$, con $nd = \lfloor \log_{2} 100 \rfloor + 1 = 7$ cifre.

    2. Conversione di $100$ in base $b=3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(33&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(33&#92;)</span></td>
        <td><span class="arithmatex">&#92;(33/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;5&#93; = d&#95;{4}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $100$ in base $3$ è $(10201)_{3}$, con $nd = \lfloor \log_{3} 100 \rfloor + 1 = 5$ cifre.

    3. Conversione di $100$ in base $b=5$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        <td><span class="arithmatex">&#92;(20/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4/5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $100$ in base $5$ è $(400)_{5}$, con $nd = \lfloor \log_{5} 100 \rfloor + 1 = 3$ cifre.

    4. Conversione di $100$ in base $b=8$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $100$ in base $8$ è $(144)_{8}$, con $nd = \lfloor \log_{8} 100 \rfloor + 1 = 3$ cifre.

    5. Conversione di $100$ in base $b=16$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione <span class="arithmatex">&#92;(k&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n/b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(q&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r&#92;)</span></th>
        <th>cifra</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(100/16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6/16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $100$ in base $16$ è $(64)_{16}$, con $nd = \lfloor \log_{16} 100 \rfloor + 1 = 2$ cifre.

<a id="esercizio-6-6"></a>

!!! esercizio "Esercizio 6.6: Algoritmi numerici (E6)"

    Consideriamo i seguenti numeri naturali:

    $$
    n \in \{2,\ 7,\ 9,\ 11,\ 25\}
    $$

    **Domande**

    1. Applicare l'algoritmo PrimalityTest a ciascun numero della lista. Per ogni $n$ mostrare l'esecuzione passo per passo, indicando il valore di $\lfloor\sqrt{n}\rfloor$, i valori di $d$ provati e il risultato di ciascun test $n \bmod d = 0$.

??? soluzione "Soluzione"

    1. Esecuzione di PrimalityTest su ciascun numero.

        <strong>Verifica $n = 2$:</strong> $\lfloor\sqrt{2}\rfloor = 1$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(2 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td colspan="3">Il ciclo non viene eseguito, poiché <span class="arithmatex">&#92;(2 &gt; 1&#92;)</span>.</td>
        </tr>
        <tr>
        <td colspan="3">Restituisce <code>true</code>: <strong>2 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 7$:</strong> $\lfloor\sqrt{7}\rfloor = 2$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(7 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>7 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 9$:</strong> $\lfloor\sqrt{9}\rfloor = 3$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(9 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>9 non è primo</strong> (<span class="arithmatex">&#92;(9 = 3 &#92;cdot 3&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 11$:</strong> $\lfloor\sqrt{11}\rfloor = 3$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(11 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>11 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 25$:</strong> $\lfloor\sqrt{25}\rfloor = 5$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(25 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>25 non è primo</strong> (<span class="arithmatex">&#92;(25 = 5 &#92;cdot 5&#92;)</span>).</td>
        </tr>
        </table></div>

<a id="esercizio-6-7"></a>

!!! esercizio "Esercizio 6.7: Algoritmi numerici (E7)"

    Consideriamo i seguenti numeri naturali:

    $$
    n \in \{4,\ 13,\ 17,\ 49,\ 97\}
    $$

    **Domande**

    1. Applicare l'algoritmo PrimalityTest a ciascun numero della lista. Per ogni $n$ mostrare l'esecuzione passo per passo, indicando il valore di $\lfloor\sqrt{n}\rfloor$, i valori di $d$ provati e il risultato di ciascun test $n \bmod d = 0$.

??? soluzione "Soluzione"

    1. Esecuzione di PrimalityTest su ciascun numero.

        <strong>Verifica $n = 4$:</strong> $\lfloor\sqrt{4}\rfloor = 2$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(4 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>4 non è primo</strong> (<span class="arithmatex">&#92;(4 = 2 &#92;cdot 2&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 13$:</strong> $\lfloor\sqrt{13}\rfloor = 3$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(13 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>13 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 17$:</strong> $\lfloor\sqrt{17}\rfloor = 4$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(17 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>17 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 49$:</strong> $\lfloor\sqrt{49}\rfloor = 7$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(49 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>49 non è primo</strong> (<span class="arithmatex">&#92;(49 = 7 &#92;cdot 7&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 97$:</strong> $\lfloor\sqrt{97}\rfloor = 9$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(97 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>97 è primo</strong>.</td>
        </tr>
        </table></div>

<a id="esercizio-6-8"></a>

!!! esercizio "Esercizio 6.8: Algoritmi numerici (E8)"

    Consideriamo i seguenti numeri naturali:

    $$
    n \in \{1,\ 3,\ 15,\ 23,\ 36\}
    $$

    **Domande**

    1. Applicare l'algoritmo PrimalityTest a ciascun numero della lista. Per ogni $n$ mostrare l'esecuzione passo per passo, indicando il valore di $\lfloor\sqrt{n}\rfloor$, i valori di $d$ provati e il risultato di ciascun test $n \bmod d = 0$.

??? soluzione "Soluzione"

    1. Esecuzione di PrimalityTest su ciascun numero.

        <strong>Verifica $n = 1$:</strong> $n < 2$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(1 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td colspan="3"><span class="arithmatex">&#92;(n = 1 &lt; 2&#92;)</span>: restituisce <code>false</code> immediately.</td>
        </tr>
        <tr>
        <td colspan="3"><strong>1 non è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 3$:</strong> $\lfloor\sqrt{3}\rfloor = 1$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(3 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td colspan="3">Il ciclo non viene eseguito, poiché <span class="arithmatex">&#92;(2 &gt; 1&#92;)</span>.</td>
        </tr>
        <tr>
        <td colspan="3">Restituisce <code>true</code>: <strong>3 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 15$:</strong> $\lfloor\sqrt{15}\rfloor = 3$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(15 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>15 non è primo</strong> (<span class="arithmatex">&#92;(15 = 3 &#92;cdot 5&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 23$:</strong> $\lfloor\sqrt{23}\rfloor = 4$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(23 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>23 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 36$:</strong> $\lfloor\sqrt{36}\rfloor = 6$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(36 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>36 non è primo</strong> (<span class="arithmatex">&#92;(36 = 2 &#92;cdot 18&#92;)</span>).</td>
        </tr>
        </table></div>

<a id="esercizio-6-9"></a>

!!! esercizio "Esercizio 6.9: Algoritmi numerici (E9)"

    Consideriamo i numeri naturali $n = 29$ e $n = 49$.

    **Domande**

    1. Per ciascun numero $n$, applicare sia l'algoritmo BasicPrimalityTest (ciclo fino a $\lfloor n/2 \rfloor$) sia l'algoritmo PrimalityTest (ciclo fino a $\lfloor\sqrt{n}\rfloor$). Mostrare l'esecuzione passo per passo di ciascun algoritmo.

    2. Per ciascun numero, contare il numero di iterazioni eseguite da ciascun algoritmo e confrontarle.

??? soluzione "Soluzione"

    1. Esecuzione passo per passo.

        <strong>Caso $n = 29$.</strong>

        <em>BasicPrimalityTest</em> ($\lfloor 29/2 \rfloor = 14$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(29 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(13&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>29 è primo</strong>. (13 iterazioni)</td>
        </tr>
        </table></div>

        <em>PrimalityTest</em> ($\lfloor\sqrt{29}\rfloor = 5$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(29 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>29 è primo</strong>. (4 iterazioni)</td>
        </tr>
        </table></div>

        <strong>Caso $n = 49$.</strong>

        <em>BasicPrimalityTest</em> ($\lfloor 49/2 \rfloor = 24$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(49 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>49 non è primo</strong> (<span class="arithmatex">&#92;(49 = 7 &#92;cdot 7&#92;)</span>). (6 iterazioni)</td>
        </tr>
        </table></div>

        <em>PrimalityTest</em> ($\lfloor\sqrt{49}\rfloor = 7$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(49 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>49 non è primo</strong> (<span class="arithmatex">&#92;(49 = 7 &#92;cdot 7&#92;)</span>). (6 iterazioni)</td>
        </tr>
        </table></div>

    2. Confronto delle iterazioni:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;lfloor n/2 &#92;rfloor&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span></th>
        <th>BasicPrimalityTest</th>
        <th>PrimalityTest</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(29&#92;)</span></td>
        <td><span class="arithmatex">&#92;(14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(13&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(49&#92;)</span></td>
        <td><span class="arithmatex">&#92;(24&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        </tr>
        </table></div>

        Per $n = 29$ (primo), PrimalityTest esegue solo $4$ iterazioni invece di $13$: entrambi gli algoritmi devono provare tutti i loro candidati, e PrimalityTest ne ha molti meno. Per $n = 49$ (composto, con il più piccolo divisore $7 = \sqrt{49}$), entrambi gli algoritmi si fermano allo stesso divisore $d = 7$, quindi il numero di iterazioni è lo stesso.

<a id="esercizio-6-10"></a>

!!! esercizio "Esercizio 6.10: Algoritmi numerici (E10)"

    Consideriamo i numeri naturali $n \in \{2, 3, 4, \dots, 30\}$.

    **Domande**

    1. Applicare l'algoritmo PrimalityTest a ciascun numero naturale $n \in \{2, 3, \dots, 30\}$ e determinare quali numeri sono primi. Per ogni $n$ riportare il valore di $\lfloor\sqrt{n}\rfloor$, se è stato trovato un divisore (e quale) e il risultato.

    2. Elencare tutti i numeri primi in $\{2, 3, \dots, 30\}$ e contarli.

??? soluzione "Soluzione"

    1. Riepilogo delle esecuzioni di PrimalityTest (il divisore riportato è il primo trovato, cioè il valore di $d$ per cui la funzione restituisce <code>false</code>):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span></th>
        <th>primo divisore trovato</th>
        <th>risultato</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>nessuno (ciclo non eseguito)</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>nessuno (ciclo non eseguito)</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(4 = 2 &#92;cdot 2&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(6 = 2 &#92;cdot 3&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(8 = 2 &#92;cdot 4&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 3&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(9 = 3 &#92;cdot 3&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(10 = 2 &#92;cdot 5&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(12 = 2 &#92;cdot 6&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(13&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(14&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(14 = 2 &#92;cdot 7&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(15&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 3&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(15 = 3 &#92;cdot 5&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(16&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(16 = 2 &#92;cdot 8&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(17&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(18 = 2 &#92;cdot 9&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(19&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(20&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(20 = 2 &#92;cdot 10&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 3&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(21 = 3 &#92;cdot 7&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(22&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(22 = 2 &#92;cdot 11&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(23&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(24&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(24 = 2 &#92;cdot 12&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 5&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(25 = 5 &#92;cdot 5&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(26&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(26 = 2 &#92;cdot 13&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(27&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 3&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(27 = 3 &#92;cdot 9&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(28&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(28 = 2 &#92;cdot 14&#92;)</span>)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(29&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td>nessuno</td>
        <td><strong>primo</strong></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(30&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
        <td>non primo (<span class="arithmatex">&#92;(30 = 2 &#92;cdot 15&#92;)</span>)</td>
        </tr>
        </table></div>

    2. I numeri primi in $\{2, 3, \dots, 30\}$ sono

        $$
        2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19,\ 23,\ 29
        $$

        Ci sono $10$ numeri primi in $\{2, 3, \dots, 30\}$.

<a id="esercizio-6-11"></a>

!!! esercizio "Esercizio 6.11: Algoritmi numerici (E11)"

    Consideriamo i seguenti numeri naturali:

    $$
    n \in \{6,\ 19,\ 49,\ 53,\ 91\}
    $$

    **Domande**

    1. Applicare l'algoritmo PrimalityTest a ciascun numero della lista. Per ogni $n$ mostrare l'esecuzione passo per passo, indicando il valore di $\lfloor\sqrt{n}\rfloor$, i valori di $d$ provati e il risultato di ciascun test $n \bmod d = 0$.

??? soluzione "Soluzione"

    1. Esecuzione di PrimalityTest su ciascun numero.

        <strong>Verifica $n = 6$:</strong> $\lfloor\sqrt{6}\rfloor = 2$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(6 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>6 non è primo</strong> (<span class="arithmatex">&#92;(6 = 2 &#92;cdot 3&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 19$:</strong> $\lfloor\sqrt{19}\rfloor = 4$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(19 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>19 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 49$:</strong> $\lfloor\sqrt{49}\rfloor = 7$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(49 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>49 non è primo</strong> (<span class="arithmatex">&#92;(49 = 7 &#92;cdot 7&#92;)</span>).</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 53$:</strong> $\lfloor\sqrt{53}\rfloor = 7$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(53 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>53 è primo</strong>.</td>
        </tr>
        </table></div>

        <strong>Verifica $n = 91$:</strong> $\lfloor\sqrt{91}\rfloor = 9$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(d&#92;)</span></th>
        <th><span class="arithmatex">&#92;(91 &#92;bmod d&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td>continua</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>restituisce <code>false</code></td>
        </tr>
        <tr>
        <td colspan="3"><strong>91 non è primo</strong> (<span class="arithmatex">&#92;(91 = 7 &#92;cdot 13&#92;)</span>).</td>
        </tr>
        </table></div>

<a id="esercizio-6-12"></a>

!!! esercizio "Esercizio 6.12: Algoritmi numerici (E12)"

    Consideriamo il numero naturale $n = 15$.

    **Domande**

    1. Applicare l'algoritmo SieveOfEratosthenes con $n = 15$. Mostrare l'esecuzione passo per passo: indicare il valore di $\lfloor\sqrt{15}\rfloor$ e, per ogni primo $p$ trovato, elencare i valori di $j$ nel ciclo interno e i corrispondenti assegnamenti $prime[j] \leftarrow 0$.

    2. Elencare tutti i numeri primi $\le 15$.

??? soluzione "Soluzione"

    1. Si ha $n = 15$ e $\lfloor\sqrt{15}\rfloor = 3$. L'array $prime[1..15]$ è inizializzato a $1$ e poi $prime[1] \leftarrow 0$. Ogni riga della tabella mostra lo stato dell'array dopo l'assegnamento $prime[j] \leftarrow 0$ (blu: elemento appena posto a $0$; rosso: valore corrente di $p$).

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th></th>
        <th colspan="15"><span class="arithmatex">&#92;(prime&#91;1..15&#93;&#92;)</span></th>
        <th></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(p&#92;)</span></td>
        <td><span class="arithmatex">&#92;(j&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
        <td>14</td>
        <td>15</td>
        <td>azione</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>inizializzazione</td>
        </tr>
        <tr>
        <td class="cella-rossa">2</td>
        <td>4</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;4&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;6&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;8&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>10</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>12</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>14</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;14&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>16</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(j = 16 &gt; 15&#92;)</span>: arresto</td>
        </tr>
        <tr>
        <td class="cella-rossa">3</td>
        <td>9</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td class="cella-blu">0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>12</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span> (già <span class="arithmatex">&#92;(0&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>15</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td class="cella-blu">0</td>
        <td><span class="arithmatex">&#92;(prime&#91;15&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>18</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(j = 18 &gt; 15&#92;)</span>: arresto</td>
        </tr>
        <tr>
        <td colspan="18">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 4 &gt; &#92;lfloor&#92;sqrt{15}&#92;rfloor = 3&#92;)</span>.</td>
        </tr>
        </table></div>

    2. I numeri primi $\le 15$ sono $2,\ 3,\ 5,\ 7,\ 11,\ 13$.

<a id="esercizio-6-13"></a>

!!! esercizio "Esercizio 6.13: Algoritmi numerici (E13)"

    Consideriamo il numero naturale $n = 30$.

    **Domande**

    1. Applicare l'algoritmo SieveOfEratosthenes con $n = 30$. Mostrare l'esecuzione passo per passo: indicare il valore di $\lfloor\sqrt{30}\rfloor$ e, per ogni primo $p$ trovato, elencare i valori di $j$ nel ciclo interno e i corrispondenti assegnamenti $prime[j] \leftarrow 0$.

    2. Elencare tutti i numeri primi $\le 30$.

??? soluzione "Soluzione"

    1. Si ha $n = 30$ e $\lfloor\sqrt{30}\rfloor = 5$. L'array $prime[1..30]$ è inizializzato a $1$ e poi $prime[1] \leftarrow 0$.

        - <strong>Iterazione $p = 2$</strong>: $prime[2] = 1$, quindi $2$ è primo. Ciclo interno da $j = p^2 = 4$ con passo $2$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;4&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(6&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;6&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(8&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;8&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(10&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(12&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(14&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;14&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(16&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;16&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(18&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(20&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;20&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(22&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;22&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;24&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(26&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;26&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(28&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;28&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;30&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(32&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 32 &gt; 30&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - <strong>Iterazione $p = 3$</strong>: $prime[3] = 1$, quindi $3$ è primo. Ciclo interno da $j = p^2 = 9$ con passo $3$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(9&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(12&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(15&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;15&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(18&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;21&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;24&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(27&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;27&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;30&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(33&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 33 &gt; 30&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - <strong>Iterazione $p = 4$</strong>: $prime[4] = 0$, quindi $4$ non è primo: si salta.

        - <strong>Iterazione $p = 5$</strong>: $prime[5] = 1$, quindi $5$ è primo. Ciclo interno da $j = p^2 = 25$ con passo $5$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(25&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;25&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;30&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(35&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 35 &gt; 30&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - Il ciclo esterno termina: $p = 6 > \lfloor\sqrt{30}\rfloor = 5$.

        Stato finale dell'array $prime[1..30]$ (gli elementi uguali a $1$ sono in blu):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
        <th>7</th>
        <th>8</th>
        <th>9</th>
        <th>10</th>
        <th>11</th>
        <th>12</th>
        <th>13</th>
        <th>14</th>
        <th>15</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(i&#92;)</span></td>
        <td>16</td>
        <td>17</td>
        <td>18</td>
        <td>19</td>
        <td>20</td>
        <td>21</td>
        <td>22</td>
        <td>23</td>
        <td>24</td>
        <td>25</td>
        <td>26</td>
        <td>27</td>
        <td>28</td>
        <td>29</td>
        <td>30</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        </tr>
        </table></div>

    2. I numeri primi $\le 30$ sono $2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19,\ 23,\ 29$.

<a id="esercizio-6-14"></a>

!!! esercizio "Esercizio 6.14: Algoritmi numerici (E14)"

    Consideriamo la seguente traccia di esecuzione dell'algoritmo SieveOfEratosthenes per $n = 12$, in cui alcuni elementi sono stati sostituiti da un punto interrogativo.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th></th>
    <th colspan="12"><span class="arithmatex">&#92;(prime&#91;1..12&#93;&#92;)</span></th>
    <th></th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(p&#92;)</span></td>
    <td><span class="arithmatex">&#92;(j&#92;)</span></td>
    <td>1</td>
    <td>2</td>
    <td>3</td>
    <td>4</td>
    <td>5</td>
    <td>6</td>
    <td>7</td>
    <td>8</td>
    <td>9</td>
    <td>10</td>
    <td>11</td>
    <td>12</td>
    <td>azione</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(-&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-&#92;)</span></td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>inizializzazione</td>
    </tr>
    <tr>
    <td class="cella-rossa">2</td>
    <td>4</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>?</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;4&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>6</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>?</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;6&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>8</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>?</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;8&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>10</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>?</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>12</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>?</td>
    <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>14</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">&#92;(j = 14 &gt; 12&#92;)</span>: arresto</td>
    </tr>
    <tr>
    <td class="cella-rossa">3</td>
    <td>9</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>?</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>12</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>?</td>
    <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span> (già <span class="arithmatex">&#92;(0&#92;)</span>)</td>
    </tr>
    <tr>
    <td></td>
    <td>15</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">&#92;(j = 15 &gt; 12&#92;)</span>: arresto</td>
    </tr>
    <tr>
    <td colspan="15">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 4 &gt; &#92;lfloor&#92;sqrt{12}&#92;rfloor = ?&#92;)</span>.</td>
    </tr>
    </table></div>

    **Domande**

    1. Completare tutti gli elementi contrassegnati da un punto interrogativo nella tabella.

    2. Qual è il valore di $\lfloor\sqrt{12}\rfloor$? Perché il ciclo esterno può fermarsi quando $p = 4$?

    3. Elencare tutti i numeri primi $\le 12$.

??? soluzione "Soluzione"

    1. Tabella completata:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th></th>
        <th colspan="12"><span class="arithmatex">&#92;(prime&#91;1..12&#93;&#92;)</span></th>
        <th></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(p&#92;)</span></td>
        <td><span class="arithmatex">&#92;(j&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>azione</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td><span class="arithmatex">&#92;(-&#92;)</span></td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>inizializzazione</td>
        </tr>
        <tr>
        <td class="cella-rossa">2</td>
        <td>4</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;4&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>6</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;6&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>8</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;8&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>10</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>12</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>14</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(j = 14 &gt; 12&#92;)</span>: arresto</td>
        </tr>
        <tr>
        <td class="cella-rossa">3</td>
        <td>9</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td class="cella-blu">0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
        </tr>
        <tr>
        <td></td>
        <td>12</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span> (già <span class="arithmatex">&#92;(0&#92;)</span>)</td>
        </tr>
        <tr>
        <td></td>
        <td>15</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(j = 15 &gt; 12&#92;)</span>: arresto</td>
        </tr>
        <tr>
        <td colspan="15">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 4 &gt; &#92;lfloor&#92;sqrt{12}&#92;rfloor = 3&#92;)</span>.</td>
        </tr>
        </table></div>

        Ogni punto interrogativo è l'elemento $prime[j]$ della riga di indice $j$: vale $0$ dopo l'assegnamento $prime[j] \leftarrow 0$ (nella riga $p = 3$, $j = 12$, l'elemento era già $0$).

    2. $\lfloor\sqrt{12}\rfloor = 3$. Il ciclo esterno viene eseguito per $p = 2, 3$ e si ferma quando $p = 4 > 3$. Ogni numero composto $m \le 12$ ha un divisore primo non maggiore di $\lfloor\sqrt{12}\rfloor = 3$ (capitolo «Algoritmi numerici», sezione «Crivello di Eratostene»), quindi tutti i numeri composti sono già stati marcati: $4, 6, 8, 10, 12$ da $p = 2$ e $9$ da $p = 3$.

    3. I numeri primi $\le 12$ sono $2,\ 3,\ 5,\ 7,\ 11$.

<a id="esercizio-6-15"></a>

!!! esercizio "Esercizio 6.15: Algoritmi numerici (E15)"

    Consideriamo l'algoritmo SieveOfEratosthenes applicato a $n = 25$.

    **Domande**

    1. Applicare l'algoritmo SieveOfEratosthenes con $n = 25$. Mostrare l'esecuzione passo per passo, indicando il valore di $\lfloor\sqrt{25}\rfloor$ e, per ogni primo $p$, i valori di $j$ provati nel ciclo interno e i corrispondenti assegnamenti $prime[j] \leftarrow 0$.

    2. Per $p = 5$: qual è il primo valore di $j$ elaborato dal ciclo interno? Perché il punto di partenza è $p^2 = 25$ e non $2p = 10$?

    3. Elencare tutti i numeri primi $\le 25$.

??? soluzione "Soluzione"

    1. Si ha $n = 25$ e $\lfloor\sqrt{25}\rfloor = 5$. L'array $prime[1..25]$ è inizializzato a $1$ e poi $prime[1] \leftarrow 0$.

        - <strong>Iterazione $p = 2$</strong>: $prime[2] = 1$, quindi $2$ è primo. Ciclo interno da $j = p^2 = 4$ con passo $2$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;4&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(6&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;6&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(8&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;8&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(10&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(12&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(14&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;14&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(16&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;16&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(18&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(20&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;20&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(22&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;22&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;24&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(26&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 26 &gt; 25&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - <strong>Iterazione $p = 3$</strong>: $prime[3] = 1$, quindi $3$ è primo. Ciclo interno da $j = p^2 = 9$ con passo $3$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(9&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(12&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;12&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(15&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;15&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(18&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;21&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;24&#93; &#92;leftarrow 0&#92;)</span></td>
            <td>già <span class="arithmatex">&#92;(0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(27&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 27 &gt; 25&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - <strong>Iterazione $p = 4$</strong>: $prime[4] = 0$, quindi $4$ non è primo: si salta.

        - <strong>Iterazione $p = 5$</strong>: $prime[5] = 1$, quindi $5$ è primo. Ciclo interno da $j = p^2 = 25$ con passo $5$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th><span class="arithmatex">&#92;(j&#92;)</span></th>
            <th>assegnamento</th>
            <th>nota</th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(25&#92;)</span></td>
            <td><span class="arithmatex">&#92;(prime&#91;25&#93; &#92;leftarrow 0&#92;)</span></td>
            <td></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td></td>
            <td><span class="arithmatex">&#92;(j = 30 &gt; 25&#92;)</span>: arresto</td>
            </tr>
            </table></div>

        - Il ciclo esterno termina: $p = 6 > \lfloor\sqrt{25}\rfloor = 5$.

        Stato finale dell'array $prime[1..25]$ (gli elementi uguali a $1$ sono in blu):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
        <th>7</th>
        <th>8</th>
        <th>9</th>
        <th>10</th>
        <th>11</th>
        <th>12</th>
        <th>13</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(i&#92;)</span></td>
        <td>14</td>
        <td>15</td>
        <td>16</td>
        <td>17</td>
        <td>18</td>
        <td>19</td>
        <td>20</td>
        <td>21</td>
        <td>22</td>
        <td>23</td>
        <td>24</td>
        <td>25</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td></td>
        </tr>
        </table></div>

    2. Per $p = 5$, il ciclo interno parte da $j = p^2 = 25$. Tutti i multipli più piccoli di $5$ maggiori di $5$, cioè $10, 15, 20$, sono già stati posti a $0$: $10 = 2 \cdot 5$ e $20 = 2 \cdot 10$ quando $p = 2$, e $15 = 3 \cdot 5$ quando $p = 3$. In generale, ogni multiplo $m$ di $p$ con $p < m < p^2$ ha un divisore $d$ con $2 \le d < p$, quindi un divisore primo minore di $p$, che lo ha già marcato.

    3. I numeri primi $\le 25$ sono $2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19,\ 23$.

<a id="esercizio-6-16"></a>

!!! esercizio "Esercizio 6.16: Algoritmi numerici (E16)"

    Consideriamo il numero naturale $n = 50$.

    **Domande**

    1. Applicare l'algoritmo SieveOfEratosthenes con $n = 50$. Per ogni valore di $p$ del ciclo esterno riportare il valore di $prime[p]$ e, quando $p$ è primo, tutti i valori di $j$ elaborati dal ciclo interno (i multipli di $p$ da $p^2$ a $50$), distinguendo gli elementi posti a $0$ per la prima volta da quelli già uguali a $0$.

    2. Elencare tutti i numeri primi $\le 50$ e contarli.

??? soluzione "Soluzione"

    1. Si ha $n = 50$ e $\lfloor\sqrt{50}\rfloor = 7$. L'array $prime[1..50]$ è inizializzato a $1$ e poi $prime[1] \leftarrow 0$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(p&#92;)</span></th>
        <th><span class="arithmatex">&#92;(prime&#91;p&#93;&#92;)</span></th>
        <th>valori di <span class="arithmatex">&#92;(j&#92;)</span></th>
        <th>posti a <span class="arithmatex">&#92;(0&#92;)</span> ora</th>
        <th>già <span class="arithmatex">&#92;(0&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (primo)</td>
        <td><span class="arithmatex">&#92;(4, 6, &#92;dots, 50&#92;)</span></td>
        <td>4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50</td>
        <td>—</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (primo)</td>
        <td><span class="arithmatex">&#92;(9, 12, &#92;dots, 48&#92;)</span></td>
        <td>9, 15, 21, 27, 33, 39, 45</td>
        <td>12, 18, 24, 30, 36, 42, 48</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (salta)</td>
        <td>—</td>
        <td>—</td>
        <td>—</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (primo)</td>
        <td><span class="arithmatex">&#92;(25, 30, &#92;dots, 50&#92;)</span></td>
        <td>25, 35</td>
        <td>30, 40, 45, 50</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (salta)</td>
        <td>—</td>
        <td>—</td>
        <td>—</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (primo)</td>
        <td><span class="arithmatex">&#92;(49&#92;)</span></td>
        <td>49</td>
        <td>—</td>
        </tr>
        <tr>
        <td colspan="5">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 8 &gt; &#92;lfloor&#92;sqrt{50}&#92;rfloor = 7&#92;)</span>.</td>
        </tr>
        </table></div>

        Stato finale dell'array $prime[1..50]$ (gli elementi uguali a $1$ sono in blu):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(i&#92;)</span></th>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
        <th>7</th>
        <th>8</th>
        <th>9</th>
        <th>10</th>
        <th>11</th>
        <th>12</th>
        <th>13</th>
        <th>14</th>
        <th>15</th>
        <th>16</th>
        <th>17</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(i&#92;)</span></td>
        <td>18</td>
        <td>19</td>
        <td>20</td>
        <td>21</td>
        <td>22</td>
        <td>23</td>
        <td>24</td>
        <td>25</td>
        <td>26</td>
        <td>27</td>
        <td>28</td>
        <td>29</td>
        <td>30</td>
        <td>31</td>
        <td>32</td>
        <td>33</td>
        <td>34</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(i&#92;)</span></td>
        <td>35</td>
        <td>36</td>
        <td>37</td>
        <td>38</td>
        <td>39</td>
        <td>40</td>
        <td>41</td>
        <td>42</td>
        <td>43</td>
        <td>44</td>
        <td>45</td>
        <td>46</td>
        <td>47</td>
        <td>48</td>
        <td>49</td>
        <td>50</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(prime&#91;i&#93;&#92;)</span></td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td></td>
        </tr>
        </table></div>

    2. I numeri primi $\le 50$ sono

        $$
        2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19,\ 23,\ 29,\ 31,\ 37,\ 41,\ 43,\ 47
        $$

        Ci sono $15$ numeri primi $\le 50$.

<a id="esercizio-6-17"></a>

!!! esercizio "Esercizio 6.17: Algoritmi numerici (E17)"

    Consideriamo le seguenti coppie di numeri naturali $(n,m)$:

    1. $(1071,\ 462)$

    2. $(100,\ 75)$

    3. $(17,\ 5)$

    4. $(89,\ 55)$

    5. $(30,\ 84)$

    **Domande**

    1. Applicare l'algoritmo EuclideanAlgorithm per calcolare $\gcd(n,m)$ per tutte le coppie. Per ogni coppia mostrare l'esecuzione passo per passo in una tabella, indicando a ogni passo i valori di $n$, $m$ e $r=n\bmod m$, e dare il numero di iterazioni del ciclo while.

    2. Quali coppie sono coprime?

    3. Nella coppia 5 si ha $n<m$. Che cosa accade nella prima iterazione?

??? soluzione "Soluzione"

    1. Esecuzioni dell'algoritmo di Euclide.

        1. Calcoliamo $\gcd(1071,462)$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th>passo</th>
            <th><span class="arithmatex">&#92;(n&#92;)</span></th>
            <th><span class="arithmatex">&#92;(m&#92;)</span></th>
            <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1071&#92;)</span></td>
            <td><span class="arithmatex">&#92;(462&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1071 &#92;bmod 462 = 147&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(462&#92;)</span></td>
            <td><span class="arithmatex">&#92;(147&#92;)</span></td>
            <td><span class="arithmatex">&#92;(462 &#92;bmod 147 = 21&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(147&#92;)</span></td>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(147 &#92;bmod 21 = 0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(0&#92;)</span></td>
            <td>— (il ciclo termina)</td>
            </tr>
            </table></div>

            <strong>Risultato:</strong> $\gcd(1071, 462) = 21$, con $3$ iterazioni del ciclo while.

        2. Calcoliamo $\gcd(100,75)$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th>passo</th>
            <th><span class="arithmatex">&#92;(n&#92;)</span></th>
            <th><span class="arithmatex">&#92;(m&#92;)</span></th>
            <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(100&#92;)</span></td>
            <td><span class="arithmatex">&#92;(75&#92;)</span></td>
            <td><span class="arithmatex">&#92;(100 &#92;bmod 75 = 25&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(75&#92;)</span></td>
            <td><span class="arithmatex">&#92;(25&#92;)</span></td>
            <td><span class="arithmatex">&#92;(75 &#92;bmod 25 = 0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(25&#92;)</span></td>
            <td><span class="arithmatex">&#92;(0&#92;)</span></td>
            <td>— (il ciclo termina)</td>
            </tr>
            </table></div>

            <strong>Risultato:</strong> $\gcd(100, 75) = 25$, con $2$ iterazioni del ciclo while.

        3. Calcoliamo $\gcd(17,5)$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th>passo</th>
            <th><span class="arithmatex">&#92;(n&#92;)</span></th>
            <th><span class="arithmatex">&#92;(m&#92;)</span></th>
            <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(17&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(17 &#92;bmod 5 = 2&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5 &#92;bmod 2 = 1&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2 &#92;bmod 1 = 0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(0&#92;)</span></td>
            <td>— (il ciclo termina)</td>
            </tr>
            </table></div>

            <strong>Risultato:</strong> $\gcd(17, 5) = 1$, con $3$ iterazioni del ciclo while.

        4. Calcoliamo $\gcd(89,55)$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th>passo</th>
            <th><span class="arithmatex">&#92;(n&#92;)</span></th>
            <th><span class="arithmatex">&#92;(m&#92;)</span></th>
            <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(89&#92;)</span></td>
            <td><span class="arithmatex">&#92;(55&#92;)</span></td>
            <td><span class="arithmatex">&#92;(89 &#92;bmod 55 = 34&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(55&#92;)</span></td>
            <td><span class="arithmatex">&#92;(34&#92;)</span></td>
            <td><span class="arithmatex">&#92;(55 &#92;bmod 34 = 21&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(34&#92;)</span></td>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(34 &#92;bmod 21 = 13&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(21&#92;)</span></td>
            <td><span class="arithmatex">&#92;(13&#92;)</span></td>
            <td><span class="arithmatex">&#92;(21 &#92;bmod 13 = 8&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(13&#92;)</span></td>
            <td><span class="arithmatex">&#92;(8&#92;)</span></td>
            <td><span class="arithmatex">&#92;(13 &#92;bmod 8 = 5&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(6&#92;)</span></td>
            <td><span class="arithmatex">&#92;(8&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(8 &#92;bmod 5 = 3&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(7&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(5 &#92;bmod 3 = 2&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(8&#92;)</span></td>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(3 &#92;bmod 2 = 1&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(9&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(2 &#92;bmod 1 = 0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(10&#92;)</span></td>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(0&#92;)</span></td>
            <td>— (il ciclo termina)</td>
            </tr>
            </table></div>

            <strong>Risultato:</strong> $\gcd(89, 55) = 1$, con $9$ iterazioni del ciclo while.

            I numeri $89, 55, 34, 21, 13, 8, 5, 3, 2, 1$ sono numeri di Fibonacci consecutivi: a ogni passo il quoziente è $1$, e i resti decrescono più lentamente possibile.

        5. Calcoliamo $\gcd(30,84)$:

            <div class="tabella" markdown="0"><table>
            <tr>
            <th>passo</th>
            <th><span class="arithmatex">&#92;(n&#92;)</span></th>
            <th><span class="arithmatex">&#92;(m&#92;)</span></th>
            <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(1&#92;)</span></td>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(84&#92;)</span></td>
            <td><span class="arithmatex">&#92;(30 &#92;bmod 84 = 30&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(2&#92;)</span></td>
            <td><span class="arithmatex">&#92;(84&#92;)</span></td>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(84 &#92;bmod 30 = 24&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(3&#92;)</span></td>
            <td><span class="arithmatex">&#92;(30&#92;)</span></td>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(30 &#92;bmod 24 = 6&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(4&#92;)</span></td>
            <td><span class="arithmatex">&#92;(24&#92;)</span></td>
            <td><span class="arithmatex">&#92;(6&#92;)</span></td>
            <td><span class="arithmatex">&#92;(24 &#92;bmod 6 = 0&#92;)</span></td>
            </tr>
            <tr>
            <td><span class="arithmatex">&#92;(5&#92;)</span></td>
            <td><span class="arithmatex">&#92;(6&#92;)</span></td>
            <td><span class="arithmatex">&#92;(0&#92;)</span></td>
            <td>— (il ciclo termina)</td>
            </tr>
            </table></div>

            <strong>Risultato:</strong> $\gcd(30, 84) = 6$, con $4$ iterazioni del ciclo while.

    2. Due numeri sono coprimi se e solo se il loro massimo comun divisore è $1$. Quindi le coppie coprime sono $(17,5)$ e $(89,55)$. Le coppie $(1071,462)$, $(100,75)$ e $(30,84)$ non sono coprime.

    3. Poiché $30<84$, si ha $30\bmod 84=30$, quindi la prima iterazione sostituisce $(30,84)$ con $(84,30)$: <strong>scambia</strong> semplicemente i due numeri. Dalla seconda iterazione in poi l'esecuzione è la stessa che per $(84,30)$, che richiede $3$ iterazioni. Dunque l'ipotesi $n\ge m$ non serve per la correttezza: se $n<m$, l'algoritmo esegue solo un'iterazione in più.

<a id="esercizio-6-18"></a>

!!! esercizio "Esercizio 6.18: Algoritmi numerici (E18)"

    Consideriamo il seguente algoritmo <strong>naïf</strong> per il massimo comun divisore, che prova tutti i candidati divisori da $\min\{n,m\}$ fino a $1$.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> NaiveGCD</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(n, m &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(&#92;gcd(n, m)&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> NaiveGCD(<span class="arithmatex">&#92;(n&#92;)</span>, <span class="arithmatex">&#92;(m&#92;)</span>)</span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd2-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d := &#92;min&#92;{n,m&#92;}&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd2-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(n &#92;bmod d &#92;ne 0&#92;)</span> <strong>or</strong> <span class="arithmatex">&#92;(m &#92;bmod d &#92;ne 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd2-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d &#92;leftarrow d - 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd2-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(d&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    Le domande 2–4 usano le nozioni di invariante di ciclo, numero di passi e dimensione dell'input $|I|$ (capitoli «Dimensione dell'input», «Tempo di esecuzione» e «Correttezza»).

    1. Applicare NaiveGCD a $(48,18)$ e $(35,12)$. Quante iterazioni del ciclo while vengono eseguite? Confrontarle con il numero di iterazioni dell'algoritmo di Euclide sulle stesse coppie.

    2. Dimostrare che NaiveGCD è corretto, usando un invariante di ciclo.

    3. Calcolare il numero di passi $S$ di NaiveGCD in funzione di $n$, $m$ e $\gcd(n,m)$, contando un passo per ogni esecuzione di una riga. Quali input danno il caso peggiore? Confrontare i due algoritmi su $(1000,999)$.

    4. Mostrare che NaiveGCD è esponenziale nella dimensione dell'input $|I|$.

??? soluzione "Soluzione"

    1. Per $(48,18)$: $d$ parte da $\min\{48,18\}=18$, e i candidati vengono controllati nell'ordine

        $$
        18,17,16,15,14,13,12,11,10,9,8,7,6.
        $$

        Il primo divisore comune è $d=6$ ($48=8\cdot 6$, $18=3\cdot 6$). Il corpo del ciclo while viene eseguito $18-6=12$ volte. L'algoritmo di Euclide richiede solo $3$ iterazioni ($48\bmod 18=12$, $18\bmod 12=6$, $12\bmod 6=0$).

        Per $(35,12)$: $d$ scende da $12$ a $1$, poiché $35$ e $12$ sono coprimi: $12-1=11$ iterazioni. L'algoritmo di Euclide richiede $3$ iterazioni ($35\bmod 12=11$, $12\bmod 11=1$, $11\bmod 1=0$).

    2. Invariante di ciclo:

        !!! chiave ""

            Ogni volta che la condizione alla riga [3](#riga-es-06-algoritmi-numerici-exgcd2-b) viene valutata, $1\le \gcd(n,m)\le d\le\min\{n,m\}$, cioè nessun numero $d'$ con $d<d'\le\min\{n,m\}$ è un divisore comune di $n$ e $m$.

        - <strong>Inizializzazione.</strong> $d=\min\{n,m\}$, e ogni divisore comune è al più $\min\{n,m\}$.

        - <strong>Conservazione.</strong> Se la condizione è vera, $d$ non è un divisore comune; poiché nessun numero più grande fino a $\min\{n,m\}$ è un divisore comune, $\gcd(n,m)<d$, cioè $\gcd(n,m)\le d-1$. La riga [4](#riga-es-06-algoritmi-numerici-exgcd2-c) pone $d\leftarrow d-1$, e l'invariante continua a valere.

        - <strong>Terminazione.</strong> $d$ diminuisce di $1$ a ogni iterazione e, per l'invariante, non può mai diventare minore di $\gcd(n,m)\ge 1$; quando $d=\gcd(n,m)$ la condizione è falsa. Quindi il ciclo termina, e quando termina $d$ è un divisore comune con $d\ge\gcd(n,m)$, dunque $d=\gcd(n,m)$, che viene restituito.

    3. Sia $k=\min\{n,m\}-\gcd(n,m)$ il numero di iterazioni. Le righe [2](#riga-es-06-algoritmi-numerici-exgcd2-a) e [6](#riga-es-06-algoritmi-numerici-exgcd2-d) sono eseguite una volta, la riga [3](#riga-es-06-algoritmi-numerici-exgcd2-b) $k+1$ volte, la riga [4](#riga-es-06-algoritmi-numerici-exgcd2-c) $k$ volte:

        $$
        S=1+(k+1)+k+1=2k+3=2\big(\min\{n,m\}-\gcd(n,m)\big)+3.
        $$

        Il caso peggiore si ha quando $n$ e $m$ sono coprimi: $S=2\min\{n,m\}+1$. Per $(1000,999)$ (numeri consecutivi sono sempre coprimi) NaiveGCD esegue $999-1=998$ iterazioni, mentre l'algoritmo di Euclide ne esegue solo $2$ ($1000\bmod 999=1$, $999\bmod 1=0$).

    4. Consideriamo le coppie $(n,m)=(M,M-1)$, con $M\ge 3$: sono coprime, quindi $S=2(M-1)+1=2M-1=\Theta(M)$. L'input è formato da due numeri naturali, quindi $|I|=\Theta(\log_2 M)$ con $M=\max\{n,m\}$, cioè esistono $c_1,c_2>0$ tali che

        $$
        2^{\frac{1}{c_2}|I|}\le M\le 2^{\frac{1}{c_1}|I|}.
        $$

        Quindi, su questi input, $S=2^{\Theta(|I|)}$, e il tempo di esecuzione nel caso peggiore soddisfa $T(|I|)=2^{\Theta(|I|)}$ (è anche al più $2M+1$ su ogni input).

        !!! chiave ""

            NaiveGCD è esponenziale nella dimensione dell'input, mentre l'algoritmo di Euclide esegue $O(\log_2 m)$ iterazioni (si veda l'esercizio successivo): per numeri con centinaia di cifre si può usare solo l'algoritmo di Euclide.

<a id="esercizio-6-19"></a>

!!! esercizio "Esercizio 6.19: Algoritmi numerici (E19)"

    Consideriamo l'algoritmo di Euclide.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> EuclideanAlgorithm</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(n, m &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(&#92;gcd(n, m)&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> EuclideanAlgorithm(<span class="arithmatex">&#92;(n&#92;)</span>, <span class="arithmatex">&#92;(m&#92;)</span>)</span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd3-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(m &#92;ne 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd3-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r := n &#92;bmod m&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd3-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow m&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd3-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow r&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd3-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(n&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    I numeri di Fibonacci sono $F_1=F_2=1$ e $F_{k}=F_{k-1}+F_{k-2}$ per $k\ge 3$:

    $$
    1,1,2,3,5,8,13,21,34,55,89,144,233,\dots
    $$

    **Domande**

    La domanda 4 usa le nozioni di tempo di esecuzione e dimensione dell'input $|I|$ (capitoli «Dimensione dell'input» e «Tempo di esecuzione»).

    1. Contare il numero di iterazioni del ciclo while per le coppie di numeri di Fibonacci consecutivi $(5,3)$, $(8,5)$, $(13,8)$, $(21,13)$, $(34,21)$, $(55,34)$, $(89,55)$, $(144,89)$, $(233,144)$.

    2. Dimostrare che, per ogni $n\ge m\ge 1$,

        $$
        n\bmod m<\frac n2.
        $$

    3. Usando il punto 2, dimostrare che il numero $t$ di iterazioni del ciclo while sull'input $(n_0,m_0)$ soddisfa

        $$
        t<2\log_2 m_0+2.
        $$

    4. Assumendo che ogni operazione aritmetica sia un passo, determinare il tempo di esecuzione nel caso peggiore $T(|I|)$ dell'algoritmo di Euclide. È polinomiale?

??? soluzione "Soluzione"

    1. Per una coppia $(F_{k+1},F_k)$ con $k\ge 3$ si ha $F_k < F_{k+1} < 2F_k$, quindi $F_{k+1}\bmod F_k=F_{k+1}-F_k=F_{k-1}$: a ogni iterazione si passa alla coppia precedente di numeri di Fibonacci consecutivi, fino a $(2,1)\to(1,0)$. Il numero di iterazioni è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;((n, m)&#92;)</span></th>
        <th>iterazioni <span class="arithmatex">&#92;(t&#92;)</span></th>
        <th><span class="arithmatex">&#92;(2 &#92;log&#95;2 m + 2&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((5, 3)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 5.17&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((8, 5)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 6.64&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((13, 8)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((21, 13)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 9.40&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((34, 21)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 10.78&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((55, 34)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 12.17&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((89, 55)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 13.56&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((144, 89)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 14.95&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((233, 144)&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;approx 16.34&#92;)</span></td>
        </tr>
        </table></div>

        Per esempio, $(89,55)\to(55,34)\to(34,21)\to(21,13)\to(13,8)\to(8,5)\to(5,3)\to(3,2)\to(2,1)\to(1,0)$: $9$ iterazioni. Il numero di iterazioni cresce di $1$ ogni volta che $m$ viene moltiplicato per circa $1.618$: cresce in modo logaritmico in $m$. (I numeri di Fibonacci consecutivi sono, di fatto, il caso peggiore dell'algoritmo di Euclide.)

    2. Sia $n\ge m\ge 1$. Due casi:

        - se $m\le\frac n2$, allora $n\bmod m<m\le\frac n2$;

        - se $m>\frac n2$, allora $m\le n<2m$, quindi il quoziente di $n$ diviso $m$ è $1$ e $n\bmod m=n-m<n-\frac n2=\frac n2$.

    3. Indichiamo con $m_s$ il valore di $m$ dopo $s$ iterazioni ($m_0$ è l'input). Nell'iterazione $s+1$ la coppia $(n,m)$ diventa $(m,\ n\bmod m)$, quindi dopo l'iterazione $s+1$ la variabile $n$ è uguale a $m_s$ e $m_{s+1}<m_s$. Dunque, se l'iterazione $s+2$ viene eseguita,

        $$
        m_{s+2}=m_s\bmod m_{s+1}
        \quad\text{con}\quad m_s> m_{s+1}\ge 1,
        $$

        e per il punto 2, $m_{s+2}<\dfrac{m_s}{2}$: ogni due iterazioni il valore di $m$ almeno si dimezza. Per induzione su $k$,

        $$
        m_{2k}<\frac{m_0}{2^k}\qquad\text{ogni volta che l'iterazione }2k\text{ viene eseguita}, \ k\ge 1.
        $$

        Se $t\le 2$ la limitazione vale: $t=1<2\le 2\log_2 m_0+2$, e $t=2$ è possibile solo se $m_0\ge 2$ (per $m_0=1$ il primo resto è $0$), quindi $2<2\log_2 m_0+2$. Sia $t\ge 3$ e sia $k=\lfloor (t-1)/2\rfloor\ge 1$. Poiché $2k\le t-1$, l'iterazione $2k+1$ viene eseguita, quindi $m_{2k}\ge 1$. Dunque

        $$
        1\le m_{2k}<\frac{m_0}{2^k}
        \quad\Longrightarrow\quad
        2^k<m_0
        \quad\Longrightarrow\quad
        k<\log_2 m_0 .
        $$

        Poiché $k\ge\frac{t-2}{2}$, si ottiene $\frac{t-2}{2}<\log_2 m_0$, cioè

        $$
        t<2\log_2 m_0+2.
        $$

        I valori nella tabella del punto 1 rispettano questa limitazione.

    4. Ogni iterazione esegue un numero costante di passi (righe [2](#riga-es-06-algoritmi-numerici-exgcd3-a)–[5](#riga-es-06-algoritmi-numerici-exgcd3-d)), quindi il numero di passi soddisfa $S=O(t)=O(\log_2 m_0)$. L'input è formato da due numeri naturali, quindi $|I|=\Theta(\log_2 M)$ con $M=\max\{n_0,m_0\}\ge m_0$: esiste $c>0$ tale che $\log_2 m_0\le\log_2 M\le\frac1c|I|$ per tutti gli input sufficientemente grandi. Quindi

        $$
        T(|I|)=O(|I|).
        $$

        !!! chiave ""

            L'algoritmo di Euclide esegue $O(\log_2 m)$ iterazioni, e il suo tempo di esecuzione nel caso peggiore è $T(|I|)=O(|I|)$: è polinomiale (lineare) nella dimensione dell'input.

        Osservazione: se i numeri sono molto grandi, un'operazione $n\bmod m$ non è un singolo passo, ma può essere eseguita in un numero di passi polinomiale in $|I|$; quindi l'algoritmo rimane polinomiale.

<a id="esercizio-6-20"></a>

!!! esercizio "Esercizio 6.20: Algoritmi numerici (E20)"

    Consideriamo la seguente variante dell'algoritmo di Euclide, che usa solo sottrazioni (è la versione descritta originariamente da Euclide).

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> SubtractiveGCD</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(n, m &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(&#92;gcd(n, m)&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> SubtractiveGCD(<span class="arithmatex">&#92;(n&#92;)</span>, <span class="arithmatex">&#92;(m&#92;)</span>)</span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd4-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(n &#92;ne m&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd4-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &gt; m&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd4-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow n - m&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd4-d"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow m - n&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-06-algoritmi-numerici-exgcd4-e"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(n&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    Le domande 3 e 4 usano le nozioni di invariante di ciclo, tempo di esecuzione e dimensione dell'input $|I|$ (capitoli «Dimensione dell'input», «Tempo di esecuzione» e «Correttezza»).

    1. Applicare SubtractiveGCD a $(48,18)$, mostrando i valori di $n$ e $m$ a ogni iterazione. Confrontare con l'algoritmo di Euclide.

    2. Dimostrare che, per ogni $n>m\ge 1$, $\gcd(n,m)=\gcd(n-m,m)$.

    3. Dimostrare la correttezza di SubtractiveGCD usando un invariante di ciclo.

    4. Quante iterazioni vengono eseguite sull'input $(n,1)$? SubtractiveGCD è polinomiale nella dimensione dell'input?

??? soluzione "Soluzione"

    1. Esecuzione su $(48,18)$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(m&#92;)</span></th>
        <th>azione</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(48&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n &gt; m&#92;)</span>: <span class="arithmatex">&#92;(n &#92;leftarrow 48 - 18 = 30&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(30&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n &gt; m&#92;)</span>: <span class="arithmatex">&#92;(n &#92;leftarrow 30 - 18 = 12&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n &lt; m&#92;)</span>: <span class="arithmatex">&#92;(m &#92;leftarrow 18 - 12 = 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n &gt; m&#92;)</span>: <span class="arithmatex">&#92;(n &#92;leftarrow 12 - 6 = 6&#92;)</span></td>
        </tr>
        <tr>
        <td>—</td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n = m&#92;)</span>: il ciclo termina, restituisce <span class="arithmatex">&#92;(6&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Risultato:</strong> $\gcd(48,18)=6$, con $4$ iterazioni. L'algoritmo di Euclide calcola $48\bmod 18=12$ in un solo passo: sottrarre $18$ da $48$ finché possibile (iterazioni 1–2) dà esattamente il resto $12$. In generale, una sequenza di sottrazioni consecutive dello stesso numero è un solo passo dell'algoritmo di Euclide.

    2. Sia $n>m\ge 1$. Se $d$ è un divisore comune di $n$ e $m$, allora $n=k_1d$ e $m=k_2d$, quindi $n-m=(k_1-k_2)d$, con $k_1-k_2\ge 1$ poiché $n>m$: $d$ è un divisore comune di $n-m$ e $m$. Viceversa, se $n-m=k_1d$ e $m=k_2d$, allora $n=(n-m)+m=(k_1+k_2)d$: $d$ è un divisore comune di $n$ e $m$. Le due coppie hanno gli stessi divisori comuni, quindi lo stesso massimo comun divisore.

    3. Indichiamo con $n_0,m_0$ i valori in input. Invariante di ciclo:

        !!! chiave ""

            Ogni volta che la condizione alla riga [2](#riga-es-06-algoritmi-numerici-exgcd4-a) viene valutata, $n\ge 1$, $m\ge 1$ e $\gcd(n,m)=\gcd(n_0,m_0)$.

        - <strong>Inizializzazione.</strong> $n=n_0\ge 1$, $m=m_0\ge 1$.

        - <strong>Conservazione.</strong> Supponiamo che valga l'invariante e che $n\neq m$. Se $n>m$, la riga [4](#riga-es-06-algoritmi-numerici-exgcd4-c) sostituisce $n$ con $n-m\ge 1$ e, per il punto 2, $\gcd(n-m,m)=\gcd(n,m)$. Se $n<m$, la riga [7](#riga-es-06-algoritmi-numerici-exgcd4-d) sostituisce $m$ con $m-n\ge 1$ e, per il punto 2 con i ruoli scambiati, $\gcd(n,m-n)=\gcd(n,m)$. In entrambi i casi l'invariante continua a valere.

        - <strong>Terminazione.</strong> Il numero naturale $n+m$ diminuisce di almeno $1$ a ogni iterazione (si sottrae un numero $\ge 1$), ed è sempre almeno $2$. Quindi il ciclo termina, e termina quando $n=m$. Allora

            $$
            \gcd(n_0,m_0)=\gcd(n,n)=n,
            $$

            che viene restituito alla riga [10](#riga-es-06-algoritmi-numerici-exgcd4-e).

    4. Su $(n,1)$ con $n\ge 2$, ogni iterazione esegue $n\leftarrow n-1$, fino a $n=1$: il ciclo esegue $n-1$ iterazioni (per esempio $(7,1)$ ne richiede $6$), mentre l'algoritmo di Euclide ne richiede solo $1$ ($n\bmod 1=0$). Ogni iterazione esegue un numero costante di passi, quindi sugli input $(M,1)$ si ha $S=\Theta(M)$. La dimensione dell'input è $|I|=(\lfloor\log_2 M\rfloor+1)+1=\Theta(\log_2 M)$, quindi $M=2^{\Theta(|I|)}$ e

        $$
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            SubtractiveGCD è corretto, ma è esponenziale nella dimensione dell'input. Sostituendo le sottrazioni ripetute con una singola operazione $\bmod$ si ottiene l'algoritmo di Euclide, che è polinomiale.
