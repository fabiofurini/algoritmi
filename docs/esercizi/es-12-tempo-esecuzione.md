---
title: "Esercizi · Tempo di esecuzione"
---

# Esercizi · Tempo di esecuzione

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 12** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 12: Tempo di esecuzione](../analisi/12-tempo-esecuzione.md) · [:material-file-pdf-box: Eserciziario, volume 4 (PDF)](../pdf/esercizi-4-analisi.pdf)

</div>

Negli esercizi di questo capitolo i passi si contano con le convenzioni del capitolo «Tempo di esecuzione»: ogni esecuzione di una riga numerata dello pseudocodice (comprese le righe <code>return</code>) è un passo, la condizione di un ciclo <code>while</code> il cui corpo viene eseguito $k$ volte viene valutata $k+1$ volte, e le righe di un ramo che non viene percorso non vengono eseguite. Dopo aver ottenuto il numero di passi $S(n)$, il tempo di esecuzione si esprime in funzione della dimensione dell'input $|I|$ con una delle due regole seguenti.

!!! nota ""

    <strong>Regola (A): l'input è un numero naturale $n$.</strong> Allora $|I|=\Theta(\log_2 n)$: esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    c_1\log_2 n \le |I| \le c_2\log_2 n
    \qquad\Longleftrightarrow\qquad
    2^{\frac{1}{c_2}|I|}\le n \le 2^{\frac{1}{c_1}|I|},
    $$

    poiché $x\mapsto 2^x$ è strettamente crescente e $2^{\log_2 n}=n$. Se $S(n)=\Theta(n)$, esistono costanti $a_1,a_2>0$ tali che $a_1 n \le S(n) \le a_2 n$ per ogni $n$ sufficientemente grande, e quindi

    $$
    a_1\, 2^{\frac{1}{c_2}|I|}
    \le
    S(n)
    \le
    a_2\, 2^{\frac{1}{c_1}|I|},
    \qquad\text{cioè}\qquad
    T(|I|)=2^{\Theta(|I|)}.
    $$

!!! nota ""

    <strong>Regola (B): l'input è un array $a[1..n]$ i cui elementi usano un numero costante fisso di bit.</strong> Allora $|I|=\Theta(n)$: esistono costanti $c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

    $$
    c_1 n \le |I| \le c_2 n
    \qquad\Longleftrightarrow\qquad
    \frac{1}{c_2}|I| \le n \le \frac{1}{c_1}|I|.
    $$

    Se $S(n)=\Theta(n^k)$ per una costante $k\ge 1$, esistono costanti $a_1,a_2>0$ tali che $a_1 n^k \le S(n) \le a_2 n^k$ per ogni $n$ sufficientemente grande, e quindi

    $$
    \frac{a_1}{c_2^{k}}\,|I|^k
    \le
    S(n)
    \le
    \frac{a_2}{c_1^{k}}\,|I|^k,
    \qquad\text{cioè}\qquad
    T(|I|)=\Theta(|I|^k).
    $$

<a id="esercizio-12-1"></a>

