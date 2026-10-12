---
title: "Esercizi · Dimensione dell'input"
---

# Esercizi · Dimensione dell'input

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 11** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 11: Dimensione dell'input](../analisi/11-dimensione-input.md) · [:material-file-pdf-box: Eserciziario, volume 4 (PDF)](../pdf/esercizi-4-analisi.pdf)

</div>

Negli esercizi di questo capitolo la dimensione dell'input si calcola con le formule del capitolo «Dimensione dell'input», riassunte qui sotto.

!!! nota ""

    La dimensione dell'input $|I|$ di un'istanza $I$ è il numero totale di bit necessari per rappresentare $I$ in binario:

    - un numero naturale $n\ge 1$:

        $$
        |I|=\lfloor\log_2 n\rfloor+1=\Theta(\log_2 n);
        $$

    - due numeri naturali $n,m\ge 1$:

        $$
        |I|=\big(\lfloor\log_2 n\rfloor+1\big)+\big(\lfloor\log_2 m\rfloor+1\big)=\Theta\big(\log_2 \max\{n,m\}\big);
        $$

    - un array $a[1..n]$ di numeri naturali (una componente uguale a $0$ usa $1$ bit):

        $$
        |I|=\sum_{i=1}^{n}\big(\lfloor\log_2(\max\{1,a[i]\})\rfloor+1\big),
        \qquad
        n \le |I| \le n(1+\log_2 M),
        $$

        dove $M=\max\{1,a[1],a[2],\dots,a[n]\}$.

    Un numero naturale si scrive con esattamente $k$ bit se e solo se $2^{k-1}\le n\le 2^k-1$.

<a id="esercizio-11-1"></a>

!!! esercizio "Esercizio 11.1: Dimensione dell'input (E1)"

    Consideriamo le seguenti istanze di input:

    - **(a)** i numeri naturali $n=1$, $n=13$, $n=255$, $n=256$, $n=1000$, $n=10^6$;

    - **(b)** le coppie di numeri naturali $(n,m)=(48,18)$ e $(n,m)=(1000,7)$;

    - **(c)** gli array $[5,2,4,1,3]$, $[1,1,1,1]$, $[1024,1,1]$, $[0,7,8]$.

    **Domande**

    1. Calcolare la dimensione dell'input $|I|$ di ogni istanza in (a), e scrivere la rappresentazione binaria di $13$, $255$ e $256$.

    2. Calcolare la dimensione dell'input delle due istanze in (b).

    3. Calcolare la dimensione dell'input dei quattro array in (c). Per ogni array confrontare $|I|$ con il numero $n$ di componenti e con il limite superiore $n(1+\log_2 M)$, dove $M=\max\{1,a[1],a[2],\dots,a[n]\}$.

    4. Qual è il più grande numero naturale rappresentabile con $|I|=k$ bit? E il più piccolo numero naturale $n\ge 1$ la cui dimensione dell'input è $k$?

