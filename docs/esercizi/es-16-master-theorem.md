---
title: "Esercizi · Il Master theorem"
---

# Esercizi · Il Master theorem

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 16** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 16](../ricorsione/16-master-theorem.md) · [:material-file-pdf-box: Eserciziario, volume 5 (PDF)](../pdf/esercizi-5-ricorsione.pdf)

</div>

Negli esercizi di questo capitolo le ricorrenze in forma standard $T(n)=a\,T(n/b)+f(n)$, con costanti $a\ge 1$, $b>1$ e $f(n)$ asintoticamente positiva, sono risolte con il Master theorem del capitolo «Il Master theorem», seguendo lo schema in cinque passi (identificare, calcolare $n^{\log_b a}$, confrontare, verificare, concludere). Si usano le formule seguenti.

!!! nota ""

    I tre casi del Master theorem:

    - <strong>Caso 1</strong>: se $f(n)=O\big(n^{\log_b a-\epsilon}\big)$ per qualche $\epsilon>0$, allora $T(n)=\Theta\big(n^{\log_b a}\big)$.

    - <strong>Caso 2</strong>: se $f(n)=\Theta\big(n^{\log_b a}\log^k n\big)$ per qualche $k\ge 0$, allora $T(n)=\Theta\big(n^{\log_b a}\log^{k+1} n\big)$.

    - <strong>Caso 3</strong>: se $f(n)=\Omega\big(n^{\log_b a+\epsilon}\big)$ per qualche $\epsilon>0$ e $a\,f(n/b)\le c\,f(n)$ per qualche $c<1$ e per ogni $n$ grande (condizione di regolarità), allora $T(n)=\Theta\big(f(n)\big)$.

!!! nota ""

    Costo dell'albero di ricorsione, per $n$ potenza esatta di $b$:

    $$
    T(n)=T(1)\,n^{\log_b a}+\sum_{j=0}^{\log_b n-1}a^j f\left(\frac{n}{b^j}\right),
    \qquad a^{\log_b n}=n^{\log_b a}.
    $$

    Numeri armonici: $H_L=\sum_{i=1}^{L}\frac{1}{i}$ soddisfa $\ln(L+1)\le H_L\le 1+\ln L$; inoltre $\sum_{i=1}^{\infty}\frac{1}{i^2}=\frac{\pi^2}{6}$.

<a id="esercizio-16-1"></a>

!!! esercizio "Esercizio 16.1: Il Master theorem (E1)"

    Consideriamo le seguenti ricorrenze ($\log$ denota $\log_2$):

    - **(a)** $T(n)=9\,T(n/3)+n$;

    - **(b)** $T(n)=2\,T(n/4)+\sqrt{n}$;

    - **(c)** $T(n)=2\,T(n/2)+n^2$;

    - **(d)** $T(n)=4\,T(n/2)+n^2\log n$;

    - **(e)** $T(n)=6\,T(n/3)+n^2\log n$.

    **Domande**

    1. Per ciascuna ricorrenza, identificare $a$, $b$, $f(n)$ e calcolare $n^{\log_b a}$.

    2. Per ciascuna ricorrenza, determinare quale caso del Master theorem si applica, verificarne tutte le ipotesi ($\epsilon$, $k$, condizione di regolarità) e dare l'ordine di grandezza di $T(n)$.

    3. Per la ricorrenza (c), calcolare $T(n)$ esattamente per $n=2^L$ supponendo $T(1)=1$, e verificare il risultato della domanda precedente.

