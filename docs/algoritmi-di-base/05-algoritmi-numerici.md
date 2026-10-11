---
title: "Algoritmi numerici"
---

# Algoritmi numerici

<div class="info-capitolo" markdown>

**Parte 1 · Algoritmi di base · Capitolo 5** · [:material-file-pdf-box: Dispensa, volume 1 (PDF)](../pdf/dispensa-1-algoritmi-di-base.pdf) · [:material-pencil: Esercizi](../esercizi/es-05-algoritmi-numerici.md)

</div>

## Introduzione

In questo capitolo studiamo quattro algoritmi classici che operano sui numeri naturali:

- il <strong>cambio di base</strong>, che scrive un numero naturale dato in base dieci come sequenza di cifre in un'altra base $b$;

- il <strong>test di primalità</strong>, che decide se un numero naturale è primo;

- il <strong>crivello di Eratostene</strong>, che trova tutti i numeri primi fino a un dato numero naturale;

- l'<strong>algoritmo di Euclide</strong>, che calcola il massimo comun divisore di due numeri naturali.

Tutti e quattro gli algoritmi si basano su una sola operazione elementare, la <strong>divisione con resto</strong>: il cambio di base legge le cifre come resti, il test di primalità e il crivello cercano resti uguali a zero, e l'algoritmo di Euclide sostituisce una coppia di numeri con una coppia più piccola per mezzo di un resto. Per ogni algoritmo presentiamo lo pseudocodice (con array indicizzati a partire da $1$), un'esecuzione passo per passo e un'implementazione in <code>C++</code> (con array indicizzati a partire da $0$), insieme alla sua esecuzione sugli stessi input.

## 5.1 Cambio di base

Nel capitolo «Rappresentazione dei numeri» abbiamo visto che una sequenza di $k$ cifre $(d_{k-1} \dots d_1 d_0)_b$ in base $b$ rappresenta il numero naturale $\sum_{i=0}^{k-1} d_i \, b^i$, e che servono $\lfloor \log_b n \rfloor + 1$ cifre per scrivere un numero naturale $n \ge 1$ in base $b$. In questa sezione risolviamo il problema inverso: dato $n$ in base dieci, calcoliamo le sue cifre in base $b$.

### 5.1.1 Divisione con resto

<a id="box-1-ch6-defDivision"></a>

!!! definizione "Definizione 5.1: divisione con resto"

    Dati un numero naturale $n$ e un numero naturale $b \ge 1$, la <strong>divisione con resto</strong> (o divisione euclidea) di $n$ per $b$ determina i due numeri naturali $q$ e $r$ tali che

    $$
    n = q \; b + r \qquad \text{con} \qquad 0 \le r < b .
    $$

    Il numero $n$ si chiama <strong>dividendo</strong>, $b$ <strong>divisore</strong>, $q$ <strong>quoziente</strong> e $r$ <strong>resto</strong>. I due numeri $q$ e $r$ sono unici, e scriviamo

    $$
    q = \lfloor n / b \rfloor \qquad \text{e} \qquad r = n \bmod b .
    $$

Il fatto chiave alla base del cambio di base è che una divisione per $b$ estrae la cifra meno significativa di $n$ in base $b$ e lascia come quoziente il numero formato dalle cifre rimanenti.

<a id="box-2-ch6-obsLastDigit"></a>

!!! teorema "Osservazione 5.2"

    Sia $n \ge 1$ un numero naturale la cui rappresentazione in base $b \ge 2$ è $(d_{k-1} \dots d_1 d_0)_b$. Allora

    $$
    n \bmod b = d_0
    \qquad \text{e} \qquad
    \lfloor n / b \rfloor = \sum_{i=1}^{k-1} d_i \, b^{i-1} = (d_{k-1} \dots d_1)_b ,
    $$

    dove il quoziente è $0$ se $k = 1$.

??? dimostrazione "Dimostrazione"

    Raccogliendo il fattore $b$ da tutti i termini con $i \ge 1$, otteniamo

    $$
    n = \sum_{i=0}^{k-1} d_i \, b^i = \Big( \sum_{i=1}^{k-1} d_i \, b^{i-1} \Big) \, b + d_0 .
    $$

    Poiché $d_0$ è una cifra in base $b$, si ha $0 \le d_0 < b$. Per l'unicità del quoziente e del resto della divisione con resto, il quoziente di $n$ diviso $b$ è $\sum_{i=1}^{k-1} d_i \, b^{i-1}$ e il resto è $d_0$. <span class="qed">□</span>

!!! chiave ""

    Dividendo $n$ per $b$, il resto è la cifra meno significativa $d_0$, e il quoziente è il numero scritto con le altre cifre $(d_{k-1} \dots d_1)_b$. Dividendo di nuovo il quoziente per $b$ si ottiene $d_1$, e così via: ripetendo la divisione fino a ottenere quoziente $0$ si producono tutte le cifre di $n$ in base $b$, dalla meno significativa alla più significativa, in esattamente $\lfloor \log_b n \rfloor + 1$ divisioni.

### 5.1.2 L'algoritmo

!!! chiave ""

    Dato un numero naturale $n>0$ rappresentato in base 10 (decimale) e una base di arrivo $b \geq 2$, consideriamo il problema di convertire $n$ in base $b$.

- Pseudocodice dell'algoritmo per convertire sequenze di cifre dalla base dieci alla base $b$:

!!! algoritmo "Algoritmo: ChangeOfBase"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> (in base 10) e una base <span class="arithmatex">&#92;(b &#92;ge 2&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un array <span class="arithmatex">&#92;(d&#91;1..nd&#93;&#92;)</span> di cifre in base <span class="arithmatex">&#92;(b&#92;)</span> e il numero di cifre <span class="arithmatex">&#92;(nd&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ChangeOfBase(n, b)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(nd&#92;)</span> := <span class="arithmatex">&#92;(&#92;lfloor &#92;log&#95;b n &#92;rfloor + 1&#92;)</span></span><span class="pc-c">// Numero di cifre necessarie</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d&#92;)</span> := new array<span class="arithmatex">&#92;(&#91;1..nd&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(k&#92;)</span> := <span class="arithmatex">&#92;(1&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(n &gt; 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(q&#92;)</span> := <span class="arithmatex">&#92;(&#92;lfloor n / b &#92;rfloor&#92;)</span></span><span class="pc-c">// Quoziente</span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r&#92;)</span> := <span class="arithmatex">&#92;(n &#92;bmod b&#92;)</span></span><span class="pc-c">// Resto (cifra in base <span class="arithmatex">&#92;(b&#92;)</span>)</span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d&#91;k&#93;&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(r&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(q&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(k&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(k + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(d, nd&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

