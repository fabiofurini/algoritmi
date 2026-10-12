---
title: "Esercizi · Rappresentazione dei numeri"
---

# Esercizi · Rappresentazione dei numeri

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 1** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 1: Rappresentazione dei numeri](../algoritmi-di-base/01-rappresentazione-numeri.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-algoritmi-di-base.pdf)

</div>

Negli esercizi di questo capitolo i numeri sono rappresentati soltanto con le definizioni e le osservazioni del capitolo «Rappresentazione dei numeri», riassunte dalle seguenti formule.

!!! nota ""

    <strong>Numeri naturali</strong> con $k$ cifre in base $b$:

    \begin{align*}
    (d_{k-1} \dots d_1 d_0)_b &= \sum_{i=0}^{k-1} d_i\, b^i
    && \text{(valore di una sequenza di cifre)}\\[1ex]
    &[0,\, b^k-1]
    && \text{(intervallo di rappresentazione)}\\[1ex]
    &\lfloor \log_b n \rfloor + 1
    && \text{(numero minimo di cifre di } n \ge 1\text{)}
    \end{align*}

!!! nota ""

    <strong>Numeri interi</strong> con $k$ bit:

    \begin{align*}
    &\big[-(2^{k-1}-1),\, 2^{k-1}-1\big]
    && \text{(intervallo in modulo e segno)}\\[1ex]
    &\big[-2^{k-1},\, 2^{k-1}-1\big]
    && \text{(intervallo in complemento a due)}\\[1ex]
    &n < 0 \;\longmapsto\; 2^k + n
    && \text{(complemento a due di un } n\text{ negativo)}
    \end{align*}

    Nel complemento a due, la rappresentazione di un $n$ negativo si ottiene anche invertendo i bit di $|n|$ e aggiungendo $1$; una somma va in overflow se e solo se due operandi con lo stesso segno danno un risultato con il bit di segno opposto.

!!! nota ""

    <strong>Numeri reali</strong> in IEEE 754 a singola precisione ($1$ bit di segno $s$, $8$ bit di esponente polarizzato $E$, $23$ bit di parte frazionaria $f$), per $1 \le E \le 254$:

    $$
    x = (-1)^{s} \cdot (1.f_1 f_2 \dots f_{23})_2 \cdot 2^{E - 127}
    $$

    Doppia precisione: $1 + 11 + 52$ bit, polarizzazione $1023$.

<a id="esercizio-1-1"></a>

!!! esercizio "Esercizio 1.1: Rappresentazione dei numeri (E1)"

    Si consideri la rappresentazione dei numeri naturali nel sistema binario (base $b=2$): intervalli di rappresentazione e numero minimo di cifre.

    **Domande**

    1. Calcolare il più grande numero naturale rappresentabile con $k=6$ cifre in binario e determinare il relativo intervallo di rappresentazione.

    2. Per i seguenti valori di $k$ (numero di cifre), determinare l'intervallo di rappresentazione $[0, b^k-1]$ in base $b=2$:

        $$
        k=4, \qquad k=8, \qquad k=10, \qquad k=16
        $$

    3. Determinare il numero minimo di cifre necessarie per rappresentare ciascuno dei seguenti numeri in binario, usando la formula $\lfloor \log_b n\rfloor +1$:

        $$
        n=64, \qquad n=128, \qquad n=256, \qquad n=512
        $$

    4. Dati $k=12$ bit:

        1. determinare l'intervallo di rappresentazione;

        2. verificare che $n=2{,}048$ si può rappresentare con $k=12$ bit;

        3. calcolare il numero minimo di bit necessari per rappresentare $n=2{,}048$.

