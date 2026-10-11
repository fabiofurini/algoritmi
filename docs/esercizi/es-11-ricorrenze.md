---
title: "Esercizi · Equazioni di ricorrenza"
---

# Esercizi · Equazioni di ricorrenza

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 11** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 11](../analisi-ricorsione/11-ricorrenze.md) · [:material-file-pdf-box: Eserciziario, volume 2 (PDF)](../pdf/esercizi-2-analisi-ricorsione.pdf)

</div>

Negli esercizi di questo capitolo le ricorrenze sono risolte con i tre metodi del capitolo «Equazioni di ricorrenza» (espansione, sostituzione, albero di ricorsione), usando le formule seguenti.

!!! nota ""

    Per ogni $n,m\in\N$, $n,m\ge 1$, ogni $k\in\N$ e ogni numero reale $x\neq 1$:

    \begin{align*}
    \sum_{i=1}^{n} i &= \frac{n(n+1)}{2}
    && \text{(serie aritmetica)}\\[1ex]
    \sum_{j=1}^{m} j^2 &= \frac{m(m+1)(2m+1)}{6}
    && \text{(somma dei quadrati)}\\[1ex]
    \sum_{i=0}^{k} x^i &= \frac{x^{k+1}-1}{x-1}=\frac{1-x^{k+1}}{1-x}
    && \text{(serie geometrica)}\\[1ex]
    \sum_{i=0}^{\infty} x^i &= \frac{1}{1-x}\quad\text{se } |x|<1
    && \text{(serie geometrica infinita decrescente)}
    \end{align*}

!!! nota ""

    Per ogni $a,b,n>0$ con $b\neq 1$, e ogni numero reale $x$:

    \begin{align*}
    a^{\log_b n}&=n^{\log_b a}, \qquad \log_b n=\frac{\log_2 n}{\log_2 b},\\[1ex]
    x-1&<\lfloor x\rfloor\le x, \qquad 2\lfloor n/2\rfloor\ge n-1 \quad (n\in\N).
    \end{align*}

<a id="esercizio-11-1"></a>

!!! esercizio "Esercizio 11.1: Equazioni di ricorrenza (E1)"

    Consideriamo le seguenti ricorrenze.

    - **(a)** $T(n)=T(n-1)+2n-1$ per $n>1$, con $T(1)=1$.

    - **(b)** $T(n)=3\,T(n-1)$ per $n>1$, con $T(1)=2$.

    - **(c)** $T(n)=T\left(\frac{n}{3}\right)+1$ per $n>1$, con $T(1)=1$, dove $n$ è una potenza esatta di $3$.

    - **(d)** $T(n)=2\,T\left(\frac{n}{2}\right)+n^2$ per $n>1$, con $T(1)=1$, dove $n$ è una potenza esatta di $2$.

    **Domande**

    1. Per ciascuna ricorrenza, calcolare i primi quattro valori di $T(n)$ (per (c) e (d), sui primi quattro valori ammissibili di $n$).

    2. Risolvere ciascuna ricorrenza con il metodo di espansione, cioè determinare una forma chiusa di $T(n)$.

    3. Verificare che le forme chiuse siano coerenti con i valori calcolati alla domanda 1.

    4. Determinare l'ordine di grandezza di ciascuna ricorrenza (notazione $\Theta$).