- <strong>Spiegazione:</strong>

    - L'algoritmo calcola il numero di cifre $nd$ necessarie per rappresentare $n$ in base $b$ con la formula $\lfloor \log_b n \rfloor + 1$.

    - Inizializza un array $d[1..nd]$ per memorizzare le cifre e un contatore $k$ che tiene traccia della posizione corrente.

    - Il ciclo principale divide ripetutamente $n$ per $b$ per estrarre le cifre da destra a sinistra (dalla meno significativa alla più significativa).

    - A ogni iterazione il resto $r = n \bmod b$ fornisce la cifra successiva, che viene memorizzata in $d[k]$.

    - Il quoziente $q = \lfloor n / b \rfloor$ diventa il nuovo valore di $n$ per l'iterazione successiva.

    - L'algoritmo termina quando $n = 0$, restituendo l'array $d$ e il numero totale di cifre $nd$.

    - Le cifre in $d$ sono memorizzate in ordine inverso: l'elemento $d[k]$ è la cifra $d_{k-1}$ di peso $b^{k-1}$, quindi $d[1] = d_0$ è la cifra meno significativa (la più a destra) e $d[nd] = d_{nd-1}$ è la cifra più significativa (la più a sinistra).

<a id="box-3-ch6-exConversion"></a>

!!! esempio "Esempio 5.1: conversione dalla base dieci alla base $b$"

    - Conversione di $7$ in base $b=2$:

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
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(7/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $7$ in base $2$ è $(111)_{2}$, con $nd = \lfloor \log_{2} 7 \rfloor + 1 = 3$ cifre.

    - Conversione di $8$ in base $b=2$:

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
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(8/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;1&#93; = d&#95;{0}&#92;)</span> (meno significativa)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;2&#93; = d&#95;{1}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;3&#93; = d&#95;{2}&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1/2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(d&#91;4&#93; = d&#95;{3}&#92;)</span> (più significativa)</td>
        </tr>
        </table></div>

        Quindi $8$ in base $2$ è $(1000)_{2}$, con $nd = \lfloor \log_{2} 8 \rfloor + 1 = 4$ cifre.

    - Conversione di $25$ in base $b=3$:

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

    - Conversione di $100$ in base $b=8$:

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

### 5.1.3 Implementazione in <code>C++</code>

- Questa è un'implementazione in <code>C++</code> dell'algoritmo di conversione dalla base dieci alla base $b$:

```cpp
// Converte un numero decimale n in base b
// La funzione restituisce il numero di cifre nd del risultato
// digits[i] contiene la cifra in posizione i (da destra a sinistra, a partire da i=0)

int ChangeToBase(int n, int b, int *digits)
{
    int nd = 0;  // contatore del numero di cifre

    while (n > 0)
    {
        int q = n / b;  // quoziente
        int r = n % b;  // resto

        digits[nd] = r;  // memorizza la cifra in posizione nd
        n = q;           // n diventa il quoziente
        nd++;            // incrementa il contatore
    }

    return nd;  // restituisce il numero di cifre
}
```

- Per due numeri naturali <code>n</code> e <code>b</code> con <code>b</code> $\ge 1$, gli operatori <code>n / b</code> e <code>n % b</code> del <code>C++</code> calcolano esattamente il quoziente $\lfloor n/b \rfloor$ e il resto $n \bmod b$ della divisione con resto.

- L'array <code>digits</code> è indicizzato a partire da $0$: l'elemento <code>digits[i]</code> è la cifra $d_i$ di peso $b^i$. La cifra memorizzata nello pseudocodice in $d[k]$ è memorizzata in <code>C++</code> in <code>digits[k-1]</code>.

- La funzione non calcola $\lfloor \log_b n \rfloor + 1$: conta le cifre nella variabile <code>nd</code> man mano che le estrae. Ciò evita anche un problema sottile dell'aritmetica in virgola mobile: in doppia precisione <code>log(1000.0)/log(10.0)</code> vale $2.9999999999999996$, quindi la formula darebbe $3$ cifre invece delle $4$ cifre di $(1000)_{10}$.

- L'array <code>digits</code> deve essere dichiarato dal chiamante con un numero sufficiente di elementi; per esempio, $31$ elementi bastano per ogni <code>int</code> positivo (al più $2^{31}-1$) e per ogni base $b \ge 2$.

<a id="box-4-ch6-exConversionCpp"></a>

!!! esempio "Esempio 5.2: esecuzione della funzione <code>C++</code>"

    Ogni riga mostra i valori calcolati in un'iterazione del ciclo while e il contenuto dell'array <code>digits</code> dopo l'iterazione (l'elemento appena scritto è in blu; “–” indica un elemento non ancora scritto).

    - Conversione di $n = 7$ in base $b = 2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><code>q</code></th>
        <th><code>r</code></th>
        <th><code>digits[3]</code></th>
        <th><code>digits[2]</code></th>
        <th><code>digits[1]</code></th>
        <th><code>digits[0]</code></th>
        <th><code>n</code></th>
        <th><code>nd</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(7&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td>1</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        La funzione restituisce <code>nd</code> $= 3$; leggendo <code>digits</code> dalla posizione <code>2</code> alla posizione <code>0</code> si ottiene $(111)_{2}$.

    - Conversione di $n = 8$ in base $b = 2$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><code>q</code></th>
        <th><code>r</code></th>
        <th><code>digits[4]</code></th>
        <th><code>digits[3]</code></th>
        <th><code>digits[2]</code></th>
        <th><code>digits[1]</code></th>
        <th><code>digits[0]</code></th>
        <th><code>n</code></th>
        <th><code>nd</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">0</td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">0</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">0</td>
        <td>0</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        <tr>
        <td>4</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        </tr>
        </table></div>

        La funzione restituisce <code>nd</code> $= 4$; leggendo <code>digits</code> dalla posizione <code>3</code> alla posizione <code>0</code> si ottiene $(1000)_{2}$.

    - Conversione di $n = 25$ in base $b = 3$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><code>q</code></th>
        <th><code>r</code></th>
        <th><code>digits[3]</code></th>
        <th><code>digits[2]</code></th>
        <th><code>digits[1]</code></th>
        <th><code>digits[0]</code></th>
        <th><code>n</code></th>
        <th><code>nd</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(25&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td><span class="arithmatex">&#92;(8&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td>–</td>
        <td class="cella-blu">2</td>
        <td>2</td>
        <td>1</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        La funzione restituisce <code>nd</code> $= 3$; leggendo <code>digits</code> dalla posizione <code>2</code> alla posizione <code>0</code> si ottiene $(221)_{3}$.

    - Conversione di $n = 100$ in base $b = 8$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th><code>q</code></th>
        <th><code>r</code></th>
        <th><code>digits[3]</code></th>
        <th><code>digits[2]</code></th>
        <th><code>digits[1]</code></th>
        <th><code>digits[0]</code></th>
        <th><code>n</code></th>
        <th><code>nd</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td><span class="arithmatex">&#92;(100&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td>1</td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">4</td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td>2</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td>–</td>
        <td>–</td>
        <td class="cella-blu">4</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        </tr>
        <tr>
        <td>3</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td>–</td>
        <td class="cella-blu">1</td>
        <td>4</td>
        <td>4</td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        </tr>
        </table></div>

        La funzione restituisce <code>nd</code> $= 3$; leggendo <code>digits</code> dalla posizione <code>2</code> alla posizione <code>0</code> si ottiene $(144)_{8}$.

!!! chiave ""

    <strong>Punti chiave.</strong>

    - Il resto della divisione di $n$ per $b$ è la cifra meno significativa di $n$ in base $b$; il quoziente è il numero scritto con le altre cifre.

    - L'algoritmo esegue una divisione per ogni cifra: $\lfloor \log_b n \rfloor + 1$ iterazioni.

    - Le cifre vengono prodotte dalla meno significativa alla più significativa, quindi il risultato si legge al contrario: da $d[nd]$ a $d[1]$ nello pseudocodice, da <code>digits[nd-1]</code> a <code>digits[0]</code> in <code>C++</code>.

## 5.2 Test di primalità

Il cambio di base usa il resto $n \bmod b$ per leggere una cifra. Un resto uguale a zero ha un significato proprio: dice che la divisione è esatta, cioè che $b$ è un divisore di $n$. Contare i divisori porta ai numeri primi.

<a id="box-5-ch6-defDivisor"></a>

!!! definizione "Definizione 5.3: divisore"

    Un numero naturale $d \ge 1$ è un <strong>divisore</strong> di un numero naturale $n$ se esiste un numero naturale $k$ tale che $n = k \; d$:

    $$
    \text{$d$ è un divisore di $n$} \quad \Longleftrightarrow \quad \exists\, k \in \N,\ n = k \; d
    $$

    o, equivalentemente, se $n \bmod d = 0$.

<a id="box-6-ch6-defPrime"></a>

!!! definizione "Definizione 5.4: numero primo"

    Un numero naturale $n \ge 2$ è <strong>primo</strong> se i suoi unici divisori sono $1$ e $n$ stesso. Un numero naturale $n \ge 2$ che non è primo si dice <strong>composto</strong>: ha un divisore $d$ con $2 \le d \le n-1$. I numeri $0$ e $1$ non sono primi.

!!! chiave ""

    Dato un numero naturale $n$, consideriamo il problema di stabilire se $n$ è un numero primo.

### 5.2.1 Un primo algoritmo

La definizione suggerisce un algoritmo diretto: provare, uno per uno, i candidati divisori di $n$ diversi da $1$ e da $n$. L'osservazione seguente mostra che i candidati maggiori di $n/2$ si possono saltare.

<a id="box-7-ch6-obsHalf"></a>

!!! teorema "Osservazione 5.5"

    Per ogni numero naturale $n \ge 2$, se $d$ è un divisore di $n$ con $d < n$, allora $d \le n/2$.

??? dimostrazione "Dimostrazione"

    Poiché $d$ è un divisore di $n$, esiste un numero naturale $k$ tale che $n = k \; d$. Poiché $d < n$, si ha $k \ge 2$, quindi

    $$
    d = \frac{n}{k} \le \frac{n}{2} .
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Ne segue che basta controllare se qualche numero naturale $d$ in $\{2, 3, \dots, \lfloor n/2 \rfloor\}$ è un divisore di $n$. Se non esiste alcun divisore di questo tipo, $n$ è primo.

- Pseudocodice dell'algoritmo Basic Primality Test (test di primalità di base):

!!! algoritmo "Algoritmo: BasicPrimalityTest"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><code>true</code> se <span class="arithmatex">&#92;(n&#92;)</span> è primo, <code>false</code> altrimenti</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> BasicPrimalityTest(n)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &lt; 2&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span><span class="pc-c">// 0 e 1 non sono primi</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(d := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(&#92;lfloor n/2 &#92;rfloor&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;bmod d = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span><span class="pc-c">// <span class="arithmatex">&#92;(d&#92;)</span> divide <span class="arithmatex">&#92;(n&#92;)</span>: non primo</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>true</code></span><span class="pc-c">// Nessun divisore trovato: <span class="arithmatex">&#92;(n&#92;)</span> è primo</span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

- Spiegazione dell'algoritmo:

    - I numeri minori di $2$ non sono primi per definizione.

    - Il ciclo prova ogni candidato divisore $d$ da $2$ fino a $\lfloor n/2 \rfloor$.

    - Se $d$ è un divisore di $n$ (cioè $n \bmod d = 0$), la funzione restituisce subito <code>false</code>.

    - Se il ciclo termina senza trovare alcun divisore, $n$ è primo e la funzione restituisce <code>true</code>.

- Per un numero primo il ciclo viene eseguito per intero: per $n = 29$ l'algoritmo prova i $13$ candidati $d = 2, 3, \dots, 14$. Mostriamo ora che bastano molti meno candidati.

### 5.2.2 Provare i divisori fino a $\sqrt{n}$

I divisori di un numero naturale si presentano a coppie: $d$ e $n/d$. In ogni coppia, uno dei due numeri è al più $\sqrt{n}$.

<a id="box-8-ch6-obsPair"></a>

!!! teorema "Osservazione 5.6"

    Per ogni numero naturale $n \ge 2$, se $d$ è un divisore di $n$ allora $n/d$ è un divisore di $n$.

??? dimostrazione "Dimostrazione"

    Se $d$ è un divisore di $n$, allora esiste un numero naturale $k$ tale che

    $$
    n = k \; d.
    $$

    Poiché $k = n/d$, ne segue che $n/d$ è un numero naturale. Quindi

    $$
    n = d \left(\frac{n}{d}\right),
    $$

    quindi anche $n/d$ è un divisore di $n$. <span class="qed">□</span>

<a id="box-9-ch6-obsSqrt"></a>

!!! teorema "Osservazione 5.7"

    Per ogni numero naturale $n \ge 2$, se $d > \sqrt{n}$ allora $n/d < \sqrt{n}$.

??? dimostrazione "Dimostrazione"

    Se $d > \sqrt{n}$, dividendo $n$ per entrambi i membri di questa disuguaglianza otteniamo

    $$
    \frac{n}{d} < \frac{n}{\sqrt{n}} = \sqrt{n}.
    $$

    Quindi $n/d$ è minore di $\sqrt{n}$. <span class="qed">□</span>

<a id="box-10-ch6-corSqrt"></a>

!!! teorema "Corollario 5.8"

    Ogni numero naturale composto $n \ge 2$ ha un divisore $d$ con $2 \le d \le \lfloor \sqrt{n} \rfloor$. Equivalentemente, un numero naturale $n \ge 2$ è primo se e solo se nessun numero naturale in $\{2, 3, \dots, \lfloor \sqrt{n} \rfloor\}$ è un divisore di $n$.

??? dimostrazione "Dimostrazione"

    Poiché $n$ è composto, ha un divisore $d$ con $2 \le d \le n-1$. Se $d \le \sqrt{n}$, allora $d \le \lfloor \sqrt{n} \rfloor$, perché $d$ è un numero naturale, e abbiamo finito. Altrimenti $d > \sqrt{n}$: per le due osservazioni precedenti, $n/d$ è un divisore di $n$ con $n/d < \sqrt{n}$, e $n/d \ge 2$ perché $d < n$. Quindi $n/d$ è un divisore di $n$ con $2 \le n/d \le \lfloor \sqrt{n} \rfloor$. <span class="qed">□</span>

!!! chiave ""

    Dalle osservazioni precedenti sappiamo che, per ogni numero naturale $n \ge 2$, se $d > \sqrt{n}$ è un divisore di $n$, allora anche $n/d$ è un divisore di $n$ e $n/d < \sqrt{n}$. Ne segue che ogni divisore di $n$ maggiore di $\sqrt{n}$ è accoppiato a un divisore di $n$ minore di $\sqrt{n}$. Quindi, se $n$ ha un qualche divisore (diverso da $1$ e da $n$), almeno uno di essi deve essere $\le \sqrt{n}$.

<a id="box-11-ch6-exPairs"></a>

!!! esempio "Esempio 5.3: illustrazione della proprietà"

    Consideriamo $n = 36$: $\sqrt{36} = 6$. I divisori di $36$ diversi da $1$ e da $36$ sono $2, 3, 4, 6, 9, 12, 18$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>divisore <span class="arithmatex">&#92;(d &gt; &#92;sqrt{36}&#92;)</span></th>
    <th>divisore accoppiato <span class="arithmatex">&#92;(36/d &lt; &#92;sqrt{36}&#92;)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    <td><span class="arithmatex">&#92;(36/9  = 4&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    <td><span class="arithmatex">&#92;(36/12 = 3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(18&#92;)</span></td>
    <td><span class="arithmatex">&#92;(36/18 = 2&#92;)</span></td>
    </tr>
    </table></div>

    Ogni divisore $> 6$ è accoppiato a un divisore $< 6$; il divisore $6 = \sqrt{36}$ è accoppiato con se stesso.

- Per il corollario, il ciclo dell'algoritmo di base può fermarsi a $\lfloor \sqrt{n} \rfloor$ invece che a $\lfloor n/2 \rfloor$.

- Pseudocodice dell'algoritmo Primality Test (test di primalità):

!!! algoritmo "Algoritmo: PrimalityTest"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><code>true</code> se <span class="arithmatex">&#92;(n&#92;)</span> è primo, <code>false</code> altrimenti</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> PrimalityTest(n)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &lt; 2&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span><span class="pc-c">// 0 e 1 non sono primi</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d := 2&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(d &#92;le &#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(n &#92;bmod d = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>false</code></span><span class="pc-c">// <span class="arithmatex">&#92;(d&#92;)</span> divide <span class="arithmatex">&#92;(n&#92;)</span>: non primo</span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(d &#92;leftarrow d + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <code>true</code></span><span class="pc-c">// Nessun divisore trovato: <span class="arithmatex">&#92;(n&#92;)</span> è primo</span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

- Spiegazione dell'algoritmo:

    - I numeri minori di $2$ non sono primi per definizione.

    - Il ciclo prova ogni candidato divisore $d$ da $2$ fino a $\lfloor\sqrt{n}\rfloor$.

    - Se $d$ divide $n$ (cioè $n \bmod d = 0$), la funzione restituisce subito <code>false</code>.

    - Se il ciclo termina senza trovare alcun divisore, allora, per il corollario, $n$ è primo e la funzione restituisce <code>true</code>.

    - Per $n = 2$ e $n = 3$ si ha $\lfloor \sqrt{n} \rfloor = 1 < 2$: il ciclo non viene eseguito e la funzione restituisce <code>true</code>.

<a id="box-12-ch6-exPrimality"></a>

!!! esempio "Esempio 5.4: test di primalità"

    - Verifica $n = 36$: $\lfloor\sqrt{36}\rfloor = 6$

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

    - Verifica $n = 29$: $\lfloor\sqrt{29}\rfloor = 5$

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
        <td colspan="3">Il ciclo termina. Restituisce <code>true</code>: <strong>29 è primo</strong>.</td>
        </tr>
        </table></div>

    - Verifica $n = 25$: $\lfloor\sqrt{25}\rfloor = 5$

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

    Per il numero primo $29$ l'algoritmo prova $4$ candidati, mentre l'algoritmo di base ne prova $13$.

### 5.2.3 Implementazione in <code>C++</code>

- Questa è un'implementazione in <code>C++</code> dell'algoritmo Primality Test:

```cpp
// Restituisce true se n è primo, false altrimenti

bool PrimalityTest(int n)
{
    if (n < 2)
    {
        return false;  // 0 e 1 non sono primi
    }

    for (int d = 2; d <= (int)sqrt((double)n); d++)
    {
        if (n % d == 0)
        {
            return false;  // d divide n: non è primo
        }
    }

    return true;  // Nessun divisore trovato: n è primo
}
```

- La funzione <code>sqrt</code> dell'header <code>cmath</code> opera su numeri in virgola mobile: il cast <code>(double)</code> converte <code>n</code> in un numero in virgola mobile, e il cast <code>(int)</code> tronca la radice quadrata, quindi il test confronta <code>d</code> con $\lfloor \sqrt{n} \rfloor$.

- Il ciclo while dello pseudocodice diventa un ciclo for: l'inizializzazione <code>d = 2</code>, il test su <code>d</code> e l'incremento <code>d++</code> sono scritti nella sua intestazione.

<a id="box-13-ch6-exPrimalityCpp"></a>

!!! esempio "Esempio 5.5: esecuzione della funzione <code>C++</code>"

    Sui tre numeri dell'esempio precedente la funzione esegue gli stessi test:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><code>n</code></th>
    <th><code>(int)sqrt((double)n)</code></th>
    <th>valori di <code>d</code> provati</th>
    <th>valore restituito</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(36&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span> (con <code>36 % 2 == 0</code>)</td>
    <td><code>false</code>: <span class="arithmatex">&#92;(36&#92;)</span> non è primo</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(29&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2, 3, 4, 5&#92;)</span> (nessun resto è <span class="arithmatex">&#92;(0&#92;)</span>)</td>
    <td><code>true</code>: <span class="arithmatex">&#92;(29&#92;)</span> è primo</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2, 3, 4, 5&#92;)</span> (con <code>25 % 5 == 0</code>)</td>
    <td><code>false</code>: <span class="arithmatex">&#92;(25&#92;)</span> non è primo</td>
    </tr>
    </table></div>

    Per $n = 29$, dopo l'iterazione con <code>d = 5</code> l'incremento dà <code>d = 6</code>, il test $6 \le 5$ è falso e il ciclo termina.

!!! chiave ""

    <strong>Punti chiave.</strong>

    - I divisori di $n$ si presentano a coppie $d$ e $n/d$, e in ogni coppia uno dei due numeri è al più $\sqrt{n}$.

    - Quindi $n \ge 2$ è primo se e solo se nessun numero naturale in $\{2, 3, \dots, \lfloor \sqrt{n} \rfloor\}$ lo divide.

    - Il Primality Test esegue al più $\lfloor \sqrt{n} \rfloor - 1$ iterazioni, invece delle $\lfloor n/2 \rfloor - 1$ iterazioni dell'algoritmo di base.

## 5.3 Crivello di Eratostene

Il Primality Test risponde alla domanda per un solo numero. Quando servono tutti i numeri primi fino a $n$, chiamarlo su $2, 3, \dots, n$ ripete molte divisioni; il crivello lavora al contrario: invece di cercare i divisori di ciascun numero, cancella i multipli di ciascun primo.

!!! chiave ""

    Dato un numero naturale $n$, consideriamo il problema di determinare tutti i numeri primi minori o uguali a $n$.

- Il <strong>crivello di Eratostene</strong> è un algoritmo antico (attribuito al matematico greco Eratostene di Cirene, ca. 276–194 a.C.) che calcola tutti i numeri primi fino a un numero naturale $n$.

- L'idea chiave è partire con tutti i numeri naturali da $2$ a $n$ marcati come potenzialmente primi, e poi marcare iterativamente come composti i multipli di ciascun primo.

<a id="box-14-ch6-defMultiple"></a>

!!! definizione "Definizione 5.9: multiplo"

    Un numero naturale $m$ è un <strong>multiplo</strong> di un numero naturale $p \ge 1$ se esiste un numero naturale $k$ tale che $m = k \; p$:

    $$
    \text{$m$ è un multiplo di $p$} \quad \Longleftrightarrow \quad \exists\, k \in \N,\ m = k \; p
    $$

    o, equivalentemente, se $m \bmod p = 0$.

La prima osservazione dice da dove può partire la marcatura dei multipli di $p$.

<a id="box-15-ch6-obsSieveStart"></a>

!!! teorema "Osservazione 5.10"

    Per ogni numero naturale $p \ge 2$, se un numero naturale $m$ è un multiplo di $p$ con $p < m < p^2$, allora $m$ ha un divisore $d$ con $2 \le d < p$.

??? dimostrazione "Dimostrazione"

    Poiché $m$ è un multiplo di $p$, esiste un numero naturale $d$ tale che $m = d \; p$. Allora $d$ è un divisore di $m$.

    Inoltre, poiché $m > p$ e $m = d \; p$, si ha $d \ge 2$. Poiché $m < p^2$ e $m = d \; p$, si ha $d < p$. Quindi $2 \le d < p$. <span class="qed">□</span>

!!! chiave ""

    Dall'osservazione precedente, per ogni primo $p$ e ogni multiplo $m$ di $p$ con $p < m < p^2$, il numero $m$ ha un divisore $d$ con $2 \le d < p$. Quindi $m$ ha anche un divisore primo $q$ con $2 \le q < p$, ed era perciò già stato marcato come composto quando è stato elaborato $q$. Dunque, nel marcare i multipli di $p$, si può partire da $p^2$.

<a id="box-16-ch6-exSieveStart"></a>

!!! esempio "Esempio 5.6: illustrazione della proprietà"

    Sia $p = 5$. I suoi multipli compresi tra $p$ e $p^2 = 25$ sono $m = 10, 15, 20$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>multiplo <span class="arithmatex">&#92;(m&#92;)</span></th>
    <th><span class="arithmatex">&#92;(m = d &#92;cdot p&#92;)</span></th>
    <th>divisore <span class="arithmatex">&#92;(d &lt; p&#92;)</span></th>
    <th>già marcato quando</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10 = 2 &#92;cdot 5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d = 2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(p = 2&#92;)</span> (da <span class="arithmatex">&#92;(j = 4&#92;)</span>, passo <span class="arithmatex">&#92;(2&#92;)</span>)</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    <td><span class="arithmatex">&#92;(15 = 3 &#92;cdot 5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d = 3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(p = 3&#92;)</span> (da <span class="arithmatex">&#92;(j = 9&#92;)</span>, passo <span class="arithmatex">&#92;(3&#92;)</span>)</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(20&#92;)</span></td>
    <td><span class="arithmatex">&#92;(20 = 4 &#92;cdot 5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(d = 4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(p = 2&#92;)</span> (da <span class="arithmatex">&#92;(j = 4&#92;)</span>, passo <span class="arithmatex">&#92;(2&#92;)</span>)</td>
    </tr>
    </table></div>

    Il numero $20$ ha il divisore $d = 4$, che non è primo, e anche il divisore primo $2$, che lo ha marcato. Il multiplo successivo è $25 = 5 \cdot 5 = p^2$, che non è stato marcato da nessun primo precedente. Quindi, per $p = 5$, si può iniziare a marcare i numeri da $25$.

La seconda osservazione dice dove può fermarsi il ciclo esterno su $p$.

<a id="box-17-ch6-obsSieveStop"></a>

!!! teorema "Osservazione 5.11"

    Per ogni numero naturale $n \ge 2$, ogni numero naturale composto $m \le n$ ha un divisore primo $q$ con $q \le \lfloor \sqrt{n} \rfloor$.

??? dimostrazione "Dimostrazione"

    Per il corollario della sezione «Test di primalità», $m$ ha un divisore $d$ con $2 \le d \le \lfloor \sqrt{m} \rfloor \le \lfloor \sqrt{n} \rfloor$. Sia $q$ il più piccolo divisore di $m$ con $q \ge 2$; allora $q \le d \le \lfloor \sqrt{n} \rfloor$. Il numero $q$ è primo: se $q$ avesse un divisore $c$ con $2 \le c < q$, allora $c$ sarebbe anche un divisore di $m$ (da $q = k_1 c$ e $m = k_2 q$ si ottiene $m = k_2 k_1 c$), contro la scelta di $q$ come il più piccolo. <span class="qed">□</span>

- Quindi, dopo che sono stati marcati i multipli di tutti i primi $p \le \lfloor \sqrt{n} \rfloor$, ogni numero composto fino a $n$ è marcato, e il ciclo esterno può fermarsi.

- Pseudocodice del crivello di Eratostene:

!!! algoritmo "Algoritmo: SieveOfEratosthenes"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un numero naturale <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>Un array booleano <span class="arithmatex">&#92;(prime&#91;1..n&#93;&#92;)</span> dove <span class="arithmatex">&#92;(prime&#91;i&#93; = 1&#92;)</span> se e solo se <span class="arithmatex">&#92;(i&#92;)</span> è primo</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> SieveOfEratosthenes(<span class="arithmatex">&#92;(n&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prime := &#92;text{new array}&#91;1..n&#93;&#92;)</span></span><span class="pc-c">// dichiara l'array booleano</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prime &#92;leftarrow 1&#92;)</span></span><span class="pc-c">// inizializza tutti gli elementi a 1</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prime&#91;1&#93; &#92;leftarrow 0&#92;)</span></span><span class="pc-c">// 1 non è primo</span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p := 2&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(p &#92;le &#92;lfloor&#92;sqrt{n}&#92;rfloor&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(prime&#91;p&#93; = 1&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j := p^2&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(j &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prime&#91;j&#93; &#92;leftarrow 0&#92;)</span></span><span class="pc-c">// <span class="arithmatex">&#92;(j&#92;)</span> non è primo</span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(j &#92;leftarrow j + p&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(p &#92;leftarrow p + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(prime&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

- Spiegazione dell'algoritmo:

    - L'array $prime$ viene dichiarato e tutti i suoi elementi sono inizializzati a $1$; l'elemento $prime[1]$ viene subito posto a $0$, poiché $1$ non è primo.

    - Il ciclo esterno scorre ogni candidato primo $p$ da $2$ fino a $\lfloor\sqrt{n}\rfloor$.

    - Se $prime[p] = 1$, allora $p$ è primo (un $p$ composto sarebbe stato marcato dal suo più piccolo divisore primo), e tutti i suoi multipli a partire da $p^2$ sono posti a $0$.

    - Il ciclo interno parte da $p^2$ perché tutti i multipli più piccoli $2p, 3p, \ldots, (p{-}1)p$ sono già stati posti a $0$ nell'elaborare i primi più piccoli $2, 3, 5, 7, \ldots$.

    - Dopo l'esecuzione dell'algoritmo, $prime[i] = 1$ se e solo se $i$ è primo.

<a id="box-18-ch6-exSieve10"></a>

!!! esempio "Esempio 5.7: crivello di Eratostene ($n=10$)"

    Con $n=10$ ($\lfloor\sqrt{10}\rfloor = 3$), ogni riga mostra lo stato dell'array $prime[1..10]$ dopo l'assegnamento $prime[j] \leftarrow 0$. Le celle blu indicano gli elementi appena posti a $0$; le celle rosse indicano il valore corrente di $p$.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th></th>
    <th colspan="10"><span class="arithmatex">&#92;(prime&#91;1..10&#93;&#92;)</span></th>
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
    <td><span class="arithmatex">&#92;(prime&#91;10&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>12</td>
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
    <td><span class="arithmatex">&#92;(j = 12 &gt; 10&#92;)</span>: arresto</td>
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
    <td><span class="arithmatex">&#92;(prime&#91;9&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>12</td>
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
    <td><span class="arithmatex">&#92;(j = 12 &gt; 10&#92;)</span>: arresto</td>
    </tr>
    <tr>
    <td colspan="13">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 4 &gt; &#92;lfloor&#92;sqrt{10}&#92;rfloor = 3&#92;)</span>.</td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> i numeri primi $\le 10$ sono $2,\ 3,\ 5,\ 7$.

<a id="box-19-ch6-exSieve20"></a>

!!! esempio "Esempio 5.8: crivello di Eratostene ($n=20$)"

    Con $n=20$ ($\lfloor\sqrt{20}\rfloor = 4$), ogni riga mostra lo stato dell'array $prime[1..20]$ dopo l'assegnamento $prime[j] \leftarrow 0$. Celle blu: elemento appena posto a $0$; celle rosse: valore corrente di $p$. Quando l'elemento è già $0$, l'assegnamento non modifica l'array.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th></th>
    <th colspan="20"><span class="arithmatex">&#92;(prime&#91;1..20&#93;&#92;)</span></th>
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
    <td>16</td>
    <td>17</td>
    <td>18</td>
    <td>19</td>
    <td>20</td>
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
    <td>1</td>
    <td>1</td>
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
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;14&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>16</td>
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
    <td>0</td>
    <td>1</td>
    <td class="cella-blu">0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;16&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>18</td>
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
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td class="cella-blu">0</td>
    <td>1</td>
    <td>1</td>
    <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>20</td>
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
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td class="cella-blu">0</td>
    <td><span class="arithmatex">&#92;(prime&#91;20&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>22</td>
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
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">&#92;(j = 22 &gt; 20&#92;)</span>: arresto</td>
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
    <td>0</td>
    <td>1</td>
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
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
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
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td><span class="arithmatex">&#92;(prime&#91;15&#93; &#92;leftarrow 0&#92;)</span></td>
    </tr>
    <tr>
    <td></td>
    <td>18</td>
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
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td><span class="arithmatex">&#92;(prime&#91;18&#93; &#92;leftarrow 0&#92;)</span> (già <span class="arithmatex">&#92;(0&#92;)</span>)</td>
    </tr>
    <tr>
    <td></td>
    <td>21</td>
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
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">&#92;(j = 21 &gt; 20&#92;)</span>: arresto</td>
    </tr>
    <tr>
    <td class="cella-rossa">4</td>
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
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span class="arithmatex">&#92;(prime&#91;4&#93; = 0&#92;)</span>: salta</td>
    </tr>
    <tr>
    <td colspan="23">Il ciclo esterno termina: <span class="arithmatex">&#92;(p = 5 &gt; &#92;lfloor&#92;sqrt{20}&#92;rfloor = 4&#92;)</span>.</td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> i numeri primi $\le 20$ sono $2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19$.

### 5.3.1 Implementazione in <code>C++</code>

- Questa è un'implementazione in <code>C++</code> del crivello di Eratostene:

```cpp
// l'array in input è già dichiarato con n+1 posizioni
// e inizializzato a 1, e n vale almeno 2
int SieveOfEratosthenes(int n, int *prime)
{
    prime[0] = 0;
    prime[1] = 0;

    for (int p = 2; p <= (int)sqrt((double)n); p++)
    {
        if (prime[p] == 1)
        {
            // Marca i multipli di p a partire da p*p
            for (int j = p * p; j <= n; j += p)
            {
                prime[j] = 0;  // j non è primo
            }
        }
    }

    return 1;
}
```

- In <code>C++</code> l'array è indicizzato a partire da $0$. Per mantenere l'elemento <code>prime[i]</code> associato al numero $i$, l'array ha $n+1$ elementi, <code>prime[0..n]</code>; l'elemento in più <code>prime[0]</code> si riferisce al numero $0$, che non è primo, ed è posto a $0$.

- I due cicli while dello pseudocodice diventano due cicli for; quello interno avanza con <code>j += p</code>.

<a id="box-20-ch6-exSieveCpp"></a>

!!! esempio "Esempio 5.9: esecuzione della funzione <code>C++</code>"

    Ogni riga mostra l'array <code>prime[0..n]</code> al termine di un'iterazione del ciclo esterno, con i valori di <code>j</code> del suo ciclo interno; gli elementi modificati in quell'iterazione sono in blu.

    - Esecuzione per $n = 10$ (<code>(int)sqrt((double)10)</code> $= 3$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th colspan="11"><code>prime[0..10]</code></th>
        </tr>
        <tr>
        <td><code>p</code></td>
        <td>0</td>
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
        </tr>
        <tr>
        <td>inizio</td>
        <td>0</td>
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
        </tr>
        <tr>
        <td>2</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        </tr>
        <tr>
        <td>3</td>
        <td>0</td>
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
        </tr>
        </table></div>

        Valori di <code>j</code> nel ciclo interno: per <code>p = 2</code>: <code>j</code> $= 4, 6, 8, 10$; per <code>p = 3</code>: <code>j</code> $= 9$.

    - Esecuzione per $n = 20$ (<code>(int)sqrt((double)20)</code> $= 4$):

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th colspan="21"><code>prime[0..20]</code></th>
        </tr>
        <tr>
        <td><code>p</code></td>
        <td>0</td>
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
        <td>16</td>
        <td>17</td>
        <td>18</td>
        <td>19</td>
        <td>20</td>
        </tr>
        <tr>
        <td>inizio</td>
        <td>0</td>
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
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        </tr>
        <tr>
        <td>2</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        <td>1</td>
        <td class="cella-blu">0</td>
        </tr>
        <tr>
        <td>3</td>
        <td>0</td>
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
        <td class="cella-blu">0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        </tr>
        <tr>
        <td>4</td>
        <td>0</td>
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
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        </tr>
        </table></div>

        Valori di <code>j</code> nel ciclo interno: per <code>p = 2</code>: <code>j</code> $= 4, 6, 8, 10, 12, 14, 16, 18, 20$; per <code>p = 3</code>: <code>j</code> $= 9, 12, 15, 18$; per <code>p = 4</code>: nessun ciclo interno, poiché <code>prime[4]</code> è $0$.

    Alla fine gli elementi uguali a $1$ sono quelli dei numeri primi: $2,\ 3,\ 5,\ 7$ per $n = 10$, e $2,\ 3,\ 5,\ 7,\ 11,\ 13,\ 17,\ 19$ per $n = 20$.

!!! chiave ""

    <strong>Punti chiave.</strong>

    - Il crivello non divide: marca come composti i multipli di ciascun primo $p$.

    - La marcatura dei multipli di $p$ parte da $p^2$: i multipli più piccoli hanno un divisore primo più piccolo e sono già marcati.

    - Il ciclo esterno si ferma a $\lfloor \sqrt{n} \rfloor$: ogni numero composto fino a $n$ ha un divisore primo non maggiore di $\lfloor \sqrt{n} \rfloor$.

## 5.4 Massimo comun divisore

L'ultimo algoritmo del capitolo tratta due numeri alla volta: cerchiamo i divisori che hanno in comune.

<a id="box-21-ch6-defGCD"></a>

!!! definizione "Definizione 5.12: divisore comune e massimo comun divisore"

    Siano $n, m$ due numeri naturali con $n, m \ge 1$.

    - Un numero naturale $d \ge 1$ è un <strong>divisore comune</strong> di $n$ e $m$ se $d$ è un divisore sia di $n$ sia di $m$, cioè se esistono numeri naturali $k_1, k_2$ tali che

        $$
        n = k_1 \; d \qquad \text{e} \qquad m = k_2 \; d.
        $$

        Equivalentemente, $n \bmod d = 0$ e $m \bmod d = 0$.

    - Il <strong>massimo comun divisore</strong> di $n$ e $m$, indicato con $\gcd(n, m)$, è il più grande divisore comune di $n$ e $m$.

- Il massimo comun divisore esiste sempre: $1$ è un divisore comune, e ogni divisore comune è al più $\min\{n, m\}$.

- Per esempio, i divisori comuni di $48$ e $18$ sono $1, 2, 3, 6$, quindi $\gcd(48, 18) = 6$.

!!! chiave ""

    Dati due numeri naturali $n, m$ con $n, m \ge 1$, consideriamo il problema di calcolare il loro massimo comun divisore.

L'osservazione seguente sostituisce la coppia $(n, m)$ con una coppia di numeri più piccoli che ha lo stesso massimo comun divisore.

<a id="box-22-ch6-obsEuclid"></a>

!!! teorema "Osservazione 5.13"

    Per ogni coppia di numeri naturali $n \ge 1$ e $m \ge 1$,

    $$
    \gcd(n, m) = \gcd(m,\ n \bmod m).
    $$

??? dimostrazione "Dimostrazione"

    Sia $q = \lfloor n/m \rfloor$, in modo che $n = q m + (n \bmod m)$.

    Sia $d_1$ un divisore comune di $n$ e $m$. Allora esistono numeri naturali $k_1, k_2$ tali che

    $$
    n = k_1 d_1 \qquad \text{e} \qquad m = k_2 d_1.
    $$

    Poiché $n \bmod m = n - qm$, otteniamo

    $$
    n \bmod m = (k_1 - qk_2)\,d_1,
    $$

    dove $k_1 - q k_2 \ge 0$ perché $n \bmod m \ge 0$. Quindi $d_1$ è anche un divisore di $n \bmod m$. Perciò $d_1$ è un divisore comune di $m$ e $n \bmod m$.

    Viceversa, sia $d_2$ un divisore comune di $m$ e $n \bmod m$. Allora esistono numeri naturali $k_1, k_2$ tali che

    $$
    m = k_1 d_2 \qquad \text{e} \qquad n \bmod m = k_2 d_2.
    $$

    Poiché $n = qm + (n \bmod m)$, otteniamo

    $$
    n = (qk_1 + k_2)\,d_2,
    $$

    quindi $d_2$ è anche un divisore di $n$. Perciò $d_2$ è un divisore comune di $n$ e $m$.

    Dunque $n$ e $m$ hanno esattamente gli stessi divisori comuni di $m$ e $n \bmod m$, e quindi

    $$
    \gcd(n,m)=\gcd(m,\,n \bmod m).
    $$

    Nel membro di destra, $\gcd(m, 0)$ è inteso come il più grande divisore di $m$ (ogni $d \ge 1$ divide $0 = 0 \cdot d$), cioè $m$ stesso. <span class="qed">□</span>

### 5.4.1 Algoritmo di Euclide

- L'<strong>algoritmo di Euclide</strong> (attribuito all'antico matematico greco Euclide, ca. 300 a.C.) calcola $\gcd(n, m)$ in modo efficiente sostituendo ripetutamente la coppia $(n,m)$ con $(m,\ n \bmod m)$.

- L'algoritmo non richiede $n \ge m$: se $n < m$, allora $n \bmod m = n$, e la prima sostituzione scambia semplicemente i due numeri, trasformando $(n, m)$ in $(m, n)$.

!!! chiave ""

    - Per l'osservazione precedente, sostituire $(n,m)$ con $(m,\ n \bmod m)$ non cambia il massimo comun divisore.

    - Poiché $n \bmod m < m$, il secondo argomento decresce strettamente a ogni sostituzione.

    - Dunque l'algoritmo termina quando il resto diventa $0$; a quel punto il massimo comun divisore è l'altro argomento:

        $$
        \gcd(n,0)=n.
        $$

- Pseudocodice dell'algoritmo di Euclide:

!!! algoritmo "Algoritmo: EuclideanAlgorithm"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due numeri naturali <span class="arithmatex">&#92;(n, m &#92;ge 1&#92;)</span></span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span><span class="arithmatex">&#92;(&#92;gcd(n, m)&#92;)</span></span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> EuclideanAlgorithm(<span class="arithmatex">&#92;(n&#92;)</span>, <span class="arithmatex">&#92;(m&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(m &#92;ne 0&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(r := n &#92;bmod m&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow m&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(m &#92;leftarrow r&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(n&#92;)</span></span><span class="pc-c">// <span class="arithmatex">&#92;(m = 0&#92;)</span>: <span class="arithmatex">&#92;(n&#92;)</span> è il MCD</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

- Spiegazione dell'algoritmo:

    - A ogni passo, $(n, m)$ viene sostituita da $(m,\ n \bmod m)$.

    - Per l'osservazione precedente, questa sostituzione conserva il valore di $\gcd(n,m)$: indicando con $n_0$ e $m_0$ i valori in input, a ogni iterazione $\gcd(n, m) = \gcd(n_0, m_0)$.

    - Poiché $n \bmod m < m$, il valore di $m$ decresce strettamente a ogni iterazione, quindi l'algoritmo termina.

    - Quando $m = 0$, l'uguaglianza $\gcd(n, m) = \gcd(n_0, m_0)$ insieme a $\gcd(n, 0) = n$ dà il risultato.

<a id="box-23-ch6-exGCD"></a>

!!! esempio "Esempio 5.10: calcolo del MCD"

    - Calcoliamo $\gcd(48, 18)$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>passo</th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(m&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(48&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(48 &#92;bmod 18 = 12&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18 &#92;bmod 12 = 6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 &#92;bmod 6 = 0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>— (il ciclo termina)</td>
        </tr>
        </table></div>

        <strong>Risultato:</strong> $\gcd(48, 18) = 6$.

    - Calcoliamo $\gcd(252, 105)$:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>passo</th>
        <th><span class="arithmatex">&#92;(n&#92;)</span></th>
        <th><span class="arithmatex">&#92;(m&#92;)</span></th>
        <th><span class="arithmatex">&#92;(r = n &#92;bmod m&#92;)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(252&#92;)</span></td>
        <td><span class="arithmatex">&#92;(105&#92;)</span></td>
        <td><span class="arithmatex">&#92;(252 &#92;bmod 105 = 42&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(105&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(105 &#92;bmod 42 = 21&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(42 &#92;bmod 21 = 0&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(4&#92;)</span></td>
        <td><span class="arithmatex">&#92;(21&#92;)</span></td>
        <td><span class="arithmatex">&#92;(0&#92;)</span></td>
        <td>— (il ciclo termina)</td>
        </tr>
        </table></div>

        <strong>Risultato:</strong> $\gcd(252, 105) = 21$.

### 5.4.2 Coprimalità

<a id="box-24-ch6-defCoprime"></a>

!!! definizione "Definizione 5.14: numeri coprimi"

    Due numeri naturali $n, m \ge 1$ si dicono <strong>coprimi</strong> (o <strong>primi tra loro</strong>) se non hanno alcun divisore comune diverso da $1$:

    $$
    n \text{ e } m \text{ sono coprimi} \quad\Longleftrightarrow\quad \gcd(n, m) = 1 .
    $$

- Poiché l'algoritmo di Euclide calcola $\gcd(n,m)$, per verificare la coprimalità basta chiamare l'algoritmo e controllare se il risultato è uguale a $1$.

<a id="box-25-ch6-exCoprime"></a>

!!! esempio "Esempio 5.11: test di coprimalità"

    - Calcoliamo $\gcd(35, 12)$: l'algoritmo di Euclide restituisce $1$. Quindi $35$ e $12$ sono <strong>coprimi</strong>.

    - Calcoliamo $\gcd(48, 18)$: l'algoritmo di Euclide restituisce $6$. Quindi $48$ e $18$ <strong>non sono coprimi</strong>.

### 5.4.3 Implementazione in <code>C++</code>

- Questa è un'implementazione in <code>C++</code> dell'algoritmo di Euclide:

```cpp
int EuclideanAlgorithm(int n, int m)
{
    while (m != 0)
    {
        int r = n % m;
        n = m;
        m = r;
    }
    return n;  // m == 0: n è il MCD
}
```

- I parametri <code>n</code> e <code>m</code> sono passati per valore: la funzione modifica le proprie copie, e le variabili del chiamante conservano i loro valori.

<a id="box-26-ch6-exGCDCpp"></a>

!!! esempio "Esempio 5.12: esecuzione della funzione <code>C++</code>"

    Ogni riga mostra il test del ciclo while, il resto calcolato e i valori di <code>n</code> e <code>m</code> al termine dell'iterazione (in blu).

    - Esecuzione per <code>n = 48</code>, <code>m = 18</code>:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th>test <code>m != 0</code></th>
        <th><code>r = n % m</code></th>
        <th><code>n</code></th>
        <th><code>m</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(48&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(48 &#92;bmod 18 = 12&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(18&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(12&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(18 &#92;bmod 12 = 6&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(6&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(6 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 &#92;bmod 6 = 0&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(6&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td colspan="5">Test <code>m != 0</code> falso: il ciclo termina e la funzione restituisce <code>n</code> <span class="arithmatex">&#92;(= 6&#92;)</span>.</td>
        </tr>
        </table></div>

    - Esecuzione per <code>n = 35</code>, <code>m = 12</code>:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th>iterazione</th>
        <th>test <code>m != 0</code></th>
        <th><code>r = n % m</code></th>
        <th><code>n</code></th>
        <th><code>m</code></th>
        </tr>
        <tr>
        <td>inizio</td>
        <td></td>
        <td></td>
        <td><span class="arithmatex">&#92;(35&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(35 &#92;bmod 12 = 11&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(12&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(11&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(2&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(12 &#92;bmod 11 = 1&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(11&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(1&#92;)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">&#92;(3&#92;)</span></td>
        <td><span class="arithmatex">&#92;(1 &#92;ne 0&#92;)</span></td>
        <td><span class="arithmatex">&#92;(11 &#92;bmod 1 = 0&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(1&#92;)</span></td>
        <td class="cella-blu"><span class="arithmatex">&#92;(0&#92;)</span></td>
        </tr>
        <tr>
        <td colspan="5">Test <code>m != 0</code> falso: il ciclo termina e la funzione restituisce <code>n</code> <span class="arithmatex">&#92;(= 1&#92;)</span>.</td>
        </tr>
        </table></div>

    Quindi $\gcd(48, 18) = 6$ e $\gcd(35, 12) = 1$.

!!! chiave ""

    <strong>Punti chiave.</strong>

    - Le coppie $(n, m)$ e $(m,\ n \bmod m)$ hanno gli stessi divisori comuni, quindi lo stesso massimo comun divisore.

    - L'algoritmo di Euclide ripete la sostituzione finché il secondo numero è $0$, e restituisce il primo, poiché $\gcd(n, 0) = n$.

    - Due numeri sono coprimi se e solo se l'algoritmo di Euclide restituisce $1$.

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

## Laboratorio interattivo { #laboratorio-interattivo }

L'algoritmo del capitolo, un passo alla volta: muovi i cursori e premi ▶.
Lo stesso grafico a tutta pagina, con gli altri del corso, è nel [laboratorio interattivo](../laboratorio/euclide-crivello.md).

<div class="gi" data-grafico="euclide-crivello"></div>