??? soluzione "Soluzione"

    1. Il più grande numero naturale rappresentabile con $k=6$ cifre in base $b=2$ è:

        $$
        b^k - 1 = 2^6 - 1 = 64 - 1 = 63
        $$

        Esso corrisponde alla sequenza binaria $(111111)_2$. Il relativo intervallo di rappresentazione è:

        $$
        [0, 2^6 - 1] = [0, 63]
        $$

    2. Intervalli di rappresentazione per i diversi valori di $k$:

        \begin{align*}
        k=4: &\quad [0, 2^4-1] = [0, 16-1] = [0, 15]\\[1ex]
        k=8: &\quad [0, 2^8-1] = [0, 256-1] = [0, 255]\\[1ex]
        k=10: &\quad [0, 2^{10}-1] = [0, 1{,}024-1] = [0, 1{,}023]\\[1ex]
        k=16: &\quad [0, 2^{16}-1] = [0, 65{,}536-1] = [0, 65{,}535]
        \end{align*}

    3. Il numero minimo di cifre per ciascun numero:

        \begin{align*}
        n=64 = 2^6: &\quad \lfloor \log_2 64\rfloor +1 = \lfloor 6 \rfloor +1 = 6 + 1 = 7\\[1ex]
        n=128 = 2^7: &\quad \lfloor \log_2 128\rfloor +1 = \lfloor 7 \rfloor +1 = 7 + 1 = 8\\[1ex]
        n=256 = 2^8: &\quad \lfloor \log_2 256\rfloor +1 = \lfloor 8 \rfloor +1 = 8 + 1 = 9\\[1ex]
        n=512 = 2^9: &\quad \lfloor \log_2 512\rfloor +1 = \lfloor 9 \rfloor +1 = 9 + 1 = 10
        \end{align*}

        Per le potenze di $2$, cioè $n=2^m$, si ha $\log_2 n = m$, e quindi il numero minimo di bit è $m+1$.

    4. Per $k=12$ bit:

        1. l'intervallo di rappresentazione è:

            $$
            [0, 2^{12}-1] = [0, 4{,}096-1] = [0, 4{,}095]
            $$

        2. poiché $n=2{,}048 = 2^{11}$ e $2{,}048 \le 4{,}095$, si ha $2{,}048 \in [0, 4{,}095]$: il numero $n=2{,}048$ si può rappresentare con $k=12$ bit;

        3. il numero minimo di bit necessari per rappresentare $n=2{,}048 = 2^{11}$ è:

            $$
            \lfloor \log_2 2{,}048\rfloor +1 = \lfloor 11 \rfloor +1 = 12
            $$

        Servono esattamente $12$ bit per rappresentare $2{,}048 = 2^{11}$, perché la sua rappresentazione binaria è una cifra $1$ seguita da undici cifre $0$:

        $$
        2{,}048 = (100000000000)_2
        $$

<a id="esercizio-1-2"></a>