??? soluzione "Soluzione"

    1. Primi valori:

        - (a) $T(1)=1$, $T(2)=1+3=4$, $T(3)=4+5=9$, $T(4)=9+7=16$.

        - (b) $T(1)=2$, $T(2)=6$, $T(3)=18$, $T(4)=54$.

        - (c) $T(1)=1$, $T(3)=T(1)+1=2$, $T(9)=T(3)+1=3$, $T(27)=T(9)+1=4$.

        - (d) $T(1)=1$, $T(2)=2\cdot 1+4=6$, $T(4)=2\cdot 6+16=28$, $T(8)=2\cdot 28+64=120$.

    2. Espansione.

        - **(a)** Espandendo,

            \begin{align*}
            T(n) &= T(n-1)+(2n-1)\\
            &= T(n-2)+\big(2(n-1)-1\big)+(2n-1)\\
            &\;\;\vdots\\
            &= T(n-k)+\sum_{i=n-k+1}^{n}(2i-1).
            \end{align*}

            Con $k=n-1$ e usando la serie aritmetica $\sum_{i=1}^{n}i=\frac{n(n+1)}{2}$:

            $$
            T(n)=T(1)+\sum_{i=2}^{n}(2i-1)=\sum_{i=1}^{n}(2i-1)=2\,\frac{n(n+1)}{2}-n=n^2.
            $$

        - **(b)** Espandendo,

            $$
            T(n)=3\,T(n-1)=3^2\,T(n-2)=3^3\,T(n-3)=\cdots=3^k\,T(n-k).
            $$

            Con $k=n-1$: $T(n)=3^{n-1}\,T(1)=2\cdot 3^{n-1}$.

        - **(c)** Sia $n=3^k$. Espandendo,

            $$
            T(n)=T\left(\frac{n}{3}\right)+1=T\left(\frac{n}{3^2}\right)+2=\cdots=T\left(\frac{n}{3^j}\right)+j.
            $$

            La condizione al contorno è raggiunta quando $\frac{n}{3^j}=1$, cioè $j=\log_3 n$:

            $$
            T(n)=T(1)+\log_3 n=\log_3 n+1.
            $$

        - **(d)** Espandendo,

            \begin{align*}
            T(n) &= 2\,T\left(\frac{n}{2}\right)+n^2\\
            &= 2\left(2\,T\left(\frac{n}{2^2}\right)+\frac{n^2}{4}\right)+n^2=2^2\,T\left(\frac{n}{2^2}\right)+n^2\left(1+\frac{1}{2}\right)\\
            &= 2^2\left(2\,T\left(\frac{n}{2^3}\right)+\frac{n^2}{16}\right)+n^2\left(1+\frac{1}{2}\right)=2^3\,T\left(\frac{n}{2^3}\right)+n^2\left(1+\frac{1}{2}+\frac{1}{4}\right)\\
            &\;\;\vdots\\
            &= 2^j\,T\left(\frac{n}{2^j}\right)+n^2\sum_{i=0}^{j-1}\left(\frac{1}{2}\right)^i.
            \end{align*}

            Con $j=\log_2 n$ (quindi $2^j=n$) e la serie geometrica $\sum_{i=0}^{j-1}x^i=\frac{1-x^j}{1-x}$:

            $$
            T(n)=n\,T(1)+n^2\,\frac{1-\left(\frac{1}{2}\right)^{\log_2 n}}{1-\frac{1}{2}}=n+2n^2\left(1-\frac{1}{n}\right)=2n^2-n.
            $$

    3. Verifica:

        - (a) $n^2$: $1,4,9,16$. ✓

        - (b) $2\cdot 3^{n-1}$: $2,6,18,54$. ✓

        - (c) $\log_3 n+1$ per $n=1,3,9,27$: $1,2,3,4$. ✓

        - (d) $2n^2-n$ per $n=1,2,4,8$: $1,\;8-2=6,\;32-4=28,\;128-8=120$. ✓

    4. Ordini di grandezza:

        - (a) $T(n)=n^2=\Theta(n^2)$.

        - (b) $T(n)=2\cdot 3^{n-1}=\frac{2}{3}\,3^n=\Theta(3^n)$ (esponenziale).

        - (c) $T(n)=\log_3 n+1=\Theta(\log_2 n)$ (la base del logaritmo è irrilevante dentro $\Theta$).

        - (d) $T(n)=2n^2-n=\Theta(n^2)$, poiché $\lim_{n\to\infty}\frac{2n^2-n}{n^2}=2\in\R_{>0}$. Si noti che il costo è dominato dalla radice ($n^2$).

<a id="esercizio-11-2"></a>

!!! esercizio "Esercizio 11.2: Equazioni di ricorrenza (E2)"

    Consideriamo le seguenti ricorrenze, definite per ogni $n\in\N$, $n\ge 1$.

    $$
    \text{(A)}\quad T(n)=
    \begin{cases}
    1 & \text{se } n=1\\
    T(n-1)+n & \text{se } n>1
    \end{cases}
    \qquad\qquad
    \text{(B)}\quad U(n)=
    \begin{cases}
    1 & \text{se } n=1\\
    U(\lfloor n/2\rfloor)+1 & \text{se } n>1
    \end{cases}
    $$

    **Domande**

    1. Usando il metodo di sostituzione, dimostrare che $T(n)\le n^2$ per ogni $n\ge 1$.

    2. Usando il metodo di sostituzione, dimostrare che $T(n)\ge \frac{1}{2}n^2$ per ogni $n\ge 1$. Concludere che $T(n)=\Theta(n^2)$.

    3. Calcolare $U(n)$ per $n=1,2,\dots,8$.

    4. Dimostrare che $U(n)=O(\log_2 n)$, mostrando che $U(n)\le c\log_2 n$ per un'opportuna costante $c$ e ogni $n\ge 2$. Spiegare perché la limitazione non può valere per $n=1$ e quali casi base servono.

    5. Dimostrare che $U(n)\ge\log_2(n+1)$ per ogni $n\ge 1$. Concludere che $U(n)=\Theta(\log_2 n)$.