!!! esercizio "Esercizio 12.1: Tempo di esecuzione (E1)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 1"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(m&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm1(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow m+2&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(m&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo somma $2$ a $m$ esattamente $n$ volte, partendo da $m=0$: determina il doppio di $n$, cioè $2n$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm1</code>, dove $n$ è il numero naturale dato in input. Per ogni valore di $n$ c'è un solo input, quindi questo è anche il caso peggiore. Il corpo del ciclo viene eseguito per $i=1,2,\dots,n$, cioè $n$ volte, e la condizione della riga [4](#riga-es-12-tempo-esecuzione-l-c) viene valutata $n+1$ volte:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+1+(n+1)+n+n+1=3n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+4=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm1</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-2"></a>

!!! esercizio "Esercizio 12.2: Tempo di esecuzione (E2)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 2"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(m&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm2(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;bmod 2 = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow m+2&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>else</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m := n&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-h"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(m&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo restituisce il doppio $2n$ di $n$ se $n$ è pari. Se $n$ è dispari, restituisce $n$ invariato.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm2</code>, dove $n$ è il numero naturale dato in input. L'esecuzione delle righe [3](#riga-es-12-tempo-esecuzione-l-b)–[7](#riga-es-12-tempo-esecuzione-l-f) dipende dallo specifico valore di input $n$: prima di eseguire l'algoritmo non sappiamo se $n$ sia pari o dispari. Definiamo una funzione

        $$
        t:\N\to\{0,1\},
        $$

        dove $t(n)=1$ se $n \bmod 2 = 0$, e $t(n)=0$ altrimenti. In altre parole, $t(n)$ è un oracolo che ci dice se il numero in input $n$ è pari. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(t(n)&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(t(n)&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(t(n)&#92;,(n+1)&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(t(n)&#92;,n&#92;)</span></td>
        </tr>
        <tr>
        <td>[7](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(t(n)&#92;,n&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(1-t(n)&#92;)</span></td>
        </tr>
        <tr>
        <td>[12](#riga-es-12-tempo-esecuzione-l-h)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        1+t(n)+t(n)+t(n)(n+1)+t(n)\,n+t(n)\,n+\big(1-t(n)\big)+1=3n\,t(n)+2\,t(n)+3.
        $$

        Il caso peggiore si ha quando $n$ è pari: allora $t(n)=1$ e l'algoritmo esegue $3n+5$ passi, mentre per $n$ dispari ne esegue solo $3$. Ogni dimensione dell'input di almeno due bit è la dimensione di qualche numero pari, quindi nel caso peggiore

        $$
        S(n)=3n+5=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+5=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm2</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-3"></a>

!!! esercizio "Esercizio 12.3: Tempo di esecuzione (E3)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 3"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(s&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm3(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s &#92;leftarrow s+i&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina la somma dei primi $n$ numeri naturali positivi:

        $$
        1+2+\cdots+n=\frac{n(n+1)}{2}.
        $$

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm3</code>, dove $n$ è il numero naturale dato in input (per ogni valore di $n$ c'è un solo input). Il corpo del ciclo viene eseguito $n$ volte e la sua condizione $n+1$ volte:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+1+(n+1)+n+n+1=3n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+4=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm3</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-4"></a>

!!! esercizio "Esercizio 12.4: Tempo di esecuzione (E4)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 4"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(p&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm4(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p := 1&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p &#92;leftarrow p &#92;cdot i&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(p&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina il prodotto

        $$
        1\cdot 2\cdot \ldots \cdot n=n!
        $$

        (con $0!=1$, restituito per $n=0$).

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm4</code>, dove $n$ è il numero naturale dato in input (per ogni valore di $n$ c'è un solo input). Il corpo del ciclo viene eseguito $n$ volte e la sua condizione $n+1$ volte:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+1+(n+1)+n+n+1=3n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+4=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm4</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-5"></a>

!!! esercizio "Esercizio 12.5: Tempo di esecuzione (E5)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 5"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(c&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm5(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(i &#92;bmod 2 = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c &#92;leftarrow c+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina quanti numeri naturali tra $1$ e $n$ sono pari, cioè $\lfloor n/2\rfloor$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm5</code>, dove $n$ è il numero naturale dato in input. La riga [6](#riga-es-12-tempo-esecuzione-l-e) viene eseguita solo quando $i$ è pari, cioè $\lfloor n/2\rfloor$ volte. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(&#92;lfloor n/2&#92;rfloor&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+1+(n+1)+n+\lfloor n/2\rfloor+n+1=3n+\lfloor n/2\rfloor+4.
        $$

        Poiché $\frac{n-1}{2}\le\lfloor n/2\rfloor\le \frac{n}{2}$, si ha $\frac{7}{2}n+\frac{7}{2}\le S(n)\le \frac{7}{2}n+4$, quindi $S(n)=\Theta(n)$.

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+\lfloor n/2\rfloor+4=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm5</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-6"></a>

!!! esercizio "Esercizio 12.6: Tempo di esecuzione (E6)"

    Si consideri il seguente algoritmo, il cui input è un numero naturale $n$.

    !!! algoritmo "Algoritmo: Algoritmo 6"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(q&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm6(n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(q := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(q &#92;leftarrow q+n&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(q&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo somma $n$ a $q$ esattamente $n$ volte, partendo da $q=0$: determina $n\cdot n=n^2$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm6</code>, dove $n$ è il numero naturale dato in input (per ogni valore di $n$ c'è un solo input). Il corpo del ciclo viene eseguito $n$ volte e la sua condizione $n+1$ volte:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+1+(n+1)+n+n+1=3n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. L'input è il numero naturale $n$, quindi $|I|=\Theta(\log_2 n)$, e $S(n)=3n+4=\Theta(n)$. Per la regola (A) dell'introduzione agli esercizi esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        a_1\, 2^{\frac{1}{c_2}|I|}
        \le
        S(n)
        \le
        a_2\, 2^{\frac{1}{c_1}|I|},
        \qquad\text{quindi}\qquad
        T(|I|)=2^{\Theta(|I|)}.
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm6</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=2^{\Theta(|I|)}$: è <strong>esponenziale</strong> in $|I|$, anche se il numero di passi è lineare nel valore $n$.

<a id="esercizio-12-7"></a>

!!! esercizio "Esercizio 12.7: Tempo di esecuzione (E7)"

    Si consideri il seguente algoritmo, il cui input è un array $a[1..n]$ di $n$ numeri interi.

    !!! algoritmo "Algoritmo: Algoritmo 7"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero <span class="arithmatex">&#92;(s&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm7(a, n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(s &#92;leftarrow s+a&#91;i&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina la somma dei valori positivi nell'array $a[1..n]$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm7</code> nel caso peggiore, dove $n$ è la dimensione dell'array. L'esecuzione della riga [6](#riga-es-12-tempo-esecuzione-l-e) dipende dall'array in input. Definiamo una funzione

        $$
        t:\{1,2,\dots,n\}\to\{0,1\},
        $$

        dove $t(i)=1$ se $a[i]>0$, e $t(i)=0$ altrimenti. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(&#92;sum&#95;{i=1}^{n}t(i)&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        1+1+(n+1)+n+\sum_{i=1}^{n}t(i)+n+1=3n+4+\sum_{i=1}^{n}t(i).
        $$

        Il caso peggiore si ha quando tutti gli elementi sono positivi. Allora $t(i)=1$ per ogni $i \in \{1,2,\dots,n\}$, e

        $$
        S(n)=3n+4+\sum_{i=1}^{n}1=4n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. Se tutti i valori in input usano un numero costante fisso di bit, allora $|I|=\Theta(n)$, e $S(n)=\Theta(n)$. Per la regola (B) dell'introduzione agli esercizi (con $k=1$) esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        \frac{a_1}{c_2}\,|I|
        \le
        S(n)
        \le
        \frac{a_2}{c_1}\,|I|,
        \qquad\text{quindi}\qquad
        T(|I|)=\Theta(|I|).
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm7</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=\Theta(|I|)$: è <strong>lineare</strong> in $|I|$.

<a id="esercizio-12-8"></a>

!!! esercizio "Esercizio 12.8: Tempo di esecuzione (E8)"

    Si consideri il seguente algoritmo, il cui input è un array $a[1..n]$ di $n$ numeri interi.

    !!! algoritmo "Algoritmo: Algoritmo 8"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(c&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm8(a, n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &#92;bmod 2 = 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c &#92;leftarrow c+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina il numero di valori pari nell'array $a[1..n]$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm8</code> nel caso peggiore, dove $n$ è la dimensione dell'array. L'esecuzione della riga [6](#riga-es-12-tempo-esecuzione-l-e) dipende dall'array in input. Definiamo una funzione

        $$
        t:\{1,2,\dots,n\}\to\{0,1\},
        $$

        dove $t(i)=1$ se $a[i] \bmod 2 = 0$, e $t(i)=0$ altrimenti. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n+1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(&#92;sum&#95;{i=1}^{n}t(i)&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        1+1+(n+1)+n+\sum_{i=1}^{n}t(i)+n+1=3n+4+\sum_{i=1}^{n}t(i).
        $$

        Il caso peggiore si ha quando tutti gli elementi sono pari. Allora $t(i)=1$ per ogni $i \in \{1,2,\dots,n\}$, e

        $$
        S(n)=3n+4+\sum_{i=1}^{n}1=4n+4=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. Se tutti i valori in input usano un numero costante fisso di bit, allora $|I|=\Theta(n)$, e $S(n)=\Theta(n)$. Per la regola (B) dell'introduzione agli esercizi (con $k=1$) esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        \frac{a_1}{c_2}\,|I|
        \le
        S(n)
        \le
        \frac{a_2}{c_1}\,|I|,
        \qquad\text{quindi}\qquad
        T(|I|)=\Theta(|I|).
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm8</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=\Theta(|I|)$: è <strong>lineare</strong> in $|I|$.

<a id="esercizio-12-9"></a>

!!! esercizio "Esercizio 12.9: Tempo di esecuzione (E9)"

    Si consideri il seguente algoritmo, il cui input è un array $a[1..n]$ di $n \ge 1$ numeri interi.

    !!! algoritmo "Algoritmo: Algoritmo 9"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero intero <span class="arithmatex">&#92;(m&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm9(a, n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m := a&#91;1&#93;&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 2&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &lt; m&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(m&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina il valore minimo nell'array $a[1..n]$.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm9</code> nel caso peggiore, dove $n$ è la dimensione dell'array. Il corpo del ciclo viene eseguito per $i=2,3,\dots,n$, cioè $n-1$ volte. Definiamo

        $$
        t:\{2,3,\dots,n\}\to\{0,1\},
        $$

        dove $t(i)=1$ se la riga [6](#riga-es-12-tempo-esecuzione-l-e) viene eseguita all'iterazione $i$, e $t(i)=0$ altrimenti. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(&#92;sum&#95;{i=2}^{n}t(i)&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        1+1+n+(n-1)+\sum_{i=2}^{n}t(i)+(n-1)+1=3n+1+\sum_{i=2}^{n}t(i).
        $$

        Il caso peggiore si ha quando

        $$
        a[1]>a[2]>\cdots>a[n].
        $$

        Allora $t(i)=1$ per ogni $i\in\{2,3,\dots,n\}$, e

        $$
        S(n)=3n+1+\sum_{i=2}^{n}1=3n+1+(n-1)=4n=\Theta(n).
        $$

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. Se tutti i valori in input usano un numero costante fisso di bit, allora $|I|=\Theta(n)$, e $S(n)=\Theta(n)$. Per la regola (B) dell'introduzione agli esercizi (con $k=1$) esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        \frac{a_1}{c_2}\,|I|
        \le
        S(n)
        \le
        \frac{a_2}{c_1}\,|I|,
        \qquad\text{quindi}\qquad
        T(|I|)=\Theta(|I|).
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm9</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=\Theta(|I|)$: è <strong>lineare</strong> in $|I|$.

<a id="esercizio-12-10"></a>

!!! esercizio "Esercizio 12.10: Tempo di esecuzione (E10)"

    Si consideri il seguente algoritmo, il cui input è un array $a[1..n]$ di $n \ge 1$ numeri interi.

    !!! algoritmo "Algoritmo: Algoritmo 10"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span><code>true</code> or <code>false</code></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm10(a, n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &lt; n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93;=a&#91;i+1&#93;&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>true</code></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span></span></div>
        <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina se l'array contiene due valori consecutivi uguali: restituisce <code>true</code> se $a[i]=a[i+1]$ per qualche $i\in\{1,2,\dots,n-1\}$, e <code>false</code> altrimenti.

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm10</code> nel caso peggiore, dove $n$ è la dimensione dell'array. Se la prima coppia di valori consecutivi uguali viene trovata all'iterazione $k$, l'algoritmo si ferma alla riga [5](#riga-es-12-tempo-esecuzione-l-d) dopo $1+k+k+(k-1)+1=3k+1\le 3(n-1)+1$ passi. Il caso peggiore è quindi quello in cui non ci sono due valori consecutivi uguali: la riga [5](#riga-es-12-tempo-esecuzione-l-d) non viene mai eseguita e l'algoritmo controlla tutte le $n-1$ coppie consecutive. In questo caso il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td>[7](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[9](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        S(n)=1+n+(n-1)+(n-1)+1=3n=\Theta(n).
        $$

        (e $3n>3(n-1)+1$, quindi questo è effettivamente il caso peggiore).

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. Se tutti i valori in input usano un numero costante fisso di bit, allora $|I|=\Theta(n)$, e $S(n)=\Theta(n)$. Per la regola (B) dell'introduzione agli esercizi (con $k=1$) esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        \frac{a_1}{c_2}\,|I|
        \le
        S(n)
        \le
        \frac{a_2}{c_1}\,|I|,
        \qquad\text{quindi}\qquad
        T(|I|)=\Theta(|I|).
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm10</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=\Theta(|I|)$: è <strong>lineare</strong> in $|I|$.

<a id="esercizio-12-11"></a>

!!! esercizio "Esercizio 12.11: Tempo di esecuzione (E11)"

    Si consideri il seguente algoritmo, il cui input è un array $a[1..n]$ di $n \ge 1$ numeri interi.

    !!! algoritmo "Algoritmo: Algoritmo 11"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un numero naturale <span class="arithmatex">&#92;(c&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> Algorithm11(a, n)</span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-a"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c := 0&#92;)</span></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-b"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-c"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;leq n-1&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-d"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := i+1&#92;)</span></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-e"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;leq n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-f"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &lt; a&#91;j&#93;&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-g"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(c &#92;leftarrow c+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-h"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-i"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i+1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
        <div class="pc-riga" id="riga-es-12-tempo-esecuzione-l-j"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(c&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    **Domande**

    1. Che cosa determina l'algoritmo?

    2. Determinare il tempo di esecuzione nel caso peggiore dell'algoritmo.

??? soluzione "Soluzione"

    1. L'algoritmo determina il numero di coppie di posizioni $(i,j)$, con $1\leq i<j\leq n$, tali che

        $$
        a[i]<a[j].
        $$

    2. Sia $S(n)$ il numero di passi eseguiti da <code>Algorithm11</code> nel caso peggiore, dove $n$ è la dimensione dell'array. Il ciclo esterno viene eseguito per $i=1,2,\dots,n-1$ (la sua condizione viene valutata $n$ volte) e, per ogni $i$, il ciclo interno viene eseguito per $j=i+1,\dots,n$, cioè $n-i$ volte (la sua condizione viene valutata $n-i+1$ volte). Quindi il corpo del ciclo interno viene eseguito una volta per ogni coppia $(i,j)$ con $1\le i<j\le n$, e il numero di tali coppie è

        $$
        P=(n-1)+(n-2)+\cdots+1=\frac{n(n-1)}{2}.
        $$

        Definiamo $t(i,j)=1$ se la riga [8](#riga-es-12-tempo-esecuzione-l-g) viene eseguita per la coppia $(i,j)$, e $t(i,j)=0$ altrimenti. Il numero di volte in cui ciascuna riga viene eseguita è:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>riga</th>
        <th>numero di esecuzioni</th>
        </tr>
        <tr>
        <td>[2](#riga-es-12-tempo-esecuzione-l-a)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[3](#riga-es-12-tempo-esecuzione-l-b)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>[4](#riga-es-12-tempo-esecuzione-l-c)</td>
        <td><span class="arithmatex">&#92;(n&#92;)</span></td>
        </tr>
        <tr>
        <td>[5](#riga-es-12-tempo-esecuzione-l-d)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[6](#riga-es-12-tempo-esecuzione-l-e)</td>
        <td><span class="arithmatex">&#92;(&#92;sum&#95;{i=1}^{n-1}(n-i+1)=P+(n-1)&#92;)</span></td>
        </tr>
        <tr>
        <td>[7](#riga-es-12-tempo-esecuzione-l-f)</td>
        <td><span class="arithmatex">&#92;(P&#92;)</span></td>
        </tr>
        <tr>
        <td>[8](#riga-es-12-tempo-esecuzione-l-g)</td>
        <td><span class="arithmatex">&#92;(&#92;sum&#95;{1&#92;le i&lt;j&#92;le n}t(i,j)&#92;)</span></td>
        </tr>
        <tr>
        <td>[10](#riga-es-12-tempo-esecuzione-l-h)</td>
        <td><span class="arithmatex">&#92;(P&#92;)</span></td>
        </tr>
        <tr>
        <td>[12](#riga-es-12-tempo-esecuzione-l-i)</td>
        <td><span class="arithmatex">&#92;(n-1&#92;)</span></td>
        </tr>
        <tr>
        <td>[14](#riga-es-12-tempo-esecuzione-l-j)</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        </table></div>

        Quindi il numero totale di passi è

        $$
        1+1+n+(n-1)+\big(P+(n-1)\big)+P+\sum_{1\le i<j\le n}t(i,j)+P+(n-1)+1=4n+3P+\sum_{1\le i<j\le n}t(i,j).
        $$

        Il caso peggiore per la riga [8](#riga-es-12-tempo-esecuzione-l-g) si ha quando

        $$
        a[1]<a[2]<\cdots<a[n]:
        $$

        allora $t(i,j)=1$ per ogni coppia, e

        $$
        S(n)=4n+4P=4n+2n(n-1)=2n^2+2n=\Theta(n^2).
        $$

        Ad esempio, per $n=4$ e $a[1..4]=(1,2,3,4)$ l'algoritmo restituisce $c=6$ dopo $S(4)=2\cdot 16+8=40$ passi.

        Esprimiamo ora il tempo di esecuzione in funzione della dimensione dell'input. Se tutti i valori in input usano un numero costante fisso di bit, allora $|I|=\Theta(n)$, e $S(n)=\Theta(n^2)$. Per la regola (B) dell'introduzione agli esercizi (con $k=2$) esistono costanti $a_1,a_2,c_1,c_2>0$ tali che, per ogni $n$ sufficientemente grande,

        $$
        \frac{a_1}{c_2^{2}}\,|I|^2
        \le
        S(n)
        \le
        \frac{a_2}{c_1^{2}}\,|I|^2,
        \qquad\text{quindi}\qquad
        T(|I|)=\Theta(|I|^2).
        $$

        !!! chiave ""

            Il tempo di esecuzione nel caso peggiore di <code>Algorithm11</code>, in funzione della dimensione dell'input $|I|$, è $T(|I|)=\Theta(|I|^2)$: è <strong>quadratico</strong> in $|I|$.