!!! esercizio "Esercizio 1.2: Rappresentazione dei numeri (E2)"

    Si considerino gli intervalli di rappresentazione e il numero minimo di cifre dei numeri naturali nel sistema binario (base $b=2$).

    **Domande**

    1. Completare la seguente tabella degli intervalli di rappresentazione in binario:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(k&#92;)</span> (cifre)</th>
        <th><span class="arithmatex">&#92;(b&#92;)</span> (base)</th>
        <th><span class="arithmatex">&#92;(b^k-1&#92;)</span></th>
        <th>intervallo di rappresentazione</th>
        </tr>
        <tr>
        <td>5</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>8</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>10</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>12</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        </table></div>

    2. Per ogni numero naturale $n$ della tabella seguente, calcolare il numero minimo di cifre necessarie per rappresentarlo in base $b=2$, usando la formula $\lfloor \log_b n\rfloor +1$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;log&#95;b n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;lfloor &#92;log&#95;b n&#92;rfloor +1&#92;)</span></th>
        </tr>
        <tr>
        <td>7</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>15</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>31</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>100</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>255</td>
        <td>2</td>
        <td></td>
        <td></td>
        </tr>
        </table></div>

    3. Usando la relazione tra byte e bit, completare la tabella:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>byte</th>
        <th>bit (<span class="arithmatex">&#92;(k&#92;)</span>)</th>
        <th><span class="arithmatex">&#92;(2^k&#92;)</span></th>
        <th>intervallo di rappresentazione</th>
        </tr>
        <tr>
        <td>1</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(2^8=256&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,255&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td>4</td>
        <td></td>
        <td></td>
        <td></td>
        </tr>
        </table></div>

    4. Convertire $(11011011)_2$ in base dieci, scrivendo la somma completa $\sum_{i=0}^{k-1} d_i \cdot 2^i$.

??? soluzione "Soluzione"

    1. Intervalli di rappresentazione in binario:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(k&#92;)</span> (cifre)</th>
        <th><span class="arithmatex">&#92;(b&#92;)</span> (base)</th>
        <th><span class="arithmatex">&#92;(b^k-1&#92;)</span></th>
        <th>intervallo di rappresentazione</th>
        </tr>
        <tr>
        <td>5</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2^5-1=31&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,31&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>8</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2^8-1=255&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,255&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>10</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2^{10}-1=1{,}023&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,1{,}023&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>12</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2^{12}-1=4{,}095&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,4{,}095&#93;&#92;)</span></td>
        </tr>
        </table></div>

    2. Numero minimo di cifre per ciascun numero naturale:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;log&#95;b n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(&#92;lfloor &#92;log&#95;b n&#92;rfloor +1&#92;)</span></th>
        </tr>
        <tr>
        <td>7</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;log&#95;2 7 &#92;approx 2.807&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;lfloor 2.807 &#92;rfloor +1 = 3&#92;)</span></td>
        </tr>
        <tr>
        <td>15</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;log&#95;2 15 &#92;approx 3.907&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;lfloor 3.907 &#92;rfloor +1 = 4&#92;)</span></td>
        </tr>
        <tr>
        <td>31</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;log&#95;2 31 &#92;approx 4.954&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;lfloor 4.954 &#92;rfloor +1 = 5&#92;)</span></td>
        </tr>
        <tr>
        <td>100</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;log&#95;2 100 &#92;approx 6.644&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;lfloor 6.644 &#92;rfloor +1 = 7&#92;)</span></td>
        </tr>
        <tr>
        <td>255</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(&#92;log&#95;2 255 &#92;approx 7.994&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;lfloor 7.994 &#92;rfloor +1 = 8&#92;)</span></td>
        </tr>
        </table></div>

        Per i numeri della forma $2^k - 1$ servono esattamente $k$ bit: $2^k-1$ è il più grande numero naturale con $k$ bit.

    3. Poiché $1$ byte $= 8$ bit:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>byte</th>
        <th>bit (<span class="arithmatex">&#92;(k&#92;)</span>)</th>
        <th><span class="arithmatex">&#92;(2^k&#92;)</span></th>
        <th>intervallo di rappresentazione</th>
        </tr>
        <tr>
        <td>1</td>
        <td>8</td>
        <td><span class="arithmatex">&#92;(2^8=256&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,255&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td>16</td>
        <td><span class="arithmatex">&#92;(2^{16}=65{,}536&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,65{,}535&#93;&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td>32</td>
        <td><span class="arithmatex">&#92;(2^{32}=4{,}294{,}967{,}296&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#91;0,4{,}294{,}967{,}295&#93;&#92;)</span></td>
        </tr>
        </table></div>

    4. La sequenza ha $k=8$ cifre: $d_7=1$, $d_6=1$, $d_5=0$, $d_4=1$, $d_3=1$, $d_2=0$, $d_1=1$, $d_0=1$. Quindi:

        \begin{align*}
        (11011011)_2 &= \sum_{i=0}^{7} d_i \cdot 2^i \\
        &= d_0 \cdot 2^0 + d_1 \cdot 2^1 + d_2 \cdot 2^2 + d_3 \cdot 2^3 + d_4 \cdot 2^4 + d_5 \cdot 2^5 + d_6 \cdot 2^6 + d_7 \cdot 2^7 \\
        &= 1 \cdot 1 + 1 \cdot 2 + 0 \cdot 4 + 1 \cdot 8 + 1 \cdot 16 + 0 \cdot 32 + 1 \cdot 64 + 1 \cdot 128 \\
        &= 1 + 2 + 0 + 8 + 16 + 0 + 64 + 128 \\
        &= 219
        \end{align*}

        Pertanto, $(11011011)_2 = (219)_{10}$.

<a id="esercizio-1-3"></a>

!!! esercizio "Esercizio 1.3: Rappresentazione dei numeri (E3)"

    Si considerino l'enumerazione completa delle sequenze di cifre in binario per un dato numero di bit e la rappresentazione binaria di alcuni numeri naturali.

    **Domande**

    1. Completare la tabella di tutte le sequenze di $k=5$ cifre in binario (base $2$) e dei loro valori decimali. Mostrare il calcolo dettagliato almeno per le prime tre e le ultime tre sequenze:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>Sequenza di cifre</th>
        <th><span class="arithmatex">&#92;(b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(k&#92;)</span></th>
        <th>rappresentazione decimale</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00000)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00001)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00010)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00011)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11101)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11110)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11111)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td></td>
        </tr>
        </table></div>

    2. Quante sequenze diverse sono possibili con $k=5$ bit? Verificare la risposta con la formula $b^k$, dove $b=2$.

    3. Trovare la rappresentazione binaria dei seguenti numeri decimali, determinando quali potenze di $2$ sommano al valore dato:

        $$
        n=21, \qquad n=50, \qquad n=63
        $$

    4. Per ciascuna sequenza seguente, stabilire se rappresenta una potenza di $2$ e, in caso affermativo, quale potenza:

        $$
        (10000)_2, \qquad (10101)_2, \qquad (100000000)_2
        $$