??? soluzione "Soluzione"

    1. Usando $|I|=\lfloor\log_2 n\rfloor+1$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th>potenze di 2</th>
        <th><span class="arithmatex">&#92;(&#92;lfloor&#92;log&#95;2 n&#92;rfloor&#92;)</span></th>
        <th><span class="arithmatex">&#92;(|I|&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^0&#92;le 1&lt;2^1&#92;)</span></td>
        <td>0</td>
        <td>1</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(13&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^3&#92;le 13&lt;2^4&#92;)</span></td>
        <td>3</td>
        <td>4</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(255&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^7&#92;le 255&lt;2^8&#92;)</span></td>
        <td>7</td>
        <td>8</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(256&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^8&#92;le 256&lt;2^9&#92;)</span></td>
        <td>8</td>
        <td>9</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1000&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^9&#92;le 1000&lt;2^{10}&#92;)</span></td>
        <td>9</td>
        <td>10</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(10^6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2^{19}&#92;le 10^6&lt;2^{20}&#92;)</span></td>
        <td>19</td>
        <td>20</td>
        </tr>
        </table></div>

        Rappresentazioni binarie: $13=(1101)_2$ (4 bit), $255=(11111111)_2$ (8 bit), $256=(100000000)_2$ (9 bit). Si noti che $255$ e $256$ differiscono di $1$, ma le loro dimensioni dell'input differiscono di un bit, perché $256=2^8$ è una potenza di $2$.

    2. Per $(48,18)$: $2^5\le 48<2^6$ e $2^4\le 18<2^5$, quindi

        $$
        |I|=(5+1)+(4+1)=6+5=11.
        $$

        Per $(1000,7)$: $2^9\le 1000<2^{10}$ e $2^2\le 7<2^3$, quindi

        $$
        |I|=(9+1)+(2+1)=10+3=13.
        $$

    3. Bit di ogni componente e totale:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>array</th>
        <th>bit per componente</th>
        <th><span class="arithmatex">&#92;(|I|&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n(1+&#92;log&#95;2 M)&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#91;5,2,4,1,3&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3+2+3+1+2&#92;)</span></td>
        <td>11</td>
        <td>5</td>
        <td><span class="arithmatex">&#92;(5(1+&#92;log&#95;2 5)&#92;approx 16.61&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#91;1,1,1,1&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1+1+1+1&#92;)</span></td>
        <td>4</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(4(1+0)=4&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#91;1024,1,1&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11+1+1&#92;)</span></td>
        <td>13</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(3(1+10)=33&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(&#91;0,7,8&#93;&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1+3+4&#92;)</span></td>
        <td>8</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(3(1+3)=12&#92;)</span></td>
        </tr>
        </table></div>

        In tutti i casi $n\le|I|\le n(1+\log_2 M)$, in accordo con $|I|=\Omega(n)$ e $|I|=O(n(1+\log_2 M))$. Il limite superiore è stretto per $[1,1,1,1]$ (componenti tutte uguali), mentre è lontano da $|I|$ per $[1024,1,1]$, dove solo una componente è grande.

    4. Con $k$ bit il più grande numero rappresentabile è

        $$
        (\underbrace{11\dots1}_{k})_2=2^k-1,
        $$

        e il più piccolo numero $n\ge 1$ con $\lfloor\log_2 n\rfloor+1=k$ è $n=2^{k-1}=(1\underbrace{0\dots0}_{k-1})_2$. Dunque i numeri con dimensione dell'input esattamente $k$ sono quelli con

        $$
        2^{k-1}\le n\le 2^k-1.
        $$

        Ad esempio, per $k=8$ sono i numeri da $128$ a $255$.

<a id="esercizio-11-2"></a>

!!! esercizio "Esercizio 11.2: Dimensione dell'input (E2)"

    Consideriamo le seguenti famiglie di istanze di input, parametrizzate da un numero naturale $n\ge 1$ (oppure $k\ge 1$):

    - **(a)** il singolo numero naturale $2^k$, e il singolo numero naturale $2^k-1$;

    - **(b)** l'array $a[1..n]$ con $a[i]=i$ per ogni $i\in\{1, 2, \dots, n\}$;

    - **(c)** l'array $a[1..n]$ con $a[i]=2^i$ per ogni $i\in\{1, 2, \dots, n\}$;

    - **(d)** l'array $a[1..n]$ con $a[i]=n$ per ogni $i\in\{1, 2, \dots, n\}$;

    - **(e)** un array $a[1..n]$ le cui componenti sono numeri naturali minori di $2^{32}$, così che ciascuna di esse può essere scritta con al più $32$ bit.

    **Domande**

    1. Calcolare esattamente la dimensione dell'input delle istanze in (a), in funzione di $k$.

    2. Calcolare esattamente la dimensione dell'input degli array in (c), ed esprimerla asintoticamente in funzione di $n$.

    3. Esprimere asintoticamente la dimensione dell'input degli array in (d) ed (e).

    4. Per gli array in (b), calcolare $|I|$ per $n=1,2,3,4,8,16$, e dimostrare che $|I|=\Theta(n\log_2 n)$.

??? soluzione "Soluzione"

    1. Poiché $\log_2 2^k=k$, il numero $2^k$ ha dimensione dell'input

        $$
        |I|=\lfloor\log_2 2^k\rfloor+1=k+1.
        $$

        Poiché $2^{k-1}\le 2^k-1<2^k$, si ha $\lfloor\log_2(2^k-1)\rfloor=k-1$ e

        $$
        |I|=k.
        $$

        In entrambi i casi $|I|=\Theta(k)$, mentre il valore numerico è $\Theta(2^k)$: il valore è esponenziale nella dimensione dell'input.

    2. La componente $a[i]=2^i$ richiede $\lfloor\log_2 2^i\rfloor+1=i+1$ bit, quindi

        $$
        |I|=\sum_{i=1}^{n}(i+1)=\frac{n(n+1)}{2}+n=\frac{n(n+3)}{2}.
        $$

        Ad esempio, per $n=4$: $2+3+4+5=14=\frac{4\cdot 7}{2}$. Poiché

        $$
        \lim_{n\to\infty}\frac{n(n+3)/2}{n^2}=\lim_{n\to\infty}\frac{1}{2}\left(1+\frac{3}{n}\right)=\frac12\in\R_{>0},
        $$

        si ha $|I|=\Theta(n^2)$ per il criterio del limite. In modo diretto, poiché $n^2 \le n(n+3) \le 4n^2$ per ogni $n \ge 1$, le costanti $c_1=\frac12$, $c_2=2$ e $n_1=1$ danno $\frac12 n^2\le|I|\le 2n^2$. Qui le componenti <strong>non</strong> usano un numero costante di bit, e la dimensione dell'input è quadratica nel numero di componenti.

    3. (d) Ogni componente è uguale a $n$ e usa $\lfloor\log_2 n\rfloor+1$ bit, quindi

        $$
        |I|=n\big(\lfloor\log_2 n\rfloor+1\big)=\Theta(n\log_2 n),
        $$

        perché $\lfloor\log_2 n\rfloor+1=\Theta(\log_2 n)$ (Osservazione sulla dimensione dell'input di un numero naturale), moltiplicato per $n$.

        (e) Ogni componente usa almeno $1$ e al più $32$ bit, quindi

        $$
        n\le|I|\le 32n,
        $$

        e $|I|=\Theta(n)$. Questa è l'ipotesi “ogni componente usa un numero costante di bit” del corollario sulle componenti di dimensione costante. (Se ogni componente è memorizzata in una parola di memoria di esattamente $32$ bit, il numero di bit memorizzati è $32n$, di nuovo $\Theta(n)$.)

    4. La componente $a[i]=i$ usa $\lfloor\log_2 i\rfloor+1$ bit:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(|I|&#92;)</span></th>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(1+2=3&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(1+2+2=5&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(1+2+2+3=8&#92;)</span></td>
        </tr>
        <tr>
        <td>8</td>
        <td><span class="arithmatex">&#92;(1+2+2+3+3+3+3+4=21&#92;)</span></td>
        </tr>
        <tr>
        <td>16</td>
        <td><span class="arithmatex">&#92;(21+7&#92;cdot 4+5=54&#92;)</span></td>
        </tr>
        </table></div>

        <strong>Limite superiore.</strong> Poiché $i\le n$, ogni componente usa al più $\lfloor\log_2 n\rfloor+1\le\log_2 n+1\le 2\log_2 n$ bit per $n\ge 2$, quindi

        $$
        |I|\le 2n\log_2 n,\qquad \forall n\ge 2.
        $$

        <strong>Limite inferiore.</strong> Ogni componente usa almeno $\log_2 i$ bit (poiché $\lfloor\log_2 i\rfloor+1\ge\log_2 i$). Tenendo solo gli indici $i\ge \lceil n/2\rceil$, che sono almeno $n/2$ e sono almeno $n/2$ in numero,

        $$
        |I|\ge\sum_{i=\lceil n/2\rceil}^{n}\log_2 i\ge \frac n2\log_2\frac n2=\frac n2(\log_2 n-1)\ge \frac n4\log_2 n,
        $$

        dove l'ultima disuguaglianza vale quando $\log_2 n-1\ge\frac12\log_2 n$, cioè per $n\ge 4$.

        Quindi, con $c_1=\frac14$, $c_2=2$ e $n_1=4$,

        $$
        0\le \frac14\,n\log_2 n\le |I|\le 2\,n\log_2 n,\qquad\forall n\ge 4,
        $$

        cioè $|I|=\Theta(n\log_2 n)$. (Verifica: per $n=16$, $\frac14\cdot 16\cdot 4=16\le 54\le 2\cdot 16\cdot 4=128$.)

<a id="esercizio-11-3"></a>

!!! esercizio "Esercizio 11.3: Dimensione dell'input (E3)"

    Consideriamo il seguente algoritmo, e richiamiamo l'algoritmo <code>PrimalityTest</code> (divisione per tentativi per $d = 2, 3, \dots, \lfloor\sqrt n\rfloor$), il cui numero di passi nel caso peggiore ($n$ primo) è $S(n)=3\lfloor\sqrt n\rfloor+1$, con il corpo del suo ciclo while eseguito $\lfloor\sqrt n\rfloor-1$ volte.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> SumUpTo</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(1+2+&#92;cdots+n&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> SumUpTo(n)</span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s := 0&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s &#92;leftarrow s + i&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis3-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Calcolare il numero di passi $S(n)$ di <code>SumUpTo</code> e determinare il suo tempo di esecuzione nel caso peggiore $T(|I|)$. L'algoritmo è polinomiale?

    2. Proporre un algoritmo che calcola lo stesso output con un numero costante di passi (si assuma che le operazioni aritmetiche richiedano un numero costante di passi). È polinomiale?

    3. Dimostrare che <code>PrimalityTest</code> è esponenziale in $|I|$, anche se $S(n)=\Theta(\sqrt n)$ è “sublineare” nel valore $n$.

    4. Dare un limite superiore al numero di iterazioni del ciclo while di <code>PrimalityTest</code> per un numero primo $n$ di $32$ bit e di $64$ bit. Che cosa succede al numero di iterazioni quando la dimensione dell'input raddoppia?

??? soluzione "Soluzione"

    1. Il numero di volte in cui ogni riga di codice viene eseguita è:

        - <span style="color:#e03131">La riga</span> [2](#riga-es-11-dimensione-input-exis3-a) è eseguita $1$ volta

        - <span style="color:#e03131">La riga</span> [3](#riga-es-11-dimensione-input-exis3-b) è eseguita $1$ volta

        - <span style="color:#e03131">La riga</span> [4](#riga-es-11-dimensione-input-exis3-c) è eseguita $n+1$ volte

        - <span style="color:#e03131">La riga</span> [5](#riga-es-11-dimensione-input-exis3-d) è eseguita $n$ volte

        - <span style="color:#e03131">La riga</span> [6](#riga-es-11-dimensione-input-exis3-e) è eseguita $n$ volte

        - <span style="color:#e03131">La riga</span> [8](#riga-es-11-dimensione-input-exis3-f) è eseguita $1$ volta

        Quindi

        $$
        S(n)=1+1+(n+1)+n+n+1=3n+4=\Theta(n).
        $$

        L'input è un solo numero naturale, quindi $|I|=\lfloor\log_2 n\rfloor+1=\Theta(\log_2 n)$: esistono $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        c_1\log_2 n\le|I|\le c_2\log_2 n
        \quad\Longleftrightarrow\quad
        2^{\frac{1}{c_2}|I|}\le n\le 2^{\frac{1}{c_1}|I|}.
        $$

        Poiché $a_1n\le S(n)\le a_2 n$ per certi $a_1,a_2>0$,

        $$
        a_1 2^{\frac{1}{c_2}|I|}\le S(n)\le a_2 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad T(|I|)=2^{\Theta(|I|)},
        $$

        poiché i fattori costanti $a_1$ e $a_2$ sono assorbiti nell'esponente (Osservazione «fattori costanti nell'esponente» del capitolo). Il caso peggiore si può anche calcolare esattamente. Gli input di dimensione $|I|$ sono i numeri $n$ con $2^{|I|-1}\le n\le 2^{|I|}-1$, e $S(n)=3n+4$ è massimo per $n=2^{|I|}-1$, quindi

        $$
        T(|I|)=3\big(2^{|I|}-1\big)+4=3\cdot 2^{|I|}+1 .
        $$

        !!! chiave ""

            <code>SumUpTo</code> è lineare nel valore $n$ ma <strong>esponenziale</strong> nella dimensione dell'input: non è polinomiale.

    2. Per la formula di Gauss, $1+2+\cdots+n=\dfrac{n(n+1)}{2}$. L'algoritmo “<strong>return</strong> $n(n+1)/2$” esegue un numero costante di passi (una somma, un prodotto, una divisione, un return), quindi $T(|I|)=\Theta(1)=O(|I|^0)$: è polinomiale.

    3. L'input è un solo numero naturale, quindi come sopra $2^{\frac{1}{c_2}|I|}\le n\le 2^{\frac{1}{c_1}|I|}$. Estraendo le radici quadrate (tutti i termini sono positivi),

        $$
        2^{\frac{1}{2c_2}|I|}\le\sqrt n\le 2^{\frac{1}{2c_1}|I|}.
        $$

        Poiché $S(n)=\Theta(\sqrt n)$, esistono $a_1,a_2>0$ con $a_1\sqrt n\le S(n)\le a_2\sqrt n$, quindi

        $$
        a_1 2^{\frac{1}{2c_2}|I|}\le S(n)\le a_2 2^{\frac{1}{2c_1}|I|},
        \qquad\text{quindi}\qquad T(|I|)=2^{\Theta(|I|)},
        $$

        poiché i fattori costanti $a_1$ e $a_2$ sono assorbiti nell'esponente (Osservazione «fattori costanti nell'esponente» del capitolo). Essere sublineare in $n$ non aiuta: $\sqrt n=2^{\frac12\log_2 n}$ è ancora esponenziale nel numero di bit $\log_2 n$. L'algoritmo non è polinomiale: per ogni costante $k$, $\lim_{|I|\to\infty}2^{c|I|}/|I|^k=+\infty$ per ogni $c>0$.

    4. Il ciclo while è eseguito $\lfloor\sqrt n\rfloor-1$ volte per un $n$ primo.

        - $32$ bit: $n<2^{32}$, quindi $\sqrt n<2^{16}=65\,536$ e il ciclo esegue meno di $65\,536$ iterazioni.

        - $64$ bit: $n<2^{64}$, quindi $\sqrt n<2^{32}=4\,294\,967\,296$ e il ciclo esegue fino a circa $4.3\cdot 10^{9}$ iterazioni.

        Quando la dimensione dell'input raddoppia (da $32$ a $64$ bit) il limite sul numero di iterazioni viene <strong>elevato al quadrato</strong> ($2^{16}\to 2^{32}$), mentre per un algoritmo polinomiale con $T(|I|)=\Theta(|I|^k)$ verrebbe solo moltiplicato per la costante $2^k$.

<a id="esercizio-11-4"></a>

!!! esercizio "Esercizio 11.4: Dimensione dell'input (E4)"

    Consideriamo i due algoritmi seguenti. Entrambi contengono due cicli annidati.

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> CountPairs</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero di coppie <span class="arithmatex">&#92;((i,j)&#92;)</span> con <span class="arithmatex">&#92;(i,j&#92;in&#92;{1, 2, &#92;dots, n&#92;}&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> CountPairs(n)</span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := 0&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c &#92;leftarrow c + 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4-i"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <div class="pseudocodice" markdown="0"><div class="pc-titolo"><strong>Algoritmo:</strong> CountInversions</div>
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;ge 1&#92;)</span> numeri naturali</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero di coppie <span class="arithmatex">&#92;(i&lt;j&#92;)</span> con <span class="arithmatex">&#92;(a&#91;i&#93;&gt;a&#91;j&#93;&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> CountInversions(a, n)</span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := 0&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n-1&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := i+1&#92;)</span></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; a&#91;j&#93;&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c &#92;leftarrow c + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-i"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga" id="riga-es-11-dimensione-input-exis4b-j"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    **Domande**

    1. Calcolare il numero di passi $S(n)$ di <code>CountPairs</code> e il suo tempo di esecuzione nel caso peggiore $T(|I|)$.

    2. Calcolare il numero di passi $S(n)$ di <code>CountInversions</code> nel caso peggiore e il suo tempo di esecuzione nel caso peggiore $T(|I|)$, in generale e sotto l'ipotesi che ogni componente usi un numero costante di bit.

    3. Entrambi gli algoritmi hanno $S(n)=\Theta(n^2)$. Spiegare perché uno è polinomiale e l'altro è esponenziale nella dimensione dell'input.

    4. Supponiamo che <code>CountInversions</code> riceva anche il numero $n$ come parte dell'input. Calcolare $|I|$ per $n=5$, $a=[5,2,4,1,3]$, e spiegare perché la conclusione della domanda 2 non cambia.

??? soluzione "Soluzione"

    1. Il numero di volte in cui ogni riga di codice viene eseguita è:

        - <span style="color:#e03131">Le righe</span> [2](#riga-es-11-dimensione-input-exis4-a), [3](#riga-es-11-dimensione-input-exis4-b) e [12](#riga-es-11-dimensione-input-exis4-i) sono eseguite $1$ volta ciascuna

        - <span style="color:#e03131">La riga</span> [4](#riga-es-11-dimensione-input-exis4-c) è eseguita $n+1$ volte

        - <span style="color:#e03131">Le righe</span> [5](#riga-es-11-dimensione-input-exis4-d) e [10](#riga-es-11-dimensione-input-exis4-h) sono eseguite $n$ volte ciascuna

        - <span style="color:#e03131">La riga</span> [6](#riga-es-11-dimensione-input-exis4-e) è eseguita $n(n+1)$ volte

        - <span style="color:#e03131">Le righe</span> [7](#riga-es-11-dimensione-input-exis4-f) e [8](#riga-es-11-dimensione-input-exis4-g) sono eseguite $n^2$ volte ciascuna

        Quindi

        $$
        S(n)=3+(n+1)+2n+n(n+1)+2n^2=3n^2+4n+4=\Theta(n^2).
        $$

        L'input è un solo numero naturale, quindi $|I|=\Theta(\log_2 n)$ e, come per ogni input costituito da un solo numero, $2^{\frac{1}{c_2}|I|}\le n\le 2^{\frac{1}{c_1}|I|}$ per certi $c_1,c_2>0$. Elevando al quadrato,

        $$
        2^{\frac{2}{c_2}|I|}\le n^2\le 2^{\frac{2}{c_1}|I|},
        $$

        e poiché $a_1n^2\le S(n)\le a_2n^2$ per certi $a_1,a_2>0$, assorbendo i fattori costanti nell'esponente (Osservazione «fattori costanti nell'esponente» del capitolo) otteniamo

        $$
        T(|I|)=2^{\Theta(|I|)}:
        $$

        <code>CountPairs</code> è esponenziale nella dimensione dell'input.

    2. Nel caso peggiore (array in ordine strettamente decrescente) la riga [8](#riga-es-11-dimensione-input-exis4b-g) è eseguita a ogni iterazione del ciclo interno. Per un $i$ fissato, il ciclo interno esegue $n-i$ iterazioni, per un totale di $\sum_{i=1}^{n-1}(n-i)=\frac{n(n-1)}{2}$. Il numero di volte in cui ogni riga viene eseguita è:

        - <span style="color:#e03131">Le righe</span> [2](#riga-es-11-dimensione-input-exis4b-a), [3](#riga-es-11-dimensione-input-exis4b-b) e [14](#riga-es-11-dimensione-input-exis4b-j) sono eseguite $1$ volta ciascuna

        - <span style="color:#e03131">La riga</span> [4](#riga-es-11-dimensione-input-exis4b-c) è eseguita $n$ volte

        - <span style="color:#e03131">Le righe</span> [5](#riga-es-11-dimensione-input-exis4b-d) e [12](#riga-es-11-dimensione-input-exis4b-i) sono eseguite $n-1$ volte ciascuna

        - <span style="color:#e03131">La riga</span> [6](#riga-es-11-dimensione-input-exis4b-e) è eseguita $\frac{n(n-1)}{2}+(n-1)$ volte

        - <span style="color:#e03131">Le righe</span> [7](#riga-es-11-dimensione-input-exis4b-f), [8](#riga-es-11-dimensione-input-exis4b-g) e [10](#riga-es-11-dimensione-input-exis4b-h) sono eseguite $\frac{n(n-1)}{2}$ volte ciascuna

        Quindi

        $$
        S(n)=3+n+3(n-1)+4\cdot\frac{n(n-1)}{2}=2n^2+2n=\Theta(n^2).
        $$

        L'input è un array, quindi $|I|=\Omega(n)$, cioè $n\le\frac1c|I|$, e

        $$
        S(n)\le a\,n^2\le\frac{a}{c^2}|I|^2
        \quad\Longrightarrow\quad
        T(|I|)=O(|I|^2).
        $$

        Se ogni componente usa al più $c$ bit, con $c$ una costante, allora $|I|=\Theta(n)$, e più precisamente $n\ge\frac1c|I|$. Per un limite inferiore, si noti che solo la riga [8](#riga-es-11-dimensione-input-exis4b-g) dipende dai valori: anche se non viene mai eseguita, l'algoritmo esegue

        $$
        2n^2+2n-\frac{n(n-1)}{2}=\frac{3n^2+5n}{2}\ge\frac32\,n^2\ge\frac{3}{2c^2}\,|I|^2
        $$

        passi. Ogni input di dimensione $|I|$ richiede almeno questo numero di passi, quindi $T(|I|)=\Omega(|I|^2)$ e, insieme al limite superiore,

        $$
        T(|I|)=\Theta(|I|^2).
        $$

        In entrambi i casi <code>CountInversions</code> è polinomiale (quadratico).

    3. Il numero di passi è la stessa funzione di $n$, ma $n$ ha una relazione diversa con la dimensione dell'input:

        - in <code>CountPairs</code>, $n$ è il <strong>valore</strong> dell'input, che si scrive con soli $\Theta(\log_2 n)$ bit, quindi $n=2^{\Theta(|I|)}$;

        - in <code>CountInversions</code>, $n$ è il <strong>numero di componenti</strong> dell'array, e ogni componente richiede almeno un bit, quindi $n=O(|I|)$.

        !!! chiave ""

            Lo stesso $S(n)$ può corrispondere a un tempo di esecuzione polinomiale o esponenziale: dipende da come il parametro $n$ è legato alla dimensione dell'input $|I|$.

    4. I bit di $n=5$ sono $\lfloor\log_2 5\rfloor+1=3$, e i bit dell'array sono $3+2+3+1+2=11$, quindi

        $$
        |I|=3+11=14.
        $$

        In generale $|I|=(\lfloor\log_2 n\rfloor+1)+\sum_{i=1}^{n}(\lfloor\log_2 a[i]\rfloor+1)\ge n$, quindi ancora $|I|=\Omega(n)$ e $T(|I|)=O(|I|^2)$. Con componenti di dimensione costante, $|I|=\Theta(\log_2 n)+\Theta(n)=\Theta(n)$, quindi $T(|I|)=\Theta(|I|^2)$ come prima: aggiungere $n$ all'input aggiunge solo $\Theta(\log_2 n)$ bit, trascurabili rispetto agli $\Omega(n)$ bit dell'array.