??? soluzione "Soluzione"

    1.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">&#92;(a&#92;)</span></th>
        <th><span class="arithmatex">&#92;(b&#92;)</span></th>
        <th><span class="arithmatex">&#92;(f(n)&#92;)</span></th>
        <th><span class="arithmatex">&#92;(n^{&#92;log&#95;b a}&#92;)</span></th>
        </tr>
        <tr>
        <td>(a)</td>
        <td>9</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n^{&#92;log&#95;3 9}=n^2&#92;)</span></td>
        </tr>
        <tr>
        <td>(b)</td>
        <td>2</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(&#92;sqrt n&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n^{&#92;log&#95;4 2}=n^{1/2}=&#92;sqrt n&#92;)</span></td>
        </tr>
        <tr>
        <td>(c)</td>
        <td>2</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(n^2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n^{&#92;log&#95;2 2}=n&#92;)</span></td>
        </tr>
        <tr>
        <td>(d)</td>
        <td>4</td>
        <td>2</td>
        <td><span class="arithmatex">&#92;(n^2&#92;log n&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n^{&#92;log&#95;2 4}=n^2&#92;)</span></td>
        </tr>
        <tr>
        <td>(e)</td>
        <td>6</td>
        <td>3</td>
        <td><span class="arithmatex">&#92;(n^2&#92;log n&#92;)</span></td>
        <td><span class="arithmatex">&#92;(n^{&#92;log&#95;3 6}&#92;approx n^{1.631}&#92;)</span></td>
        </tr>
        </table></div>

    2. Seguiamo lo schema: identificare $\to$ calcolare $n^{\log_b a}$ $\to$ confrontare $\to$ verificare $\to$ concludere.

        - **(a)** $n^2$ è polinomialmente più grande di $f(n)=n$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>. Infatti $f(n)=n=O(n^{2-\epsilon})$ con $\epsilon=1$. Quindi

            $$
            T(n)=\Theta(n^2).
            $$

        - **(b)** $n^{1/2}$ e $f(n)=\sqrt n$ hanno lo stesso ordine $\longrightarrow$ <span style="color:#e03131">caso 2</span>: $f(n)=\Theta(n^{1/2}\log^k n)$ con $k=0$. Quindi

            $$
            T(n)=\Theta(\sqrt n\,\log n).
            $$

        - **(c)** $n$ è polinomialmente più piccolo di $f(n)=n^2$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>. $f(n)=n^2=\Omega(n^{1+\epsilon})$ con $\epsilon=1$. Condizione di regolarità:

            $$
            2\,f\left(\frac n2\right)=2\,\frac{n^2}{4}=\frac12\,n^2=c\,f(n)\qquad\text{con } c=\frac12<1,
            $$

            per ogni $n$. Quindi

            $$
            T(n)=\Theta(n^2).
            $$

        - **(d)** $f(n)=n^2\log n$ è più grande di $n^2$ solo di un fattore $\log n$ (non polinomialmente) e ha la forma $n^{\log_b a}\log^k n$ $\longrightarrow$ <span style="color:#e03131">caso 2</span> con $k=1$. Quindi

            $$
            T(n)=\Theta(n^2\log^2 n).
            $$

        - **(e)** $n^{1.631}$ è polinomialmente più piccolo di $f(n)=n^2\log n$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>. Poiché $n^2\log n\ge n^2$ per $n\ge2$, $f(n)=\Omega(n^{\log_3 6+\epsilon})$ con $\epsilon=2-\log_3 6\approx0.369>0$. Condizione di regolarità: per $n\ge3$, poiché $\log(n/3)\le\log n$,

            $$
            6\,f\left(\frac n3\right)=6\,\frac{n^2}{9}\log\frac n3\le\frac23\,n^2\log n=c\,f(n)\qquad\text{con } c=\frac23<1.
            $$

            Quindi

            $$
            T(n)=\Theta(n^2\log n).
            $$

    3. Con l'albero di ricorsione (Lemma del costo dell'albero di ricorsione), con $n=2^L$, $a=2$, $T(1)=1$:

        $$
        T(n)=2^L\cdot 1+\sum_{j=0}^{L-1}2^j\left(\frac{n}{2^j}\right)^2=n+n^2\sum_{j=0}^{L-1}\left(\frac12\right)^j
        =n+n^2\,\frac{1-(1/2)^L}{1-1/2}=n+2n^2\left(1-\frac1n\right)=2n^2-n .
        $$

        Verifica con la ricorrenza: $T(2)=2+4=6=2\cdot4-2$, $T(4)=12+16=28=2\cdot16-4$, $T(8)=56+64=120=2\cdot 64-8$. Poiché

        $$
        \lim_{n\to\infty}\frac{2n^2-n}{n^2}=2\in\R_{>0},
        $$

        si ha $T(n)=\Theta(n^2)$, come trovato con il caso 3. Si noti che i costi dei livelli $n^2(1/2)^j$ decrescono geometricamente: domina la radice.

<a id="esercizio-16-2"></a>

!!! esercizio "Esercizio 16.2: Il Master theorem (E2)"

    Consideriamo le seguenti ricorrenze ($\log$ denota $\log_2$):

    - **(a)** $T(n)=4\,T(n/2)+n^2/\log n$;

    - **(b)** $T(n)=n\,T(n/2)+n$;

    - **(c)** $T(n)=3\,T(n/3)+n/2$;

    - **(d)** $T(n)=T(n-2)+\log n$;

    - **(e)** $T(n)=64\,T(n/8)-n^2\log n$;

    - **(f)** $T(n)=\sqrt2\,T(n/2)+\log n$.

    **Domande**

    1. Per ciascuna ricorrenza, dire se il Master theorem può essere applicato. In caso contrario, spiegare con precisione quale ipotesi non vale.

    2. Per le ricorrenze a cui il teorema si applica, dare l'ordine di grandezza di $T(n)$, seguendo lo schema consueto.

    3. Per la ricorrenza (a), determinare l'ordine di grandezza di $T(n)$ per $n=2^L$ e $T(1)=1$ usando l'albero di ricorsione.

??? soluzione "Soluzione"

    1. - **(a)** <strong>Non applicabile.</strong> $a=4$, $b=2$, $n^{\log_2 4}=n^2$, $f(n)=n^2/\log n$. $f(n)$ è più piccola di $n^2$ ma non polinomialmente più piccola: per ogni $\epsilon>0$

            $$
            \lim_{n\to\infty}\frac{n^2/\log n}{n^{2-\epsilon}}=\lim_{n\to\infty}\frac{n^\epsilon}{\log n}=+\infty,
            $$

            quindi il caso 1 non vale; il caso 2 richiederebbe $k=-1<0$; il caso 3 non vale poiché $f(n)$ è più piccola di $n^2$. Questo è un <strong>vuoto</strong> tra il caso 1 e il caso 2.

        - **(b)** <strong>Non applicabile.</strong> Il numero di sottoproblemi $a=n$ non è una costante.

        - **(c)** <strong>Applicabile</strong>: $a=3$, $b=3$, $f(n)=n/2$ (si veda la domanda 2).

        - **(d)** <strong>Non applicabile.</strong> Il sottoproblema ha dimensione $n-2$, non $n/b$: la ricorrenza non è in forma standard.

        - **(e)** <strong>Non applicabile.</strong> $f(n)=-n^2\log n<0$ per ogni $n\ge2$: $f$ non è asintoticamente positiva.

        - **(f)** <strong>Applicabile</strong>: $a=\sqrt2\ge1$, $b=2$, $f(n)=\log n$ (si veda la domanda 2). Si noti che $a$ non deve necessariamente essere un intero.

    2. - **(c)** $n^{\log_b a}=n^{\log_3 3}=n$. $f(n)=n/2$ ha lo stesso ordine di $n$ $\longrightarrow$ <span style="color:#e03131">caso 2</span>: $f(n)=\Theta(n\log^k n)$ con $k=0$ (i fattori costanti non contano). Quindi

            $$
            T(n)=\Theta(n\log n).
            $$

        - **(f)** $n^{\log_b a}=n^{\log_2\sqrt2}=n^{1/2}$. $f(n)=\log n$ è polinomialmente più piccola di $n^{1/2}$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>. Infatti, con $\epsilon=\frac14$,

            $$
            \lim_{n\to\infty}\frac{\log n}{n^{1/2-1/4}}=\lim_{n\to\infty}\frac{\log n}{n^{1/4}}=0^+,
            $$

            quindi $f(n)=O(n^{1/2-\epsilon})$. Quindi

            $$
            T(n)=\Theta(\sqrt n).
            $$

        Anche se il Master theorem non si applica a (d), questa ricorrenza è facile da risolvere: $T(n)$ è la somma di circa $n/2$ termini $\log n,\log(n-2),\dots$, ciascuno al più $\log n$, e i primi $n/4$ di essi sono almeno $\log(n/2)$; quindi $T(n)=\Theta(n\log n)$.

    3. Albero di ricorsione con $n=2^L$: il livello $j$ ha $4^j$ nodi di dimensione $n/2^j$, e $\log(n/2^j)=L-j$. Il costo del livello $j$ è

        $$
        4^j\,\frac{(n/2^j)^2}{L-j}=\frac{n^2}{L-j}.
        $$

        Le foglie sono $4^L=n^2$, ciascuna con costo $T(1)=1$. Quindi

        $$
        T(n)=n^2+\sum_{j=0}^{L-1}\frac{n^2}{L-j}=n^2+n^2\sum_{i=1}^{L}\frac1i=n^2\,(1+H_L),
        $$

        dove $H_L$ è l'$L$-esimo numero armonico. Confrontando la somma con l'integrale di $1/x$,

        $$
        \ln(L+1)=\int_1^{L+1}\frac{dx}{x}\le H_L\le 1+\int_1^{L}\frac{dx}{x}=1+\ln L ,
        $$

        quindi $H_L=\Theta(\log L)=\Theta(\log\log n)$, e

        $$
        T(n)=\Theta(n^2\log\log n).
        $$

        Per esempio, $T(16)=256\,(1+H_4)=256\left(1+\frac{25}{12}\right)=\frac{2368}{3}\approx 789.33$, che concorda con la ricorrenza: $T(2)=8$, $T(4)=40$, $T(8)=\frac{544}{3}$, $T(16)=4\cdot\frac{544}{3}+\frac{256}{4}=\frac{2368}{3}$.

<a id="esercizio-16-3"></a>

!!! esercizio "Esercizio 16.3: Il Master theorem (E3)"

    Consideriamo le seguenti famiglie di ricorrenze, dipendenti da un parametro reale ($\log$ denota $\log_2$):

    - **(A)** $T(n)=a\,T(n/4)+n^2$, con $a\ge1$;

    - **(B)** $T(n)=8\,T(n/2)+n^d$, con $d\ge0$;

    - **(C)** $T(n)=4\,T(n/b)+n\log n$, con $b>1$.

    **Domande**

    1. Per la famiglia (A), determinare per quali valori di $a$ si applica ciascun caso del Master theorem, e dare il corrispondente ordine di grandezza di $T(n)$. Verificare la condizione di regolarità quando necessario.

    2. Stessa domanda per la famiglia (B), in funzione di $d$.

    3. Stessa domanda per la famiglia (C), in funzione di $b$.

    4. Nella famiglia (A), qual è il più grande intero $a$ tale che $T(n)=O(n^2)$? Che cosa succede per $a=17$?

??? soluzione "Soluzione"

    1. Famiglia (A): $b=4$, $f(n)=n^2$, $n^{\log_b a}=n^{\log_4 a}$. Confrontiamo gli esponenti $\log_4 a$ e $2$; si noti che $\log_4 a=2\iff a=16$.

        - $a>16$: $\log_4 a>2$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>, poiché $f(n)=n^2=O(n^{\log_4 a-\epsilon})$ con $\epsilon=\log_4 a-2>0$. Quindi $T(n)=\Theta(n^{\log_4 a})$.

        - $a=16$: $n^{\log_4 16}=n^2$ $\longrightarrow$ <span style="color:#e03131">caso 2</span> con $k=0$. Quindi $T(n)=\Theta(n^2\log n)$.

        - $1\le a<16$: $\log_4 a<2$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>, con $f(n)=\Omega(n^{\log_4 a+\epsilon})$, $\epsilon=2-\log_4 a>0$. Condizione di regolarità:

            $$
            a\,f\left(\frac n4\right)=a\,\frac{n^2}{16}=\frac{a}{16}\,n^2=c\,f(n)\qquad\text{con } c=\frac{a}{16}<1 .
            $$

            Quindi $T(n)=\Theta(n^2)$.

    2. Famiglia (B): $a=8$, $b=2$, $n^{\log_2 8}=n^3$, $f(n)=n^d$.

        - $0\le d<3$: <span style="color:#e03131">caso 1</span> con $\epsilon=3-d>0$. Quindi $T(n)=\Theta(n^3)$.

        - $d=3$: <span style="color:#e03131">caso 2</span> con $k=0$. Quindi $T(n)=\Theta(n^3\log n)$.

        - $d>3$: <span style="color:#e03131">caso 3</span> con $\epsilon=d-3>0$. Condizione di regolarità:

            $$
            8\left(\frac n2\right)^d=\frac{8}{2^d}\,n^d=2^{3-d}\,n^d=c\,f(n)\qquad\text{con } c=2^{3-d}<1 .
            $$

            Quindi $T(n)=\Theta(n^d)$.

    3. Famiglia (C): $a=4$, $f(n)=n\log n$, $n^{\log_b a}=n^{\log_b 4}$. Confrontiamo $\log_b 4$ con l'esponente $1$ di $n$ in $f(n)$; si noti che $\log_b 4=1\iff b=4$, e $\log_b 4>1\iff b<4$.

        - $1<b<4$: $p=\log_b 4>1$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>. Scegliamo $\epsilon=\frac{p-1}{2}>0$; allora $p-\epsilon=1+\frac{p-1}{2}>1$ e

            $$
            \lim_{n\to\infty}\frac{n\log n}{n^{p-\epsilon}}=\lim_{n\to\infty}\frac{\log n}{n^{(p-1)/2}}=0^+,
            $$

            quindi $f(n)=O(n^{p-\epsilon})$. Quindi $T(n)=\Theta(n^{\log_b 4})$.

        - $b=4$: $n^{\log_4 4}=n$ e $f(n)=n\log n=\Theta(n\log^k n)$ con $k=1$ $\longrightarrow$ <span style="color:#e03131">caso 2</span>. Quindi $T(n)=\Theta(n\log^2 n)$.

        - $b>4$: $p=\log_b 4<1$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>: poiché $n\log n\ge n$ per $n\ge2$, $f(n)=\Omega(n^{p+\epsilon})$ con $\epsilon=1-p>0$. Condizione di regolarità, per $n\ge b$:

            $$
            4\,\frac nb\log\frac nb\le\frac4b\,n\log n=c\,f(n)\qquad\text{con } c=\frac4b<1 .
            $$

            Quindi $T(n)=\Theta(n\log n)$.

    4. Dalla domanda 1, $T(n)=\Theta(n^2)$ per $1\le a<16$, mentre $T(n)=\Theta(n^2\log n)$ per $a=16$, che non è $O(n^2)$ perché $\lim_{n\to\infty}\frac{n^2\log n}{n^2}=+\infty$. Quindi il più grande intero è $a=15$.

        Per $a=17$ siamo nel caso 1: $T(n)=\Theta(n^{\log_4 17})\approx\Theta(n^{2.044})$. Una piccola variazione del numero di sottoproblemi cambia l'esponente del tempo di esecuzione.

<a id="esercizio-16-4"></a>

!!! esercizio "Esercizio 16.4: Il Master theorem (E4)"

    Consideriamo i seguenti due algoritmi ricorsivi. In <code>PairSum</code> la lunghezza $n=r-l+1$ del sotto-array è una potenza di $2$; in <code>TernaryMax</code> è una potenza di $3$. La prima chiamata è sull'intero array $a[1..n]$, cioè con $l=1$ e $r=n$.

    !!! algoritmo "Algoritmo: PairSum"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#92;)</span> di numeri interi e due indici <span class="arithmatex">&#92;(l&#92;le r&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero <span class="arithmatex">&#92;(s&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> PairSum(a, l, r)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(l = r&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(0&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m := &#92;lfloor (l+r)/2&#92;rfloor&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s :=&#92;)</span> PairSum(<span class="arithmatex">&#92;(a, l, m&#92;)</span>) <span class="arithmatex">&#92;(+&#92;)</span> PairSum(<span class="arithmatex">&#92;(a, m+1, r&#92;)</span>)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := l&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le m&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-g"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := m+1&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;le r&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-i"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s &#92;leftarrow s + a&#91;i&#93;&#92;cdot a&#91;j&#93;&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-j"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-k"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfour-l"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    !!! algoritmo "Algoritmo: TernaryMax"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#92;)</span> di numeri interi e due indici <span class="arithmatex">&#92;(l&#92;le r&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> TernaryMax(a, l, r)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(l = r&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(a&#91;l&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-c"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(t := (r-l+1)/3&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-d"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(x :=&#92;)</span> TernaryMax(<span class="arithmatex">&#92;(a, l, l+t-1&#92;)</span>)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(y :=&#92;)</span> TernaryMax(<span class="arithmatex">&#92;(a, l+t, l+2t-1&#92;)</span>)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(z :=&#92;)</span> TernaryMax(<span class="arithmatex">&#92;(a, l+2t, r&#92;)</span>)</span></span></div>
        <div class="pc-riga" id="riga-es-16-master-theorem-exfourt-g"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(&#92;max&#92;{x,y,z&#92;}&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa calcolano i due algoritmi?

    2. Scrivere la ricorrenza per il numero di passi $S(n)$ eseguiti da <code>PairSum</code>, contando le esecuzioni di ciascuna riga, e risolverla con il Master theorem. Determinare il tempo di esecuzione nel caso peggiore $T(|I|)$.

    3. Stessa domanda per <code>TernaryMax</code>. Poi calcolare $S(n)$ esattamente con l'albero di ricorsione e verificarlo per $n=9$.

??? soluzione "Soluzione"

    1. <code>PairSum</code>$(a,1,n)$ restituisce la somma dei prodotti di tutte le coppie di elementi distinti,

        $$
        \sum_{1\le i<j\le n}a[i]\,a[j]:
        $$

        ogni coppia è o dentro la metà sinistra, o dentro la metà destra (chiamate ricorsive), oppure ha $i$ nella metà sinistra e $j$ nella metà destra (i due cicli annidati).<br> <code>TernaryMax</code>$(a,1,n)$ restituisce il valore massimo dell'array: divide l'array in tre parti di uguale lunghezza, calcola ricorsivamente il massimo di ciascuna parte e restituisce il più grande dei tre.

    2. Sia $n=r-l+1\ge2$ e $h=n/2$ (la lunghezza di ciascuna metà). Il numero di volte in cui ciascuna riga è eseguita, <strong>esclusi i passi eseguiti all'interno delle chiamate ricorsive</strong>, è:

        - La <span style="color:#e03131">riga</span> [2](#riga-es-16-master-theorem-exfour-a) è eseguita $1$ volta

        - La <span style="color:#e03131">riga</span> [3](#riga-es-16-master-theorem-exfour-b) è eseguita $0$ volte

        - La <span style="color:#e03131">riga</span> [5](#riga-es-16-master-theorem-exfour-c) è eseguita $1$ volta

        - La <span style="color:#e03131">riga</span> [6](#riga-es-16-master-theorem-exfour-d) è eseguita $1$ volta (più le due chiamate ricorsive su $h$ elementi)

        - La <span style="color:#e03131">riga</span> [7](#riga-es-16-master-theorem-exfour-e) è eseguita $1$ volta

        - La <span style="color:#e03131">riga</span> [8](#riga-es-16-master-theorem-exfour-f) è eseguita $h+1$ volte

        - La <span style="color:#e03131">riga</span> [9](#riga-es-16-master-theorem-exfour-g) è eseguita $h$ volte

        - La <span style="color:#e03131">riga</span> [10](#riga-es-16-master-theorem-exfour-h) è eseguita $h(h+1)$ volte

        - La <span style="color:#e03131">riga</span> [11](#riga-es-16-master-theorem-exfour-i) è eseguita $h^2$ volte

        - La <span style="color:#e03131">riga</span> [12](#riga-es-16-master-theorem-exfour-j) è eseguita $h^2$ volte

        - La <span style="color:#e03131">riga</span> [14](#riga-es-16-master-theorem-exfour-k) è eseguita $h$ volte

        - La <span style="color:#e03131">riga</span> [16](#riga-es-16-master-theorem-exfour-l) è eseguita $1$ volta

        In totale $1+1+1+1+(h+1)+h+h(h+1)+h^2+h^2+h+1=3h^2+4h+6$. Con $h=n/2$, e poiché per $n=1$ sono eseguite solo le righe [2](#riga-es-16-master-theorem-exfour-a) e [3](#riga-es-16-master-theorem-exfour-b),

        $$
        S(n)=\begin{cases}
        2 & \text{se } n=1,\\[1mm]
        2\,S(n/2)+\dfrac34 n^2+2n+6 & \text{se } n\ge 2.
        \end{cases}
        $$

        (Per esempio $S(2)=2\cdot2+\frac34\cdot4+4+6=17$.) Applichiamo il Master theorem:

        1. $a=2$, $b=2$, $f(n)=\frac34n^2+2n+6$.

        2. $n^{\log_b a}=n^{\log_2 2}=n$.

        3. $f(n)=\Theta(n^2)$ è polinomialmente più grande di $n$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>.

        4. $f(n)\ge\frac34 n^2$, quindi $f(n)=\Omega(n^{1+\epsilon})$ con $\epsilon=1$. Condizione di regolarità con $c=\frac34$:

            $$
            2\,f\left(\frac n2\right)=\frac38n^2+2n+12\le\frac34\left(\frac34n^2+2n+6\right)=\frac{9}{16}n^2+\frac32n+\frac92
            $$

            $$
            \Longleftrightarrow\quad 0\le\frac{3}{16}n^2-\frac12 n-\frac{15}{2}
            \quad\Longleftrightarrow\quad 3n^2-8n-120\ge0,
            $$

            che vale per ogni $n\ge8$ (la radice positiva è $\frac{8+\sqrt{1504}}{6}\approx7.8$).

        5. $S(n)=\Theta(f(n))=\Theta(n^2)$.

        Nell'ipotesi che ogni elemento usi un numero costante di bit, $|I|=\Theta(n)$, quindi $n=\Theta(|I|)$.

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>PairSum</code>, in funzione della dimensione dell'input $|I|$, è

            $$
            T(|I|)=\Theta(|I|^2).
            $$

    3. Per <code>TernaryMax</code> con $n\ge 3$ (potenza di 3), escluse le chiamate ricorsive, le righe [2](#riga-es-16-master-theorem-exfourt-a), [5](#riga-es-16-master-theorem-exfourt-c), [6](#riga-es-16-master-theorem-exfourt-d), [7](#riga-es-16-master-theorem-exfourt-e), [8](#riga-es-16-master-theorem-exfourt-f), [9](#riga-es-16-master-theorem-exfourt-g) sono eseguite una volta ciascuna e la riga [3](#riga-es-16-master-theorem-exfourt-b) non è eseguita: $6$ passi. Per $n=1$, sono eseguite le righe [2](#riga-es-16-master-theorem-exfourt-a) e [3](#riga-es-16-master-theorem-exfourt-b): $2$ passi. Ciascuna delle tre chiamate è su $t=n/3$ elementi. Quindi

        $$
        S(n)=\begin{cases}
        2 & \text{se } n=1,\\
        3\,S(n/3)+6 & \text{se } n\ge 3.
        \end{cases}
        $$

        1. $a=3$, $b=3$, $f(n)=6$.

        2. $n^{\log_b a}=n^{\log_3 3}=n$.

        3. $n$ è polinomialmente più grande di $f(n)=6$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>.

        4. $f(n)=6=O(n^{1-\epsilon})$ con $\epsilon=1$.

        5. $S(n)=\Theta(n)$.

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>TernaryMax</code>, in funzione della dimensione dell'input $|I|$, è

            $$
            T(|I|)=\Theta(|I|).
            $$

        Valore esatto con l'albero di ricorsione, $n=3^L$: il livello $j$ ha $3^j$ nodi interni di costo $6$, e ci sono $3^L=n$ foglie di costo $2$:

        $$
        S(n)=2n+\sum_{j=0}^{L-1}6\cdot3^j=2n+6\,\frac{3^L-1}{3-1}=2n+3(n-1)=5n-3 .
        $$

        Verifica per $n=9$: $S(1)=2$, $S(3)=3\cdot2+6=12$, $S(9)=3\cdot12+6=42=5\cdot9-3$. $\checkmark$

<a id="esercizio-16-5"></a>

!!! esercizio "Esercizio 16.5: Il Master theorem (E5)"

    Uno studente risolve tre ricorrenze come segue ($\log$ denota $\log_2$, $T(1)=1$):

    - **(a)** $T(n)=2\,T(n/2)+n\log n$. “$f(n)=n\log n$ è più grande di $n^{\log_2 2}=n$, quindi per il caso 3 $T(n)=\Theta(n\log n)$.”

    - **(b)** $T(n)=2\,T(n/2)+n/\log n$. “$f(n)=n/\log n$ è più piccola di $n$, quindi per il caso 1 $T(n)=\Theta(n)$.”

    - **(c)** $T(n)=2\,T(n/2)+n/\log^2 n$. “$f(n)=n/\log^2 n$ è più piccola di $n$, quindi per il caso 1 $T(n)=\Theta(n)$.”

    **Domande**

    1. Trovare l'errore in ciascuna delle tre soluzioni.

    2. Risolvere correttamente (a) con il Master theorem.

    3. Risolvere (b) e (c) per $n=2^L$ con l'albero di ricorsione. La risposta finale dello studente è corretta per (b)? E per (c)?

    4. Verificare le formule per (b) e (c) calcolando $T(16)$ direttamente dalle ricorrenze.

??? soluzione "Soluzione"

    1. Lo studente confronta $f(n)$ con $n^{\log_b a}=n$ ma dimentica che il confronto deve essere <strong>polinomiale</strong>.

        - **(a)** Il caso 3 richiede $f(n)=\Omega(n^{1+\epsilon})$ per qualche $\epsilon>0$. Ma per ogni $\epsilon>0$

            $$
            \lim_{n\to\infty}\frac{n\log n}{n^{1+\epsilon}}=\lim_{n\to\infty}\frac{\log n}{n^{\epsilon}}=0^+,
            $$

            quindi $f(n)\neq\Omega(n^{1+\epsilon})$: il caso 3 non si applica.

        - **(b)** e (c) Il caso 1 richiede $f(n)=O(n^{1-\epsilon})$ per qualche $\epsilon>0$. Ma per ogni $\epsilon>0$

            $$
            \lim_{n\to\infty}\frac{n/\log n}{n^{1-\epsilon}}=\lim_{n\to\infty}\frac{n^{\epsilon}}{\log n}=+\infty,
            \qquad
            \lim_{n\to\infty}\frac{n/\log^2 n}{n^{1-\epsilon}}=\lim_{n\to\infty}\frac{n^{\epsilon}}{\log^2 n}=+\infty,
            $$

            quindi il caso 1 non si applica. Il caso 2 richiederebbe $k=-1$ e $k=-2$, rispettivamente, ma $k\ge0$. Entrambe le ricorrenze cadono nel <strong>vuoto</strong> tra il caso 1 e il caso 2: il Master theorem non può essere usato.

    2. (a) $a=2$, $b=2$, $f(n)=n\log n$, $n^{\log_2 2}=n$. $f(n)=\Theta(n\log^k n)$ con $k=1$ $\longrightarrow$ <span style="color:#e03131">caso 2</span>:

        $$
        T(n)=\Theta(n\log^2 n).
        $$

    3. Per $n=2^L$: il livello $j$ ha $2^j$ nodi di dimensione $n/2^j$, con $\log(n/2^j)=L-j$; ci sono $2^L=n$ foglie di costo $T(1)=1$.

        - **(b)** Il livello $j$ costa $2^j\,\dfrac{n/2^j}{L-j}=\dfrac{n}{L-j}$, quindi

            $$
            T(n)=n+\sum_{j=0}^{L-1}\frac{n}{L-j}=n+n\sum_{i=1}^{L}\frac1i=n\,(1+H_L).
            $$

            Poiché $\ln(L+1)\le H_L\le1+\ln L$, $H_L=\Theta(\log L)$ e

            $$
            T(n)=\Theta(n\log\log n).
            $$

            La risposta dello studente $\Theta(n)$ è <strong>sbagliata</strong>: $\lim_{n\to\infty}\frac{n\log\log n}{n}=+\infty$.

        - **(c)** Il livello $j$ costa $2^j\,\dfrac{n/2^j}{(L-j)^2}=\dfrac{n}{(L-j)^2}$, quindi

            $$
            T(n)=n+n\sum_{i=1}^{L}\frac1{i^2}.
            $$

            La serie $\sum_{i\ge1}\frac1{i^2}$ converge (a $\frac{\pi^2}{6}\approx1.645$), quindi

            $$
            n\le T(n)\le n\left(1+\frac{\pi^2}{6}\right),\qquad\text{cioè}\qquad T(n)=\Theta(n).
            $$

            La <strong>risposta</strong> dello studente <strong>è corretta, ma il ragionamento è sbagliato</strong>: il Master theorem non si applica, e il risultato deve essere dimostrato con l'albero di ricorsione. Qui i costi dei livelli decrescono così rapidamente verso le foglie che dominano le foglie (che sono $n$).

    4. Per $n=16$ ($L=4$):

        - **(b)** $T(2)=2+\frac21=4$, $T(4)=8+\frac42=10$, $T(8)=20+\frac83=\frac{68}{3}$, $T(16)=\frac{136}{3}+\frac{16}{4}=\frac{148}{3}$.<br> Formula: $16\,(1+H_4)=16\left(1+\frac{25}{12}\right)=\frac{148}{3}\approx49.33$. $\checkmark$

        - **(c)** $T(2)=2+\frac21=4$, $T(4)=8+\frac44=9$, $T(8)=18+\frac89=\frac{170}{9}$, $T(16)=\frac{340}{9}+\frac{16}{16}=\frac{349}{9}$.<br> Formula: $16\left(1+1+\frac14+\frac19+\frac1{16}\right)=16\left(2+\frac{61}{144}\right)=\frac{349}{9}\approx38.78$. $\checkmark$

<a id="esercizio-16-6"></a>

!!! esercizio "Esercizio 16.6: Il Master theorem (E6)"

    Consideriamo le ricorrenze, definite per $n$ potenza di $2$:

    $$
    T_1(n)=3\,T_1(n/2)+n^2,\qquad T_2(n)=4\,T_2(n/2)+n,\qquad T_1(1)=T_2(1)=1 .
    $$

    **Domande**

    1. Per $n=8$, disegnare la tabella dell'albero di ricorsione di $T_1$ (livello, numero di nodi, dimensione, costo del livello) e verificare il lemma, confrontando con il valore di $T_1(8)$ calcolato direttamente dalla ricorrenza.

    2. Stessa domanda per $T_2$ e $n=8$.

    3. Usando il lemma, trovare una formula chiusa per $T_1(n)$ e $T_2(n)$, $n=2^L$.

    4. Risolvere entrambe le ricorrenze con il Master theorem e controllare il risultato con le formule chiuse.

    5. Per $T_1$, controllare numericamente, per $n=8$, la limitazione $f(n)\le g(n)\le\frac{f(n)}{1-c}$ del caso 3 del lemma sulla somma $g(n)$.

??? soluzione "Soluzione"

    1. $T_1$: $a=3$, $b=2$, $f(n)=n^2$, $\log_2 8=3$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>livello <span class="arithmatex">&#92;(j&#92;)</span></th>
        <th>nodi <span class="arithmatex">&#92;(3^j&#92;)</span></th>
        <th>dimensione <span class="arithmatex">&#92;(8/2^j&#92;)</span></th>
        <th>costo per nodo</th>
        <th>costo del livello</th>
        </tr>
        <tr>
        <td>0</td>
        <td>1</td>
        <td>8</td>
        <td>64</td>
        <td>64</td>
        </tr>
        <tr>
        <td>1</td>
        <td>3</td>
        <td>4</td>
        <td>16</td>
        <td>48</td>
        </tr>
        <tr>
        <td>2</td>
        <td>9</td>
        <td>2</td>
        <td>4</td>
        <td>36</td>
        </tr>
        <tr>
        <td>3 (foglie)</td>
        <td>27</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(T&#95;1(1)=1&#92;)</span></td>
        <td>27</td>
        </tr>
        <tr>
        <td></td>
        <td></td>
        <td></td>
        <td>totale</td>
        <td>175</td>
        </tr>
        </table></div>

        Il numero di foglie è $3^{3}=27=8^{\log_2 3}$ (infatti $8^{\log_2 3}=(2^3)^{\log_2 3}=(2^{\log_2 3})^3=3^3$). Direttamente:

        $$
        T_1(2)=3+4=7,\qquad T_1(4)=21+16=37,\qquad T_1(8)=111+64=175. \quad\checkmark
        $$

    2. $T_2$: $a=4$, $b=2$, $f(n)=n$.

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>livello <span class="arithmatex">&#92;(j&#92;)</span></th>
        <th>nodi <span class="arithmatex">&#92;(4^j&#92;)</span></th>
        <th>dimensione <span class="arithmatex">&#92;(8/2^j&#92;)</span></th>
        <th>costo per nodo</th>
        <th>costo del livello</th>
        </tr>
        <tr>
        <td>0</td>
        <td>1</td>
        <td>8</td>
        <td>8</td>
        <td>8</td>
        </tr>
        <tr>
        <td>1</td>
        <td>4</td>
        <td>4</td>
        <td>4</td>
        <td>16</td>
        </tr>
        <tr>
        <td>2</td>
        <td>16</td>
        <td>2</td>
        <td>2</td>
        <td>32</td>
        </tr>
        <tr>
        <td>3 (foglie)</td>
        <td><span class="arithmatex">&#92;(64=8^{&#92;log&#95;2 4}&#92;)</span></td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(T&#95;2(1)=1&#92;)</span></td>
        <td>64</td>
        </tr>
        <tr>
        <td></td>
        <td></td>
        <td></td>
        <td>totale</td>
        <td>120</td>
        </tr>
        </table></div>

        Direttamente: $T_2(2)=4+2=6$, $T_2(4)=24+4=28$, $T_2(8)=112+8=120$. $\checkmark$

    3. Con $n=2^L$:

        $$
        T_1(n)=n^{\log_2 3}+\sum_{j=0}^{L-1}3^j\frac{n^2}{4^j}=n^{\log_2 3}+n^2\,\frac{1-(3/4)^L}{1-3/4}=n^{\log_2 3}+4n^2-4n^2\,\frac{3^L}{4^L}.
        $$

        Poiché $4^L=n^2$ e $3^L=n^{\log_2 3}$,

        $$
        T_1(n)=4n^2-3\,n^{\log_2 3}.
        $$

        (Verifica: $4\cdot64-3\cdot27=256-81=175$.) Analogamente

        $$
        T_2(n)=n^{2}+\sum_{j=0}^{L-1}4^j\frac{n}{2^j}=n^2+n\,(2^L-1)=2n^2-n .
        $$

        (Verifica: $128-8=120$.)

    4. - $T_1$: $n^{\log_2 3}\approx n^{1.585}$ è polinomialmente più piccolo di $f(n)=n^2$ $\longrightarrow$ <span style="color:#e03131">caso 3</span>, con $\epsilon=2-\log_2 3\approx0.415$. Regolarità: $3\left(\frac n2\right)^2=\frac34n^2$, quindi $c=\frac34<1$. Quindi $T_1(n)=\Theta(n^2)$. Formula chiusa:

            $$
            \lim_{n\to\infty}\frac{4n^2-3n^{\log_2 3}}{n^2}=\lim_{n\to\infty}\left(4-\frac{3}{n^{2-\log_2 3}}\right)=4\in\R_{>0}. \quad\checkmark
            $$

        - $T_2$: $n^{\log_2 4}=n^2$ è polinomialmente più grande di $f(n)=n$ $\longrightarrow$ <span style="color:#e03131">caso 1</span>, con $\epsilon=1$. Quindi $T_2(n)=\Theta(n^2)$. Formula chiusa: $\lim_{n\to\infty}\frac{2n^2-n}{n^2}=2\in\R_{>0}$. $\checkmark$

        Entrambe le ricorrenze sono $\Theta(n^2)$, ma per ragioni diverse: in $T_1$ il costo è dominato dalla radice (i costi dei livelli $n^2(3/4)^j$ decrescono), in $T_2$ dalle foglie (i costi dei livelli $n\,2^j$ crescono).

    5. Per $T_1$ e $n=8$: $g(8)=64+48+36=148$, $f(8)=64$, $c=\frac34$:

        $$
        64\le 148\le\frac{64}{1-3/4}=256. \quad\checkmark
        $$