??? soluzione "Soluzione"

    1. Ipotizziamo $T(n)\le c\,n^2$ e cerchiamo $c$. Supponiamo (ipotesi induttiva) $T(n-1)\le c\,(n-1)^2$. Allora

        $$
        T(n)\le c\,(n-1)^2+n=c\,n^2-2c\,n+c+n=c\,n^2-\big((2c-1)\,n-c\big).
        $$

        Ci serve $(2c-1)\,n-c\ge 0$. Con $c=1$ diventa $n-1\ge 0$, vero per ogni $n\ge 1$.

        <em>Caso base</em>: $T(1)=1\le 1^2$. ✓

        <em>Passo induttivo</em> ($n\ge 2$): $T(n)\le (n-1)^2+n=n^2-n+1\le n^2$. ✓

        Quindi $T(n)\le n^2$ per ogni $n\ge 1$, cioè $T(n)=O(n^2)$.

    2. Ipotizziamo $T(n)\ge d\,n^2$. Supponiamo $T(n-1)\ge d\,(n-1)^2$. Allora

        $$
        T(n)\ge d\,(n-1)^2+n=d\,n^2+\big((1-2d)\,n+d\big).
        $$

        Ci serve $(1-2d)\,n+d\ge 0$: con $d=\frac{1}{2}$ diventa $\frac{1}{2}\ge 0$. ✓

        <em>Caso base</em>: $T(1)=1\ge\frac{1}{2}$. ✓

        Quindi $\frac{1}{2}n^2\le T(n)\le n^2$ per ogni $n\ge 1$, e $T(n)=\Theta(n^2)$. (In effetti, la soluzione esatta è $T(n)=\frac{n(n+1)}{2}$.)

    3.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
        <th>7</th>
        <th>8</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(U(n)&#92;)</span></td>
        <td>1</td>
        <td>2</td>
        <td>2</td>
        <td>3</td>
        <td>3</td>
        <td>3</td>
        <td>3</td>
        <td>4</td>
        </tr>
        </table></div>

        Per esempio, $U(6)=U(3)+1=U(1)+2=3$ e $U(8)=U(4)+1=U(2)+2=U(1)+3=4$. (In generale $U(n)=\lfloor\log_2 n\rfloor+1$, il numero di bit di $n$.)

    4. Ipotizziamo $U(n)\le c\log_2 n$.

        <em>Passo induttivo.</em> Supponiamo $U(\lfloor n/2\rfloor)\le c\log_2\lfloor n/2\rfloor$. Allora

        $$
        U(n)\le c\log_2\lfloor n/2\rfloor+1\le c\log_2\frac{n}{2}+1=c\log_2 n-c+1\le c\log_2 n,
        $$

        purché $c\ge 1$.

        <em>Casi base.</em> Per $n=1$: $U(1)=1>c\log_2 1=0$ per ogni $c$, quindi la limitazione non può valere per $n=1$. Dimostriamo la limitazione per $n\ge n_0=2$. Per $n\ge 4$ si ha $\lfloor n/2\rfloor\ge 2$, quindi il passo induttivo usa solo valori $\ge 2$. Per $n=2,3$ si ha $\lfloor n/2\rfloor=1$: questi sono i casi base. Ci serve

        $$
        U(2)=2\le c\log_2 2=c, \qquad U(3)=2\le c\log_2 3\approx 1.58\,c.
        $$

        Entrambe valgono con $c=2$.

        Quindi $U(n)\le 2\log_2 n$ per ogni $n\ge 2$, e $U(n)=O(\log_2 n)$.

    5. Per induzione forte su $n$.

        <em>Caso base</em>: $U(1)=1=\log_2 2$. ✓

        <em>Passo induttivo</em> ($n\ge 2$): poiché $1\le\lfloor n/2\rfloor<n$, l'ipotesi induttiva dà

        $$
        U(\lfloor n/2\rfloor)\ge\log_2(\lfloor n/2\rfloor+1).
        $$

        Allora

        $$
        \begin{aligned}
        U(n)&\ge\log_2\left(\lfloor n/2\rfloor+1\right)+1=\log_2\left(2\lfloor n/2\rfloor+2\right)\\
        &\ge\log_2\left((n-1)+2\right)=\log_2(n+1),
        \end{aligned}
        $$

        dove abbiamo usato $2\lfloor n/2\rfloor\ge n-1$.

        Si noti che la scelta naturale $U(n)\ge\log_2 n$ <span style="color:#e03131">non</span> funziona direttamente: per $n$ dispari il passo induttivo dà soltanto

        $$
        U(n)\ge\log_2\lfloor n/2\rfloor+1=\log_2\left(2\lfloor n/2\rfloor\right)=\log_2(n-1).
        $$

        L'enunciato leggermente più forte $U(n)\ge\log_2(n+1)$ fa funzionare l'induzione.

        Poiché $\log_2(n+1)\ge\log_2 n$, si ha $U(n)=\Omega(\log_2 n)$. Insieme alla domanda 4,

        $$
        U(n)=\Theta(\log_2 n).
        $$

<a id="esercizio-11-3"></a>

!!! esercizio "Esercizio 11.3: Equazioni di ricorrenza (E3)"

    Consideriamo la ricorrenza

    $$
    T(n)=
    \begin{cases}
    1 & \text{se } n=1\\
    3\,T\left(\frac{n}{2}\right)+n & \text{se } n>1
    \end{cases}
    $$

    dove $n$ è una potenza esatta di $2$.

    **Domande**

    1. Disegnare i primi tre livelli dell'albero di ricorsione (profondità $0,1,2$) e indicare il costo di ciascun nodo.

    2. Determinare, per una profondità generica $i$, il numero di nodi, il costo di ciascun nodo e il costo del livello. Determinare la profondità dell'albero e il numero di foglie.

    3. Sommare i costi di tutti i livelli e ottenere una forma chiusa di $T(n)$.

    4. Determinare l'ordine di grandezza di $T(n)$. Quale parte dell'albero domina il costo totale?

    5. Verificare per induzione (metodo di sostituzione) la forma chiusa ottenuta alla domanda 3, e controllarla numericamente per $n=1,2,4,8$.

??? soluzione "Soluzione"

    1. La radice ha costo $n$ e tre figli, ciascuno con costo $\frac{n}{2}$; ciascuno di essi ha tre figli con costo $\frac{n}{4}$.

        ![Figura 1](../img/es-11-ricorrenze/fig01.svg){ .fig loading=lazy style="width:95%" }

    2. A profondità $i$:

        - numero di nodi: $3^i$;

        - dimensione di ciascun sottoproblema: $\frac{n}{2^i}$, quindi costo di ciascun nodo: $\frac{n}{2^i}$;

        - costo del livello: $3^i\,\frac{n}{2^i}=\left(\frac{3}{2}\right)^i n$.

        La dimensione del sottoproblema raggiunge $1$ quando $\frac{n}{2^i}=1$, cioè a profondità $k=\log_2 n$. Il numero di foglie è

        $$
        3^{\log_2 n}=n^{\log_2 3}\approx n^{1.585},
        $$

        ciascuna con costo $T(1)=1$.

    3. Sia $k=\log_2 n$. Usando la serie geometrica $\sum_{i=0}^{k-1}x^i=\frac{x^k-1}{x-1}$ con $x=\frac{3}{2}$:

        $$
        \sum_{i=0}^{k-1}\left(\frac{3}{2}\right)^i n=n\,\frac{\left(\frac{3}{2}\right)^k-1}{\frac{3}{2}-1}=2n\left(\frac{3^k}{2^k}-1\right)=2n\left(\frac{3^k}{n}-1\right)=2\cdot 3^k-2n.
        $$

        Aggiungendo il costo delle foglie, $3^k\cdot 1$:

        $$
        T(n)=2\cdot 3^k-2n+3^k=3\cdot 3^{\log_2 n}-2n=3\,n^{\log_2 3}-2n.
        $$

    4. Poiché $\log_2 3>1$, il termine $n^{\log_2 3}$ domina $n$:

        $$
        \lim_{n\to\infty}\frac{3\,n^{\log_2 3}-2n}{n^{\log_2 3}}=\lim_{n\to\infty}\left(3-\frac{2}{n^{\log_2 3-1}}\right)=3\in\R_{>0}.
        $$

        Quindi $T(n)=\Theta\left(n^{\log_2 3}\right)$. I costi dei livelli crescono geometricamente (ragione $\frac{3}{2}>1$): il costo totale è dominato dalle <strong>foglie</strong>.

    5. Dimostriamo $T(n)=3\,n^{\log_2 3}-2n$ per ogni $n=2^k$, per induzione su $k$.

        <em>Caso base</em> $k=0$ ($n=1$): $3\cdot 1-2=1=T(1)$. ✓

        <em>Passo induttivo</em>: supponiamo la formula valida per $\frac{n}{2}$. Poiché $\left(\frac{n}{2}\right)^{\log_2 3}=\frac{n^{\log_2 3}}{2^{\log_2 3}}=\frac{n^{\log_2 3}}{3}$,

        $$
        T(n)=3\left(3\,\frac{n^{\log_2 3}}{3}-2\,\frac{n}{2}\right)+n=3\,n^{\log_2 3}-3n+n=3\,n^{\log_2 3}-2n. \quad\checkmark
        $$

        <em>Verifica numerica</em> ($n^{\log_2 3}=3^k$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(T(n)&#92;)</span> dalla ricorrenza</th>
        <th><span class="arithmatex">&#92;(3&#92;cdot 3^k-2n&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3-2=1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;cdot 1+2=5&#92;)</span></td>
        <td><span class="arithmatex">&#92;(9-4=5&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;cdot 5+4=19&#92;)</span></td>
        <td><span class="arithmatex">&#92;(27-8=19&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;cdot 19+8=65&#92;)</span></td>
        <td><span class="arithmatex">&#92;(81-16=65&#92;)</span></td>
        </tr>
        </table></div>

<a id="esercizio-11-4"></a>

!!! esercizio "Esercizio 11.4: Equazioni di ricorrenza (E4)"

    Consideriamo le seguenti ricorrenze.

    $$
    \text{(A)}\quad T(n)=
    \begin{cases}
    1 & \text{se } 1\le n<4\\
    T\left(\frac{n}{2}\right)+T\left(\frac{n}{4}\right)+n & \text{se } n\ge 4
    \end{cases}
    \qquad \text{(definita per ogni numero reale } n\ge 1\text{)}
    $$

    $$
    \text{(B)}\quad U(n)=
    \begin{cases}
    0 & \text{se } n=0\\
    U(n-2)+n^2 & \text{se } n\ge 2
    \end{cases}
    \qquad \text{(definita per ogni } n\in\N\text{ pari)}
    $$

    **Domande**

    1. Disegnare i primi tre livelli dell'albero di ricorsione di (A) e calcolare il costo di ciascuno di questi livelli.

    2. Mostrare che il costo del livello a profondità $i$ dell'albero di (A) è al più $\left(\frac{3}{4}\right)^i n$, e usare questo fatto per ipotizzare una limitazione superiore per $T(n)$.

    3. Dimostrare, con il metodo di sostituzione, che $T(n)\le 4n$ per ogni $n\ge 1$. Concludere che $T(n)=\Theta(n)$.

    4. Disegnare l'albero di ricorsione di (B). Che forma ha? Qual è la sua profondità?

    5. Determinare una forma chiusa di $U(n)$ e il suo ordine di grandezza. (Si ricordi che $\sum_{j=1}^{m}j^2=\frac{m(m+1)(2m+1)}{6}$.)

??? soluzione "Soluzione"

    1. Ogni nodo di dimensione $s\ge 4$ ha due figli, di dimensioni $\frac{s}{2}$ e $\frac{s}{4}$.

        ![Figura 2](../img/es-11-ricorrenze/fig02.svg){ .fig loading=lazy style="width:90%" }

        I costi dei primi tre livelli (per $n$ abbastanza grande, in modo che tutti questi nodi siano interni) sono:

        $$
        n,\qquad \frac{n}{2}+\frac{n}{4}=\frac{3}{4}\,n,\qquad \frac{n}{4}+\frac{n}{8}+\frac{n}{8}+\frac{n}{16}=\frac{9}{16}\,n.
        $$

    2. Se un nodo ha dimensione $s$, i suoi figli hanno dimensione totale $\frac{s}{2}+\frac{s}{4}=\frac{3}{4}s$. Quindi, per induzione su $i$, i nodi a profondità $i$ hanno dimensione totale al più $\left(\frac{3}{4}\right)^i n$ (esattamente, se il livello è completo), e i nodi interni a profondità $i$ hanno costo totale al più $\left(\frac{3}{4}\right)^i n$.

        Sommando su tutti i livelli e usando la serie geometrica infinita decrescente $\sum_{i=0}^{\infty}x^i=\frac{1}{1-x}$:

        $$
        \sum_{i=0}^{\infty}\left(\frac{3}{4}\right)^i n=\frac{1}{1-\frac{3}{4}}\,n=4n.
        $$

        Poiché le foglie hanno costo costante, <strong>ipotizziamo</strong> $T(n)=O(n)$, più precisamente $T(n)\le 4n$. (Le foglie non sono facili da contare, quindi dimostriamo l'ipotesi con il metodo di sostituzione.)

    3. Dimostriamo $T(n)\le 4n$ per ogni numero reale $n\ge 1$, per induzione su $k=\lfloor\log_2 n\rfloor$.

        <em>Casi base</em> $k\in\{0,1\}$, cioè $1\le n<4$: $T(n)=1\le 4\le 4n$. ✓

        <em>Passo induttivo</em> $k\ge 2$, cioè $n\ge 4$: gli argomenti $\frac{n}{2}\ge 2$ e $\frac{n}{4}\ge 1$ sono nel dominio e hanno $\lfloor\log_2(\cdot)\rfloor<k$, quindi per l'ipotesi induttiva

        $$
        T(n)=T\left(\frac{n}{2}\right)+T\left(\frac{n}{4}\right)+n\le 4\,\frac{n}{2}+4\,\frac{n}{4}+n=2n+n+n=4n. \quad\checkmark
        $$

        Quindi $T(n)=O(n)$.

        <em>Limitazione inferiore</em>: per $n\ge 4$, tutti i termini sono non negativi e la sola radice costa $n$, quindi $T(n)\ge n$. Quindi $T(n)=\Omega(n)$ e

        $$
        T(n)=\Theta(n).
        $$

        (Il costo è dominato dalla radice: i costi dei livelli decrescono geometricamente con ragione $\frac{3}{4}$.)

    4. Ogni chiamata genera una <em>sola</em> chiamata ricorsiva, quindi l'albero di ricorsione è un <strong>cammino</strong>:

        $$
        n^2 \;\longrightarrow\; (n-2)^2 \;\longrightarrow\; (n-4)^2 \;\longrightarrow\;\cdots\;\longrightarrow\; 2^2 \;\longrightarrow\; U(0)=0.
        $$

        Il nodo a profondità $i$ ha dimensione $n-2i$ e costo $(n-2i)^2$. La dimensione raggiunge $0$ a profondità $\frac{n}{2}$, che è la profondità dell'albero.

    5. Sommando i costi di tutti i livelli, con $m=\frac{n}{2}$ e $j=m-i$ (in modo che $n-2i=2j$):

        $$
        U(n)=\sum_{i=0}^{m-1}(n-2i)^2=\sum_{j=1}^{m}(2j)^2=4\sum_{j=1}^{m}j^2=4\,\frac{m(m+1)(2m+1)}{6}.
        $$

        Sostituendo $m=\frac{n}{2}$:

        $$
        U(n)=4\,\frac{\frac{n}{2}\cdot\frac{n+2}{2}\cdot(n+1)}{6}=\frac{n(n+1)(n+2)}{6}.
        $$

        Verifica: $U(2)=4$ e $\frac{2\cdot 3\cdot 4}{6}=4$; $U(4)=4+16=20$ e $\frac{4\cdot 5\cdot 6}{6}=20$; $U(6)=20+36=56$ e $\frac{6\cdot 7\cdot 8}{6}=56$. ✓

        Ordine di grandezza:

        $$
        \lim_{n\to\infty}\frac{n(n+1)(n+2)/6}{n^3}=\frac{1}{6}\in\R_{>0}\qquad\Longrightarrow\qquad U(n)=\Theta(n^3).
        $$

        Si noti che, a differenza di (A), il costo dei livelli decresce solo lentamente (in modo polinomiale, non geometrico) e la profondità è lineare in $n$: nessun livello domina, e il totale è $\Theta(n)$ livelli per $\Theta(n^2)$ per livello (almeno metà dei livelli costa almeno $\frac{n^2}{4}$).

<a id="esercizio-11-5"></a>

!!! esercizio "Esercizio 11.5: Equazioni di ricorrenza (E5)"

    Consideriamo i seguenti due algoritmi ricorsivi. Supponiamo che ogni moltiplicazione sia un'operazione primitiva (un passo), e che $x$ sia memorizzato con un numero costante di bit.

    !!! algoritmo "Algoritmo: FastPower"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero intero <span class="arithmatex">&#92;(x&#92;)</span> e un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FastPower(x, n)</span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(y :=&#92;)</span> FastPower(<span class="arithmatex">&#92;(x, &#92;lfloor n/2&#92;rfloor&#92;)</span>)</span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n&#92;)</span> è pari <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(y&#92;cdot y&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-fp-f"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(x&#92;cdot y&#92;cdot y&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    !!! algoritmo "Algoritmo: SlowPower"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero intero <span class="arithmatex">&#92;(x&#92;)</span> e un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> SlowPower(x, n)</span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-sp-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-sp-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-sp-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n&#92;)</span> è pari <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-sp-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> SlowPower(<span class="arithmatex">&#92;(x, n/2&#92;)</span>) <span class="arithmatex">&#92;(&#92;cdot&#92;)</span> SlowPower(<span class="arithmatex">&#92;(x, n/2&#92;)</span>)</span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga" id="riga-es-11-ricorrenze-exfive-sp-e"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(x&#92;,&#92;cdot&#92;)</span> SlowPower(<span class="arithmatex">&#92;(x, &#92;lfloor n/2&#92;rfloor&#92;)</span>) <span class="arithmatex">&#92;(&#92;cdot&#92;)</span> SlowPower(<span class="arithmatex">&#92;(x, &#92;lfloor n/2&#92;rfloor&#92;)</span>)</span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa calcolano i due algoritmi? Giustificare la risposta.

    2. Sia $S_F(n)$ il numero di passi eseguiti da <code>FastPower</code>. Scrivere una ricorrenza per $S_F(n)$, contando le esecuzioni di ciascuna riga, e calcolare $S_F(n)$ per $n=0,1,\dots,8$.

    3. Risolvere la ricorrenza per $S_F(n)$ e determinarne l'ordine di grandezza.

    4. Sia $S_S(n)$ il numero di passi eseguiti da <code>SlowPower</code>. Scrivere una ricorrenza per $S_S(n)$ e risolverla con il metodo di espansione quando $n$ è una potenza esatta di $2$. Determinarne l'ordine di grandezza.

    5. Determinare il tempo di esecuzione nel caso peggiore dei due algoritmi in funzione della dimensione dell'input $|I|$, e confrontarli.

??? soluzione "Soluzione"

    1. Entrambi gli algoritmi calcolano $x^n$. Infatti, scrivendo $n=2\lfloor n/2\rfloor+r$ con $r\in\{0,1\}$,

        $$
        x^n=\left(x^{\lfloor n/2\rfloor}\right)^2\cdot x^{r}=
        \begin{cases}
        x^{n/2}\cdot x^{n/2} & \text{se } n \text{ è pari}\\
        x\cdot x^{\lfloor n/2\rfloor}\cdot x^{\lfloor n/2\rfloor} & \text{se } n \text{ è dispari}
        \end{cases}
        $$

        e $x^0=1$. Per induzione forte su $n$, se le chiamate ricorsive restituiscono $x^{\lfloor n/2\rfloor}$, entrambi gli algoritmi restituiscono $x^n$. L'unica differenza è che <code>FastPower</code> calcola $x^{\lfloor n/2\rfloor}$ <em>una volta</em> e lo memorizza in $y$, mentre <code>SlowPower</code> lo calcola <em>due volte</em>.

        <code>FastPower</code> è la funzione <code>powerRec</code> del codice del corso (in C++, <code>n / 2</code> è la divisione intera $\lfloor n/2\rfloor$ per $n\ge 0$):

        ```cpp
        long long powerRec(long long x, int n)
        {
        	if (n == 0)
        	{
        		return 1;
        	}

        	long long h = powerRec(x, n / 2);

        	if (n % 2 == 0)
        	{
        		return h * h;
        	}

        	return h * h * x;
        }
        ```

        Per $x=3$ e $n=0,1,\dots,10$ restituisce $1,3,9,27,81,243,729,2187,6561,19683,59049$, cioè $3^n$.

    2. <code>FastPower</code>.

        - Se $n=0$: le <span style="color:#e03131">righe</span> [2](#riga-es-11-ricorrenze-exfive-fp-a) e [3](#riga-es-11-ricorrenze-exfive-fp-b) sono eseguite una volta: $S_F(0)=2$.

        - Se $n\ge 1$: le <span style="color:#e03131">righe</span> [2](#riga-es-11-ricorrenze-exfive-fp-a), [5](#riga-es-11-ricorrenze-exfive-fp-c) e [6](#riga-es-11-ricorrenze-exfive-fp-d) sono eseguite una volta, ed esattamente una tra le <span style="color:#e03131">righe</span> [7](#riga-es-11-ricorrenze-exfive-fp-e) e [9](#riga-es-11-ricorrenze-exfive-fp-f) è eseguita una volta: $4$ passi. Inoltre, la chiamata ricorsiva alla riga [5](#riga-es-11-ricorrenze-exfive-fp-c) esegue $S_F(\lfloor n/2\rfloor)$ passi.

        Quindi

        $$
        S_F(n)=
        \begin{cases}
        2 & \text{se } n=0\\
        S_F(\lfloor n/2\rfloor)+4 & \text{se } n\ge 1
        \end{cases}
        $$

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th>0</th>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
        <th>7</th>
        <th>8</th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(S&#95;F(n)&#92;)</span></td>
        <td>2</td>
        <td>6</td>
        <td>10</td>
        <td>10</td>
        <td>14</td>
        <td>14</td>
        <td>14</td>
        <td>14</td>
        <td>18</td>
        </tr>
        </table></div>

    3. Espandendo,

        $$
        S_F(n)=S_F(\lfloor n/2\rfloor)+4=S_F(\lfloor n/4\rfloor)+8=\cdots=S_F\left(\lfloor n/2^j\rfloor\right)+4j.
        $$

        Per $n\ge 1$, $\lfloor n/2^j\rfloor=0$ per la prima volta quando $2^j>n$, cioè per $j=\lfloor\log_2 n\rfloor+1$ (il numero di bit di $n$). Quindi

        $$
        S_F(n)=4\left(\lfloor\log_2 n\rfloor+1\right)+2 \qquad (n\ge 1).
        $$

        Verifica: $S_F(1)=4+2=6$, $S_F(3)=8+2=10$, $S_F(8)=16+2=18$. ✓

        Poiché $\log_2 n-1<\lfloor\log_2 n\rfloor\le\log_2 n$, si ha $4\log_2 n+2<S_F(n)\le 4\log_2 n+6$, e

        $$
        S_F(n)=\Theta(\log_2 n).
        $$

    4. <code>SlowPower</code>.

        - Se $n=0$: <span style="color:#e03131">righe</span> [2](#riga-es-11-ricorrenze-exfive-sp-a) e [3](#riga-es-11-ricorrenze-exfive-sp-b): $S_S(0)=2$.

        - Se $n\ge 1$: <span style="color:#e03131">righe</span> [2](#riga-es-11-ricorrenze-exfive-sp-a), [5](#riga-es-11-ricorrenze-exfive-sp-c) e una tra [6](#riga-es-11-ricorrenze-exfive-sp-d), [8](#riga-es-11-ricorrenze-exfive-sp-e): $3$ passi, più <em>due</em> chiamate ricorsive su $\lfloor n/2\rfloor$.

        Quindi

        $$
        S_S(n)=
        \begin{cases}
        2 & \text{se } n=0\\
        2\,S_S(\lfloor n/2\rfloor)+3 & \text{se } n\ge 1
        \end{cases}
        $$

        in modo che $S_S(1)=2\cdot 2+3=7$. Sia $n=2^k$. Espandendo fino a $S_S(1)$:

        \begin{align*}
        S_S(n) &= 2\,S_S\left(\frac{n}{2}\right)+3\\
        &= 2^2\,S_S\left(\frac{n}{2^2}\right)+3\,(2+1)\\
        &= 2^3\,S_S\left(\frac{n}{2^3}\right)+3\,(2^2+2+1)\\
        &\;\;\vdots\\
        &= 2^k\,S_S(1)+3\sum_{i=0}^{k-1}2^i=7\cdot 2^k+3\left(2^k-1\right)=10\,n-3.
        \end{align*}

        Verifica: $S_S(1)=7$, $S_S(2)=2\cdot 7+3=17=20-3$, $S_S(4)=2\cdot 17+3=37=40-3$. ✓

        Quindi $S_S(n)=\Theta(n)$ per $n$ potenza di $2$. (Per un generico $n\ge 1$, $S_S(n)$ dipende solo dal numero di bit di $n$, e $S_S(n)=10\cdot 2^{\lfloor\log_2 n\rfloor}-3$, che è compreso tra $5n-3$ e $10n-3$: ancora $\Theta(n)$.)

    5. L'input è costituito da $x$ (un numero costante di bit) e dal numero naturale $n$, quindi

        $$
        |I|=\Theta(\log_2 n), \qquad\text{cioè}\qquad n=2^{\Theta(|I|)}.
        $$

        - <code>FastPower</code>: $S_F(n)=\Theta(\log_2 n)=\Theta(|I|)$.

        - <code>SlowPower</code>: $S_S(n)=\Theta(n)=2^{\Theta(|I|)}$.

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>FastPower</code> è $T(|I|)=\Theta(|I|)$ (lineare nella dimensione dell'input), mentre il tempo di esecuzione nel caso peggiore di <code>SlowPower</code> è $T(|I|)=2^{\Theta(|I|)}$ (esponenziale nella dimensione dell'input).

        Calcolare lo stesso sotto-risultato due volte cambia la ricorrenza da $S(n)=S(n/2)+c$ a $S(n)=2S(n/2)+c$, e il tempo di esecuzione da logaritmico a lineare in $n$.

<a id="esercizio-11-6"></a>

!!! esercizio "Esercizio 11.6: Equazioni di ricorrenza (E6)"

    Consideriamo le seguenti ricorrenze, dove $n$ è una potenza esatta di $2$.

    $$
    \text{(A)}\quad T(n)=
    \begin{cases}
    1 & \text{se } n=1\\
    4\,T\left(\frac{n}{2}\right)+n & \text{se } n>1
    \end{cases}
    \qquad\qquad
    \text{(B)}\quad U(n)=
    \begin{cases}
    1 & \text{se } n=1\\
    8\,U\left(\frac{n}{2}\right)+n^2 & \text{se } n>1
    \end{cases}
    $$

    **Domande**

    1. Provare a dimostrare $T(n)\le c\,n^2$ con il metodo di sostituzione. Mostrare che l'induzione fallisce per ogni scelta della costante $c$.

    2. Rafforzare l'ipotesi sottraendo un termine di ordine inferiore: dimostrare che $T(n)\le c\,n^2-d\,n$ per opportune costanti $c,d>0$, trattando il caso base.

    3. Dimostrare che $T(n)\ge n^2$ e concludere che $T(n)=\Theta(n^2)$.

    4. Ripetere le domande 1–3 per $U(n)$, con l'ipotesi $U(n)\le c\,n^3$.

    5. Usando il metodo dell'albero di ricorsione, calcolare il valore esatto di $U(n)$ e confrontarlo con la limitazione ottenuta alla domanda 4.

??? soluzione "Soluzione"

    1. Supponiamo $T\left(\frac{n}{2}\right)\le c\left(\frac{n}{2}\right)^2$. Allora

        $$
        T(n)\le 4\,c\,\frac{n^2}{4}+n=c\,n^2+n.
        $$

        Poiché $n>0$, $c\,n^2+n>c\,n^2$ per ogni $c$: non possiamo concludere $T(n)\le c\,n^2$. L'induzione fallisce, a causa del termine di ordine inferiore $n$. (Nota: concludere “$T(n)\le c\,n^2+n=O(n^2)$” sarebbe <span style="color:#e03131">sbagliato</span>: l'induzione deve dimostrare esattamente l'ipotesi induttiva, con la stessa costante $c$.)

    2. Ipotizziamo $T(n)\le c\,n^2-d\,n$. Supponiamo $T\left(\frac{n}{2}\right)\le c\left(\frac{n}{2}\right)^2-d\,\frac{n}{2}$. Allora

        $$
        T(n)\le 4\left(c\,\frac{n^2}{4}-d\,\frac{n}{2}\right)+n=c\,n^2-2d\,n+n=c\,n^2-d\,n-(d-1)\,n\le c\,n^2-d\,n,
        $$

        purché $d\ge 1$.

        <em>Caso base</em>: $T(1)=1\le c-d$. Con $d=1$ serve $c\ge 2$.

        Scegliendo $c=2$ e $d=1$: $T(n)\le 2n^2-n$ per ogni $n$ potenza di $2$. Quindi $T(n)=O(n^2)$. (In effetti, $T(n)=2n^2-n$ esattamente, come si può verificare con il metodo dell'albero di ricorsione.)

    3. Supponiamo $T\left(\frac{n}{2}\right)\ge\left(\frac{n}{2}\right)^2$. Allora

        $$
        T(n)\ge 4\,\frac{n^2}{4}+n=n^2+n\ge n^2.
        $$

        Caso base: $T(1)=1\ge 1$. Quindi $n^2\le T(n)\le 2n^2-n$, e $T(n)=\Theta(n^2)$.

    4. <em>Ipotesi ingenua.</em> Supponiamo $U\left(\frac{n}{2}\right)\le c\left(\frac{n}{2}\right)^3$. Allora

        $$
        U(n)\le 8\,c\,\frac{n^3}{8}+n^2=c\,n^3+n^2,
        $$

        e l'induzione fallisce (a causa del termine di ordine inferiore $n^2$).

        <em>Ipotesi rafforzata.</em> Supponiamo $U\left(\frac{n}{2}\right)\le c\left(\frac{n}{2}\right)^3-d\left(\frac{n}{2}\right)^2$. Allora

        $$
        U(n)\le 8\left(c\,\frac{n^3}{8}-d\,\frac{n^2}{4}\right)+n^2=c\,n^3-2d\,n^2+n^2=c\,n^3-d\,n^2-(d-1)\,n^2\le c\,n^3-d\,n^2,
        $$

        purché $d\ge 1$. Caso base: $U(1)=1\le c-d$, soddisfatto da $c=2$, $d=1$. Quindi

        $$
        U(n)\le 2n^3-n^2.
        $$

        <em>Limitazione inferiore.</em> Supponiamo $U\left(\frac{n}{2}\right)\ge\left(\frac{n}{2}\right)^3$. Allora $U(n)\ge 8\,\frac{n^3}{8}+n^2\ge n^3$; caso base $U(1)=1\ge 1$. Quindi $n^3\le U(n)\le 2n^3-n^2$, e $U(n)=\Theta(n^3)$.

    5. A profondità $i$ l'albero di ricorsione di (B) ha $8^i$ nodi, ciascuno di dimensione $\frac{n}{2^i}$ e costo $\left(\frac{n}{2^i}\right)^2$. Il costo del livello è

        $$
        8^i\,\frac{n^2}{4^i}=2^i\,n^2.
        $$

        La profondità dell'albero è $\log_2 n$, e ci sono $8^{\log_2 n}=n^{\log_2 8}=n^3$ foglie, ciascuna con costo $U(1)=1$. Usando $\sum_{i=0}^{k-1}2^i=2^k-1$:

        $$
        U(n)=\sum_{i=0}^{\log_2 n-1}2^i\,n^2+n^3=n^2\left(2^{\log_2 n}-1\right)+n^3=n^2(n-1)+n^3=2n^3-n^2.
        $$

        La limitazione della domanda 4 è quindi <em>esatta</em>: l'ipotesi rafforzata $c\,n^3-d\,n^2$ con $c=2$, $d=1$ è esattamente la soluzione della ricorrenza.

        Verifica numerica: $U(2)=8+4=12=16-4$, $U(4)=8\cdot 12+16=112=128-16$, $U(8)=8\cdot 112+64=960=1024-64$. ✓