??? soluzione "Soluzione"

    1. Tutte le sequenze con $k=5$ bit:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>Sequenza di cifre</th>
        <th><span class="arithmatex">&#92;(b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(k&#92;)</span></th>
        <th>rappresentazione decimale</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00000)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((0 &#92;cdot 2^4 + 0 &#92;cdot 2^3 + 0 &#92;cdot 2^2 + 0 &#92;cdot 2^1 + 0 &#92;cdot 2^0)&#95;{10} = (0)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00001)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((0 &#92;cdot 2^4 + 0 &#92;cdot 2^3 + 0 &#92;cdot 2^2 + 0 &#92;cdot 2^1 + 1 &#92;cdot 2^0)&#95;{10} = (1)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00010)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((0 &#92;cdot 2^4 + 0 &#92;cdot 2^3 + 0 &#92;cdot 2^2 + 1 &#92;cdot 2^1 + 0 &#92;cdot 2^0)&#95;{10} = (2)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00011)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((3)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00100)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((4)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00101)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((5)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00110)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((6)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((00111)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((7)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((01000)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((8)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((01001)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((9)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        <td><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11101)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((1 &#92;cdot 2^4 + 1 &#92;cdot 2^3 + 1 &#92;cdot 2^2 + 0 &#92;cdot 2^1 + 1 &#92;cdot 2^0)&#95;{10} = (29)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11110)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((1 &#92;cdot 2^4 + 1 &#92;cdot 2^3 + 1 &#92;cdot 2^2 + 1 &#92;cdot 2^1 + 0 &#92;cdot 2^0)&#95;{10} = (30)&#95;{10}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((11111)&#95;2&#92;)</span></td>
        <td>2</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;((1 &#92;cdot 2^4 + 1 &#92;cdot 2^3 + 1 &#92;cdot 2^2 + 1 &#92;cdot 2^1 + 1 &#92;cdot 2^0)&#95;{10} = (31)&#95;{10}&#92;)</span></td>
        </tr>
        </table></div>

    2. Il numero totale di sequenze diverse con $k=5$ bit in base $b=2$ è:

        $$
        b^k = 2^5 = 32
        $$

        Infatti, le sequenze vanno da $(00000)_2 = 0$ a $(11111)_2 = 31$, il che dà esattamente $32$ valori diversi (da $0$ a $31$ inclusi).

    3. Rappresentazione binaria dei numeri decimali:

        - $n=21$: cerchiamo le potenze di $2$ che sommano a $21$, partendo dalla più grande potenza non maggiore di $21$:

            $$
            21 = 16 + 5 = 16 + 4 + 1 = 2^4 + 2^2 + 2^0
            $$

            Quindi $(21)_{10} = (10101)_2$.

        - $n=50$:

            $$
            50 = 32 + 18 = 32 + 16 + 2 = 2^5 + 2^4 + 2^1
            $$

            Quindi $(50)_{10} = (110010)_2$.

        - $n=63$:

            $$
            63 = 32 + 31 = 32 + 16 + 8 + 4 + 2 + 1 = 2^5 + 2^4 + 2^3 + 2^2 + 2^1 + 2^0
            $$

            In alternativa, $63 = 2^6 - 1$ è il più grande numero naturale con $6$ bit, quindi tutti i suoi $6$ bit valgono $1$. Quindi $(63)_{10} = (111111)_2$.

    4. Potenze di $2$:

        - $(10000)_2 = 1 \cdot 2^4 + 0 \cdot 2^3 + 0 \cdot 2^2 + 0 \cdot 2^1 + 0 \cdot 2^0 = 2^4 = 16$: è una potenza di $2$, precisamente $2^4$.

        - $(10101)_2 = 1 \cdot 2^4 + 0 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 = 16 + 4 + 1 = 21$: non è una potenza di $2$ (è la somma di tre potenze di $2$ diverse).

        - $(100000000)_2 = 1 \cdot 2^8 = 256$: è una potenza di $2$, precisamente $2^8$.

        Una sequenza in binario rappresenta una potenza di $2$ se e solo se ha esattamente una cifra uguale a $1$ e tutte le altre cifre uguali a $0$.

<a id="esercizio-1-4"></a>

!!! esercizio "Esercizio 1.4: Rappresentazione dei numeri (E4)"

    Si consideri la rappresentazione in complemento a due dei numeri interi in binario.

    **Domande**

    1. Determinare l'intervallo di rappresentazione degli interi in complemento a due con i seguenti numeri di bit:

        $$
        k=4, \qquad k=8, \qquad k=16, \qquad k=32
        $$

    2. Completare la seguente tabella con tutte le rappresentazioni in complemento a due con $k=4$ bit:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>Binario</th>
        <th>Decimale</th>
        <th>Bit di segno</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0000)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0001)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0010)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0011)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0100)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0101)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0110)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0111)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1000)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1001)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1010)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1011)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1100)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1101)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1110)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1111)&#95;2&#92;)</span></td>
        <td></td>
        <td></td>
        </tr>
        </table></div>

    3. Calcolare la rappresentazione in complemento a due di $-5$ con $8$ bit in tre passi: (1) rappresentazione binaria di $5$, (2) inversione di tutti i bit, (3) somma di $1$.

    4. Verificare che con $k=5$ bit in complemento a due si può rappresentare l'intero $-16$ ma non l'intero $16$.

??? soluzione "Soluzione"

    1. Intervalli di rappresentazione, con la formula $[-2^{k-1}, 2^{k-1}-1]$:

        \begin{align*}
        k=4: &\quad [-2^{4-1}, 2^{4-1}-1] = [-2^3, 2^3-1] = [-8, 7]\\[1ex]
        k=8: &\quad [-2^{8-1}, 2^{8-1}-1] = [-2^7, 2^7-1] = [-128, 127]\\[1ex]
        k=16: &\quad [-2^{16-1}, 2^{16-1}-1] = [-2^{15}, 2^{15}-1] = [-32{,}768,\, 32{,}767]\\[1ex]
        k=32: &\quad [-2^{32-1}, 2^{32-1}-1] = [-2^{31}, 2^{31}-1] = [-2{,}147{,}483{,}648,\, 2{,}147{,}483{,}647]
        \end{align*}

    2. Tutte le rappresentazioni in complemento a due con $k=4$ bit: una sequenza con bit di segno $1$ e valore naturale $r$ rappresenta $r - 16$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>Binario</th>
        <th>Decimale</th>
        <th>Bit di segno</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0000)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0001)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0010)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0011)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0100)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0101)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0110)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((0111)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span> (non negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1000)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8-16=-8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1001)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9-16=-7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1010)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(10-16=-6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1011)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11-16=-5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1100)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12-16=-4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1101)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(13-16=-3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1110)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(14-16=-2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;((1111)&#95;2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(15-16=-1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span> (negativo)</td>
        </tr>
        </table></div>

        L'intervallo di rappresentazione con $4$ bit è $[-8, 7]$.

    3. Rappresentazione in complemento a due di $-5$ con $8$ bit:

        - Passo 1: rappresentazione binaria di $5$ con $8$ bit: $(00000101)_2$.

        - Passo 2: inversione di tutti i bit: $(11111010)_2$.

        - Passo 3: somma di $1$ (la prima riga contiene i riporti; il riporto sopra una colonna proviene dalla colonna alla sua destra):

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            </tr>
            <tr>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            </tr>
            </table></div>

        Pertanto, la rappresentazione in complemento a due di $-5$ con $8$ bit è $(11111011)_2$. Verifica:

        $$
        2^8 - 5 = 256 - 5 = 251 = (11111011)_2
        $$

    4. Con $k=5$ bit l'intervallo di rappresentazione è:

        $$
        [-2^{5-1}, 2^{5-1}-1] = [-2^4, 2^4-1] = [-16, 15]
        $$

        - Poiché $-16 \in [-16, 15]$, l'intero $-16$ si può rappresentare, e la sua rappresentazione è:

            $$
            2^5 - 16 = 32 - 16 = 16 = (10000)_2
            $$

        - Poiché $16 > 15$, si ha $16 \notin [-16, 15]$: l'intero $16$ non si può rappresentare con $5$ bit in complemento a due.

        Il complemento a due rappresenta un intero negativo in più rispetto a quelli positivi, perché l'intervallo $[-2^{k-1}, 2^{k-1}-1]$ è asimmetrico.

<a id="esercizio-1-5"></a>

!!! esercizio "Esercizio 1.5: Rappresentazione dei numeri (E5)"

    Si considerino la somma di numeri interi in complemento a due, il rilevamento degli overflow e il confronto tra modulo e segno e complemento a due.

    **Domande**

    1. Eseguire le seguenti somme in complemento a due con $k=5$ bit, mostrando le rappresentazioni binarie e la somma in colonna, e verificare i risultati:

        $$
        (-7) + 3, \qquad (-8) + 8, \qquad 5 + 6
        $$

    2. Stabilire se si verifica un overflow nelle seguenti somme con $k=5$ bit, e spiegarne il motivo:

        $$
        7 + 7, \qquad (-8) + (-8), \qquad 7 + (-8), \qquad 9 + 8
        $$

    3. Confrontare le rappresentazioni in modulo e segno e in complemento a due con $k=4$ bit:

        1. qual è l'intervallo di rappresentazione di ciascuna?

        2. quante rappresentazioni ha lo zero in ciascun sistema?

        3. quale sistema è migliore per le operazioni aritmetiche, e perché?

    4. Con $k=8$ bit in complemento a due, calcolare le rappresentazioni di $-64$ e $-128$, usando la formula $2^k + n$ per gli interi negativi $n$.

??? soluzione "Soluzione"

    Nelle somme in colonna, la prima riga contiene i riporti: il riporto scritto sopra una colonna proviene dalla colonna alla sua destra, e la colonna più a sinistra riceve il riporto uscente dalla posizione più significativa, che viene scartato.

    1. Con $k=5$ bit l'intervallo di rappresentazione è $[-16, 15]$.

        - $(-7) + 3 = -4$. Rappresentazioni: $-7 \rightarrow 2^5 - 7 = 25 = (11001)_2$ e $3 = (00011)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            </tr>
            </table></div>

            Il risultato $(11100)_2$ ha valore naturale $28$, quindi rappresenta $28 - 32 = -4$.

        - $(-8) + 8 = 0$. Rappresentazioni: $-8 \rightarrow 2^5 - 8 = 24 = (11000)_2$ e $8 = (01000)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            </table></div>

            Il risultato è $(00000)_2 = 0$.

        - $5 + 6 = 11$. Rappresentazioni: $5 = (00101)_2$ e $6 = (00110)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>1</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            </tr>
            </table></div>

            Il risultato è $(01011)_2 = 11$.

    2. Rilevamento dell'overflow con $k=5$ bit (intervallo $[-16, 15]$):

        - $7 + 7$ (atteso $14$). Rappresentazioni: $7 = (00111)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            </tr>
            </table></div>

            Risultato: $(01110)_2 = 14$: entrambi gli operandi sono positivi e il risultato è positivo: nessun overflow ($14 \le 15$).

        - $(-8) + (-8)$ (atteso $-16$). Rappresentazioni: $-8 \rightarrow 2^5 - 8 = 24 = (11000)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            </table></div>

            Risultato: $(10000)_2 = -16$: entrambi gli operandi sono negativi e il risultato è negativo: nessun overflow ($-16 \ge -16$). Il riporto uscente viene scartato.

        - $7 + (-8)$ (atteso $-1$). Rappresentazioni: $7 = (00111)_2$ e $-8 \rightarrow 2^5 - 8 = 24 = (11000)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>1</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>0</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            <td>1</td>
            </tr>
            </table></div>

            Risultato: $(11111)_2 = -1$: gli operandi hanno segni diversi, quindi non può verificarsi un overflow.

        - $9 + 8$ (atteso $17$). Rappresentazioni: $9 = (01001)_2$ e $8 = (01000)_2$.

            <div class="tabella" markdown="0"><table>
            <tr>
            <td>riporto</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td></td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            </tr>
            <tr>
            <td></td>
            <td></td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            </tr>
            <tr>
            <td>somma</td>
            <td>0</td>
            <td>1</td>
            <td>0</td>
            <td>0</td>
            <td>0</td>
            <td>1</td>
            </tr>
            </table></div>

            Risultato: $(10001)_2 = -15$: entrambi gli operandi sono positivi, ma il risultato ha bit di segno $1$: overflow. Infatti $9 + 8 = 17 > 15$ non si può rappresentare con $5$ bit.

        Regola: si ha overflow solo quando si sommano due interi con lo stesso segno e il risultato ha il bit di segno opposto.

    3. Confronto tra modulo e segno e complemento a due con $k=4$ bit:

        1. intervalli di rappresentazione:

            \begin{align*}
            \text{modulo e segno:} &\quad [-(2^{4-1}-1),\, 2^{4-1}-1] = [-7, 7]\\[1ex]
            \text{complemento a due:} &\quad [-2^{4-1},\, 2^{4-1}-1] = [-8, 7]
            \end{align*}

            il complemento a due rappresenta un intero in più, $-8$;

        2. il modulo e segno ha due rappresentazioni dello zero, $(0000)_2 = +0$ e $(1000)_2 = -0$; il complemento a due ne ha una sola, $(0000)_2 = 0$;

        3. il complemento a due è migliore per le operazioni aritmetiche, perché:

            - lo zero ha una rappresentazione unica;

            - somma e sottrazione si eseguono come per i numeri naturali (modulo $2^k$), con gli stessi circuiti usati per i numeri senza segno;

            - il bit di segno non richiede un trattamento speciale, quindi i circuiti sono più semplici ed efficienti.

    4. Rappresentazioni con $k=8$ bit:

        \begin{align*}
        -64: &\quad 2^k + n = 2^8 + (-64) = 256 - 64 = 192 = (11000000)_2\\[1ex]
        -128: &\quad 2^k + n = 2^8 + (-128) = 256 - 128 = 128 = (10000000)_2
        \end{align*}

        L'intero $-128 = -2^{8-1}$ è il più piccolo intero rappresentabile con $8$ bit in complemento a due.

<a id="esercizio-1-6"></a>

!!! esercizio "Esercizio 1.6: Rappresentazione dei numeri (E6)"

    Si consideri la rappresentazione dei numeri reali in virgola mobile, secondo lo standard IEEE 754.

    **Domande**

    1. Scrivere il numero reale $13.25$ in binario e in notazione scientifica binaria normalizzata, e fornire i suoi $32$ bit in IEEE 754 a singola precisione.

    2. Determinare il numero reale rappresentato dai seguenti $32$ bit in IEEE 754 a singola precisione:

        $$
        0~~01111100~~01000000000000000000000
        $$

    3. Usando il formato a doppia precisione ($1$ bit di segno, $11$ bit di esponente con polarizzazione $1023$, $52$ bit di parte frazionaria), calcolare il più grande numero finito e il più piccolo numero normalizzato positivo. I valori $E = 0$ e $E = 2^{11}-1 = 2{,}047$ dell'esponente polarizzato sono riservati.

    4. In doppia precisione, sommare dieci volte il numero $0.1$ a una variabile inizializzata a $0$ dà $0.99999999999999989$ e non $1$. Spiegare perché.

??? soluzione "Soluzione"

    1. Rappresentazione di $13.25$:

        - Passo 1 (binario): $13.25 = 8 + 4 + 1 + 0.25 = 1 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 + 0 \cdot 2^{-1} + 1 \cdot 2^{-2}$, quindi:

            $$
            13.25 = (1101.01)_2
            $$

        - Passo 2 (normalizzazione): la virgola si sposta di tre posizioni a sinistra:

            $$
            (1101.01)_2 = (1.10101)_2 \cdot 2^3
            $$

            quindi $s = 0$, $e = 3$ e la parte frazionaria inizia con $10101$.

        - Passo 3 (esponente polarizzato): $E = e + 127 = 130 = 128 + 2 = (10000010)_2$.

        - Passo 4 (parte frazionaria): $10101$ completato con zeri fino a $23$ bit.

        I $32$ bit sono:

        $$
        \underbrace{0}_{s}~~\underbrace{10000010}_{E}~~\underbrace{10101000000000000000000}_{f}
        $$

    2. Lettura dei $32$ bit:

        - Passo 1 (segno): $s = 0$, il numero è positivo.

        - Passo 2 (esponente): $E = (01111100)_2 = 64 + 32 + 16 + 8 + 4 = 124$, quindi $e = E - 127 = -3$.

        - Passo 3 (mantissa): $(1.01)_2 = 1 + 0.25 = 1.25$.

        - Passo 4 (valore):

            $$
            x = (-1)^0 \cdot 1.25 \cdot 2^{-3} = \frac{1.25}{8} = 0.15625
            $$

    3. In doppia precisione un numero normalizzato è $(-1)^s \cdot (1.f_1 f_2 \dots f_{52})_2 \cdot 2^{E - 1023}$ con $1 \le E \le 2{,}046$.

        - Il più grande numero finito ha $E = 2{,}046$, cioè $e = 1{,}023$, e tutti i $52$ bit della parte frazionaria uguali a $1$, cioè mantissa $\sum_{i=0}^{52} 2^{-i} = 2 - 2^{-52}$:

            $$
            (2 - 2^{-52}) \cdot 2^{1023} \approx 1.7976931349 \times 10^{308}
            $$

        - Il più piccolo numero normalizzato positivo ha $E = 1$, cioè $e = -1{,}022$, e tutti i bit della parte frazionaria uguali a $0$:

            $$
            1 \cdot 2^{-1022} \approx 2.2250738585 \times 10^{-308}
            $$

    4. Il numero decimale $0.1$ ha una rappresentazione binaria infinita:

        $$
        0.1 = (0.0\,0011\,0011\,0011\dots)_2 = (1.1001\,1001\,1001\dots)_2 \cdot 2^{-4}
        $$

        quindi la sua parte frazionaria non entra in $52$ bit e viene arrotondata. Il numero effettivamente memorizzato è leggermente diverso da $0.1$:

        $$
        0.1000000000000000055511151231\dots
        $$

        Inoltre, il risultato di ogni somma viene arrotondato di nuovo al più vicino numero rappresentabile in doppia precisione. I dieci errori di arrotondamento si accumulano, e il risultato finale non è $1$ ma:

        $$
        0.99999999999999989
        $$

        Per questo motivo, due numeri in virgola mobile non vanno confrontati con l'operatore di uguaglianza senza cautela.
