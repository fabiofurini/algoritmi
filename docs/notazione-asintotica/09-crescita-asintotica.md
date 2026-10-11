---
title: "Crescita asintotica"
---

# Crescita asintotica

<div class="info-capitolo" markdown>

**Parte 3 · Crescita e notazione asintotica · Capitolo 9** · [:material-file-pdf-box: Dispensa, volume 3 (PDF)](../pdf/dispensa-3-notazione-asintotica.pdf) · [:material-pencil: Esercizi](../esercizi/es-09-crescita-asintotica.md)

</div>

## Introduzione

Il numero di passi eseguiti da un algoritmo è una funzione di un numero naturale: la dimensione del suo input. Due algoritmi che risolvono lo stesso problema si confrontano guardando quanto velocemente crescono queste funzioni al crescere dell'input, e non i loro valori su poche piccole istanze. In questo capitolo studiamo le funzioni di variabile naturale che compaiono nell'analisi degli algoritmi e ne confrontiamo gli <strong>ordini di crescita</strong>.

Il capitolo è organizzato così.

- Nella Sezione [9.1](#sez-gr-sec-families) introduciamo le cinque famiglie di funzioni crescenti di variabile naturale usate nel corso: le funzioni logaritmiche, potenza, esponenziali, fattoriale e autopotenza.

- Nella Sezione [9.2](#sez-gr-sec-limits) richiamiamo i quattro limiti che mettono in ordine queste famiglie (la <strong>gerarchia degli infiniti</strong>).

- Nella Sezione [9.3](#sez-gr-sec-comparison) definiamo il confronto fra due ordini di crescita attraverso il limite del rapporto delle due funzioni. Ricaviamo poi la gerarchia degli ordini di crescita, una classificazione degli ordini di crescita e le proprietà delle funzioni logaritmiche, potenza, polinomiali ed esponenziali che si usano nell'analisi degli algoritmi.

!!! chiave ""

    <strong>Prerequisiti.</strong> Le funzioni di variabile naturale sono le <strong>successioni</strong> del corso di <em>Analisi Matematica 1</em> ([fabiofurini.github.io/analisi-matematica-1/](https://fabiofurini.github.io/analisi-matematica-1/), versione inglese [fabiofurini.github.io/mathematical-analysis-1/](https://fabiofurini.github.io/mathematical-analysis-1/)). I loro limiti, e i teoremi usati per calcolarli, non vengono rispiegati in questo capitolo: li usiamo, e rimandiamo alla parte <em>Limiti di successioni</em> di quel corso, in particolare ai capitoli <em>Calcolo dei limiti delle successioni</em> (teorema del confronto), <em>Il numero di Nepero</em> e <em>Gerarchie degli infiniti e criterio del rapporto</em>.

## 9.1 Famiglie di funzioni crescenti di variabile naturale { #sez-gr-sec-families }

Una funzione di variabile naturale è definita su un insieme di numeri naturali della forma $\N_{\ge n_0} = \{n_0, n_0+1, n_0+2, \dots\}$, e nell'analisi degli algoritmi conta solo il suo comportamento per valori grandi di $n$. Le due definizioni seguenti descrivono proprietà che valgono <em>da un certo valore di $n$ in poi</em>: nel corso di <em>Analisi Matematica 1</em> si dice che valgono <em>definitivamente</em>.

<a id="box-1-grDefPositive"></a>

!!! definizione "Definizione 9.1: funzione asintoticamente positiva"

    Una funzione di variabile naturale $f: \N_{\ge n_0} \rightarrow \R$ è <strong>asintoticamente positiva</strong> se esiste $n_1 \in \N_{\ge n_0}$ tale che:

    \begin{equation*}
    f(n) > 0, \quad \forall n \in \N_{\ge n_1} \tag{9.1}
    \end{equation*}

<a id="box-2-grDefIncreasing"></a>

!!! definizione "Definizione 9.2: funzione asintoticamente crescente"

    Una funzione di variabile naturale $f: \N_{\ge n_0} \rightarrow \R$ è <strong>asintoticamente crescente</strong> se esiste $n_1 \in \N_{\ge n_0}$ tale che:

    \begin{equation*}
    f(n) < f(n+1), \quad \forall n \in \N_{\ge n_1} \tag{9.2}
    \end{equation*}

- Le principali famiglie di funzioni di variabile naturale asintoticamente crescenti sono le seguenti.

    1. Le funzioni <strong>logaritmiche</strong> di variabile naturale:

        \begin{equation*}
        f: \N_{\ge 1} \rightarrow \R,~~~ f:n \mapsto \log_a n \quad \forall a \in \R_{>1} \tag{9.3}
        \end{equation*}

    2. Le funzioni <strong>potenza</strong> di variabile naturale:

        \begin{equation*}
        f: \N \rightarrow \R,~~~ f:n \mapsto n^{\alpha} \quad \forall \alpha \in \R_{>0} \tag{9.4}
        \end{equation*}

    3. Le funzioni <strong>esponenziali</strong> di variabile naturale:

        \begin{equation*}
        f: \N \rightarrow \R,~~~ f:n \mapsto b^{n} \quad \forall b \in \R_{>1} \tag{9.5}
        \end{equation*}

    4. La funzione <strong>fattoriale</strong> di variabile naturale:

        \begin{equation*}
        f: \N \rightarrow \R,~~~ f:n \mapsto n! \tag{9.6}
        \end{equation*}

    5. La funzione <strong>autopotenza</strong> di variabile naturale:

        \begin{equation*}
        f: \N \rightarrow \R,~~~ f:n \mapsto n^n \tag{9.7}
        \end{equation*}

        dove, per convenzione, poniamo $0^0 = 1$.

- Tutte queste funzioni sono asintoticamente positive, e tutte divergono a $\ip$ per $n \rr \ip$. Le funzioni fattoriale e autopotenza non sono crescenti su tutto il dominio, poiché $0! = 1! = 1$ e $0^0 = 1^1 = 1$, ma sono strettamente crescenti da $n = 1$ in poi: per questo parliamo di funzioni <em>asintoticamente</em> crescenti.

- In queste note $\ln n = \log_e n$ indica il logaritmo naturale, dove $e$ è il numero di Nepero.

<a id="box-3-gr-exTable"></a>

!!! esempio "Esempio 9.1: funzioni crescenti di variabile naturale"

    La tabella riporta i valori di alcune funzioni crescenti di variabile naturale, calcolati aumentando $n$ di un ordine di grandezza alla volta, da $1$ a $100$ milioni. I valori di $\ln n$ e i fattori iniziali di $2^n$ e $n!$ sono arrotondati a una cifra decimale; i valori di $n^2$ e $n^n$ sono esatti.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(n&#92;)</span></th>
    <th><span class="arithmatex">&#92;(&#92;ln n&#92;)</span></th>
    <th><span class="arithmatex">&#92;(n^2&#92;)</span></th>
    <th><span class="arithmatex">&#92;(2^n&#92;)</span></th>
    <th><span class="arithmatex">&#92;(n!&#92;)</span></th>
    <th><span class="arithmatex">&#92;(n^n&#92;)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1=10^0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10=10^1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 2.3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.0 &#92;cdot 10^{3}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 3.6&#92;cdot 10^{6}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{10}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(100=10^2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 4.6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.3 &#92;cdot 10^{30}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 9.3&#92;cdot 10^{157}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{200}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1{,}000=10^3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 6.9&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.1 &#92;cdot 10^{301}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 4.0&#92;cdot 10^{2{,}567}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{3{,}000}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10{,}000=10^4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 9.2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 2.0 &#92;cdot 10^{3{,}010}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 2.8&#92;cdot 10^{35{,}659}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{40{,}000}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(100{,}000=10^5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 11.5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{10}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.0 &#92;cdot 10^{30{,}103}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 2.8&#92;cdot 10^{456{,}573}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{500{,}000}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10^6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 13.8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{12}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 9.9 &#92;cdot 10^{301{,}029}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 8.3&#92;cdot 10^{5{,}565{,}708}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{6{,}000{,}000}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10^7&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 16.1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{14}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 9.0 &#92;cdot 10^{3{,}010{,}299}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.2&#92;cdot 10^{65{,}657{,}059}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{70{,}000{,}000}&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10^8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 18.4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{16}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 3.7 &#92;cdot 10^{30{,}102{,}999}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#92;approx 1.6&#92;cdot 10^{756{,}570{,}556}&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10^{800{,}000{,}000}&#92;)</span></td>
    </tr>
    </table></div>

    Per apprezzare questi numeri, ricordiamo che il numero di atomi dell'universo osservabile è stimato in circa $10^{82}$, e che un personal computer del 2024 esegue circa $10 \cdot 10^9 = 10^{10}$ operazioni al secondo ($10$ GFLOPS). Un algoritmo che esegue $2^n$ operazioni su un input con $n = 100$ impiega

    $$
    \frac{2^{100}}{10^{10}} \text{ secondi} \approx 1.3 \cdot 10^{20} \text{ secondi} \approx 4.0 \cdot 10^{12} \text{ anni},
    $$

    mentre un algoritmo che esegue $n^2$ operazioni ne impiega $10^{4}/10^{10} = 10^{-6}$ secondi.

- La [Figura 9.1](#box-4-gr-figFamilies) mostra i primi valori delle stesse funzioni. Poiché i valori crescono molto velocemente, l'asse verticale è in scala logaritmica: ogni linea orizzontale della griglia corrisponde a una moltiplicazione per $100$.

<a id="box-4-gr-figFamilies"></a>

![Figura 1](../img/09-crescita-asintotica/fig01.svg){ .fig loading=lazy  }

<p class="didascalia"><strong>Figura 9.1:</strong> I valori di <span class="arithmatex">&#92;(&#92;ln n&#92;)</span>, <span class="arithmatex">&#92;(n^2&#92;)</span>, <span class="arithmatex">&#92;(2^n&#92;)</span>, <span class="arithmatex">&#92;(n!&#92;)</span> e <span class="arithmatex">&#92;(n^n&#92;)</span> per <span class="arithmatex">&#92;(n &#92;in &#92;{1, 2, &#92;dots, 12&#92;}&#92;)</span> (asse verticale in scala logaritmica; i punti sono uniti da segmenti solo per leggibilità). Per piccoli valori di <span class="arithmatex">&#92;(n&#92;)</span> l'ordine delle funzioni può essere diverso da quello finale: <span class="arithmatex">&#92;(2^3 = 8 &lt; 9 = 3^2&#92;)</span>, e <span class="arithmatex">&#92;(2^n &gt; n!&#92;)</span> per <span class="arithmatex">&#92;(n &#92;in &#92;{1, 2, 3&#92;}&#92;)</span>.</p>

## 9.2 La gerarchia degli infiniti { #sez-gr-sec-limits }

Le cinque famiglie della Sezione [9.1](#sez-gr-sec-families) divergono tutte a $\ip$. Per decidere quale diverge più velocemente, calcoliamo il limite del rapporto di due di esse. I limiti di questa sezione sono la <em>gerarchia degli infiniti</em> per le successioni del corso di <em>Analisi Matematica 1</em> (capitolo <em>Gerarchie degli infiniti e criterio del rapporto</em>), dove sono dimostrati; qui li richiamiamo, insieme all'idea delle dimostrazioni, ed estendiamo il primo alle potenze dei logaritmi.

- Dati $a \in \R_{>1}$ e $\beta \in \R_{>0}$, la funzione di variabile naturale asintoticamente crescente

    \begin{equation*}
    f: \N_{\ge 1} \rightarrow \R,~~~ f:n \mapsto \log^{\beta}_a n = \big(\log_a n\big)^{\beta} \tag{9.8}
    \end{equation*}

    è detta funzione <strong>polilogaritmica</strong> di variabile naturale.

<a id="box-5-grPropLogPower"></a>

!!! teorema "Proposizione 9.3: logaritmi e potenze"

    Per ogni $\alpha \in \R_{>0}$, $\beta \in \R_{>0}$ e $a \in \R_{>1}$, si ha:

    \begin{equation*}
    \lim_{n \rr \ip} \frac{\log_a^\beta n}{n^\alpha} = 0^+ \tag{9.9}
    \end{equation*}

??? dimostrazione "Dimostrazione"

    Per $\beta = 1$ questa è la gerarchia degli infiniti (parte I) del corso di <em>Analisi Matematica 1</em>:

    $$
    \lim_{n \rr \ip} \frac{\log_a n}{n^\alpha} = 0^+, \quad \forall \alpha \in \R_{>0},~ \forall a \in \R_{>1}.
    $$

    Si dimostra con la disuguaglianza $\log_a x < x \, \log_a 2$, valida per ogni $x \in \R_{>0}$ (conseguenza della disuguaglianza di Bernoulli), applicata a $x = n^{\alpha/2}$, e con il teorema del confronto.

    Per ogni $\beta \in \R_{>0}$, poiché $\frac{\alpha}{\beta} \in \R_{>0}$, si ha allora:

    $$
    \lim_{n \rr \ip} \frac{\log_a^\beta n}{n^\alpha}
    = \lim_{n \rr \ip} \Bigg( \underbrace{\frac{\log_a n}{n^{\alpha/\beta}}}_{\rr\, 0^+} \Bigg)^{\beta}
    = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-6-grPropPowerExp"></a>

!!! teorema "Proposizione 9.4: potenze ed esponenziali"

    Per ogni $\alpha \in \R_{>0}$ e $b \in \R_{>1}$, si ha:

    \begin{equation*}
    \lim_{n \rr \ip} \frac{n^{\alpha}}{b^{n}} = 0^+ \tag{9.10}
    \end{equation*}

- Questa è la gerarchia degli infiniti (parte II). Segue dalla [Proposizione 9.3](#box-5-grPropLogPower) sostituendo $n$ con $2^n$, il che dà $\frac{n}{(2^{\mu})^n} \rr 0^+$ per ogni $\mu \in \R_{>0}$, quindi $\frac{n}{b^n} \rr 0^+$ per ogni $b \in \R_{>1}$ (si sceglie $\mu$ tale che $2^{\mu} = b$); il caso generale segue dall'identità

    $$
    \frac{n^\alpha}{b^n} = \left( \frac{n}{\big(b^{1/\alpha}\big)^n} \right)^{\alpha}, \qquad b^{1/\alpha} \in \R_{>1}.
    $$

<a id="box-7-grPropExpFact"></a>

!!! teorema "Proposizione 9.5: esponenziali e fattoriale"

    Per ogni $b \in \R_{>1}$, si ha:

    \begin{equation*}
    \lim_{n \rr \ip} \frac{b^{n}}{n!} = 0^+ \tag{9.11}
    \end{equation*}

- Questa è la gerarchia degli infiniti (parte III). Segue dal criterio del rapporto, poiché

    $$
    \frac{b^{n+1}}{(n+1)!} \; \frac{n!}{b^n} = \frac{b}{n+1} \rr 0^+ < 1.
    $$

<a id="box-8-grPropFactSelf"></a>

!!! teorema "Proposizione 9.6: fattoriale e autopotenza"

    \begin{equation*}
    \lim_{n \rr \ip} \frac{n!}{n^n} = 0^+ \tag{9.12}
    \end{equation*}

- Questa è la gerarchia degli infiniti (parte IV). Segue dal criterio del rapporto, poiché

    $$
    \frac{(n+1)!}{(n+1)^{n+1}} \; \frac{n^n}{n!} = \left( \frac{n}{n+1}\right)^n = \frac{1}{\left( 1 + \frac{1}{n} \right)^n} \rr \frac{1}{e} < 1.
    $$

!!! chiave ""

    Le funzioni polilogaritmiche (con base maggiore di uno) divergono più lentamente delle funzioni potenza (con esponente positivo), che divergono più lentamente delle funzioni esponenziali (con base maggiore di uno), che divergono più lentamente della funzione fattoriale, che diverge più lentamente della funzione autopotenza.

## 9.3 Confronto fra ordini di crescita { #sez-gr-sec-comparison }

- L'<strong>ordine di crescita</strong> di una funzione di variabile naturale asintoticamente crescente descrive quanto rapidamente crescono i suoi valori rispetto ai valori di un'altra funzione di variabile naturale asintoticamente crescente.

- Per confrontare due funzioni $f$ e $g$ guardiamo il limite del loro rapporto $\frac{f(n)}{g(n)}$, che è definito per ogni $n$ abbastanza grande quando $f$ e $g$ sono asintoticamente positive.

<a id="box-9-grDefComparison"></a>

!!! definizione "Definizione 9.7: confronto fra ordini di crescita"

    Siano $f$ e $g$ due funzioni di variabile naturale asintoticamente positive tali che il limite

    $$
    L = \lim_{n \rr \ip} \frac{f(n)}{g(n)}
    $$

    esiste (finito oppure $\ip$). Diciamo che:

    - $f$ ha un <strong>ordine di crescita strettamente minore</strong> di quello di $g$, se $L = 0^+$;

    - $f$ ha un <strong>ordine di crescita minore o uguale</strong> a quello di $g$, se $L = 0^+$ oppure $L \in \R_{>0}$;

    - $f$ ha lo <strong>stesso ordine di crescita</strong> di $g$, se $L \in \R_{>0}$;

    - $f$ ha un <strong>ordine di crescita maggiore o uguale</strong> a quello di $g$, se $L \in \R_{>0}$ oppure $L = \ip$;

    - $f$ ha un <strong>ordine di crescita strettamente maggiore</strong> di quello di $g$, se $L = \ip$.

!!! chiave ""

    Date due funzioni di variabile naturale asintoticamente crescenti $f$ e $g$:

    - se $f$ ha un ordine di crescita strettamente minore di quello di $g$, $\rightsquigarrow$ la funzione $f$ <strong>cresce più lentamente</strong> della funzione $g$;

    - se $f$ ha un ordine di crescita minore o uguale a quello di $g$, $\rightsquigarrow$ la funzione $f$ <strong>cresce al più quanto</strong> la funzione $g$;

    - se $f$ ha lo stesso ordine di crescita di $g$, $\rightsquigarrow$ la funzione $f$ <strong>cresce come</strong> la funzione $g$;

    - se $f$ ha un ordine di crescita maggiore o uguale a quello di $g$, $\rightsquigarrow$ la funzione $f$ <strong>cresce almeno quanto</strong> la funzione $g$;

    - se $f$ ha un ordine di crescita strettamente maggiore di quello di $g$, $\rightsquigarrow$ la funzione $f$ <strong>cresce più velocemente</strong> della funzione $g$.

- Il confronto non dipende dai valori di $f$ e $g$ su un numero finito di numeri naturali: cambiarli non cambia il limite del rapporto.

- Il confronto è simmetrico, come afferma la seguente osservazione.

<a id="box-10-grObsSymmetry"></a>

!!! teorema "Osservazione 9.8: scambio delle due funzioni"

    Siano $f$ e $g$ due funzioni di variabile naturale asintoticamente positive. Allora:

    - $f$ ha un ordine di crescita strettamente minore di quello di $g$ se e solo se $g$ ha un ordine di crescita strettamente maggiore di quello di $f$;

    - $f$ ha lo stesso ordine di crescita di $g$ se e solo se $g$ ha lo stesso ordine di crescita di $f$.

??? dimostrazione "Dimostrazione"

    Per ogni $n$ abbastanza grande si ha $\frac{g(n)}{f(n)} = 1 \Big/ \frac{f(n)}{g(n)}$, con entrambi i rapporti positivi. Per il teorema sul limite del reciproco di una successione:

    $$
    \begin{aligned}
    \lim_{n \rr \ip} \frac{f(n)}{g(n)} = 0^+ \quad &\iff \quad \lim_{n \rr \ip} \frac{g(n)}{f(n)} = \ip\\[1ex]
    \lim_{n \rr \ip} \frac{f(n)}{g(n)} = \ell \in \R_{>0} \quad &\iff \quad \lim_{n \rr \ip} \frac{g(n)}{f(n)} = \frac{1}{\ell} \in \R_{>0}
    \end{aligned}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-11-gr-exRatios"></a>

!!! esempio "Esempio 9.2: il limite del rapporto"

    Confrontiamo tre coppie di funzioni; i tre rapporti sono disegnati in [Figura 9.2](#box-12-gr-figRatios).

    - La funzione $n \mapsto \ln n$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto \sqrt{n} = n^{1/2}$, poiché per la [Proposizione 9.3](#box-5-grPropLogPower) (con $a = e$, $\beta = 1$, $\alpha = \frac{1}{2}$):

        $$
        \lim_{n \rr \ip} \frac{\ln n}{\sqrt n} = 0^+
        $$

    - La funzione $n \mapsto 2n^2 + 3n$ ha lo stesso ordine di crescita della funzione $n \mapsto n^2$, poiché:

        $$
        \lim_{n \rr \ip} \frac{2n^2+3n}{n^2} = \lim_{n \rr \ip} \Big( 2 + \underbrace{\frac{3}{n}}_{\rr\, 0} \Big) = 2 \in \R_{>0}
        $$

    - La funzione $n \mapsto n \ln n$ ha un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto n$, poiché:

        $$
        \lim_{n \rr \ip} \frac{n \ln n}{n} = \lim_{n \rr \ip} \ln n = \ip
        $$

    Il primo rapporto non è monotono: cresce fino al suo valore massimo, circa $0.74$, raggiunto per $n = 7$, e solo dopo decresce verso $0$.

<a id="box-12-gr-figRatios"></a>

![Figura 2](../img/09-crescita-asintotica/fig02.svg){ .fig loading=lazy  }

<p class="didascalia"><strong>Figura 9.2:</strong> I tre rapporti dell'[Esempio 9.2](#box-11-gr-exRatios) per <span class="arithmatex">&#92;(n &#92;in &#92;{1, 2, &#92;dots, 100&#92;}&#92;)</span> (i punti sono uniti da segmenti). Il primo tende a <span class="arithmatex">&#92;(0&#92;)</span>, il secondo a <span class="arithmatex">&#92;(2&#92;)</span> (retta tratteggiata), il terzo diverge a <span class="arithmatex">&#92;(&#92;ip&#92;)</span>.</p>

- Il confronto della [Definizione 9.7](#box-9-grDefComparison) richiede che il limite del rapporto esista. Per esempio, per $f(n) = n$ se $n$ è pari e $f(n) = 2n$ se $n$ è dispari, il rapporto $\frac{f(n)}{n}$ assume alternativamente i valori $1$ e $2$ e non ha limite. Tutti i confronti di questo capitolo sono fatti fra funzioni il cui rapporto ha limite.

Quando due funzioni hanno lo stesso ordine di crescita, il rapporto dei loro valori resta, per ogni $n$ abbastanza grande, fra due costanti positive.

<a id="box-13-grObsBounds"></a>

!!! teorema "Osservazione 9.9: limitazioni sul rapporto"

    Siano $f$ e $g$ due funzioni di variabile naturale asintoticamente positive con lo stesso ordine di crescita, e sia $\ell = \lim_{n \rr \ip} \frac{f(n)}{g(n)} \in \R_{>0}$. Allora esistono $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che:

    \begin{equation*}
    0 < c_1 \, g(n) \le f(n) \le c_2 \, g(n), \quad \forall n \in \N_{\ge n_1} \tag{9.13}
    \end{equation*}

??? dimostrazione "Dimostrazione"

    Per la definizione di limite con $\varepsilon = \frac{\ell}{2} > 0$, esiste $n_1 \in \N$, che possiamo scegliere così grande che $f(n) > 0$ e $g(n) > 0$ per ogni $n \ge n_1$, tale che:

    $$
    \left| \frac{f(n)}{g(n)} - \ell \right| < \frac{\ell}{2}
    \quad \Longleftrightarrow \quad
    \frac{\ell}{2} < \frac{f(n)}{g(n)} < \frac{3\,\ell}{2},
    \quad \forall n \in \N_{\ge n_1}
    $$

    Moltiplicando per $g(n) > 0$, la tesi segue con $c_1 = \frac{\ell}{2}$ e $c_2 = \frac{3\,\ell}{2}$. <span class="qed">□</span>

- Di conseguenza, se due costanti $c_1, c_2 \in \R_{>0}$ come nell'[Osservazione 9.9](#box-13-grObsBounds) non esistono, allora $f$ e $g$ non hanno lo stesso ordine di crescita.

### 9.3.1 Gerarchia degli ordini di crescita { #sez-gr-sec-hierarchy }

I limiti della Sezione [9.2](#sez-gr-sec-limits) si traducono direttamente in confronti fra ordini di crescita.

- Ogni funzione polilogaritmica di variabile naturale con base strettamente maggiore di uno ha un ordine di crescita strettamente minore di quello di ogni funzione potenza di variabile naturale con esponente positivo.

<a id="box-14-grObsLogPower"></a>

!!! teorema "Osservazione 9.10: polilogaritmi e potenze"

    Per ogni $\alpha \in \R_{>0}$, $\beta \in \R_{>0}$ e $a \in \R_{>1}$, la funzione $n \mapsto \log^{\beta}_a n$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^{\alpha}$.

??? dimostrazione "Dimostrazione"

    Per la [Proposizione 9.3](#box-5-grPropLogPower), per ogni $\alpha \in \R_{>0}$, $\beta \in \R_{>0}$ e $a \in \R_{>1}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{\log^{\beta}_a n}{n^{\alpha}} = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Ogni funzione potenza di variabile naturale con esponente positivo ha un ordine di crescita strettamente minore di quello di ogni funzione esponenziale di variabile naturale con base strettamente maggiore di uno.

<a id="box-15-grObsPowerExp"></a>

!!! teorema "Osservazione 9.11: potenze ed esponenziali"

    Per ogni $\alpha \in \R_{>0}$ e $b \in \R_{>1}$, la funzione $n \mapsto n^{\alpha}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto b^{n}$.

??? dimostrazione "Dimostrazione"

    Per la [Proposizione 9.4](#box-6-grPropPowerExp), per ogni $\alpha \in \R_{>0}$ e $b \in \R_{>1}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{n^{\alpha}}{b^{n}} = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-16-gr-exCompare1"></a>

!!! esempio "Esempio 9.3: confronto fra ordini di crescita"

    - La funzione $n \mapsto \ln^6 n + 2 + 2^{1/n} + 3^{-n} + 9\,n^2$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^3$, poiché:

        $$
        \lim_{n \rr \ip} \frac{\ln^6 n + 2 + 2^{1/n} + 3^{-n} + 9\,n^2}{n^3}
        = \lim_{n \rr \ip} \Bigg( \underbrace{\frac{\ln^6 n}{n^3}}_{\rr\, 0^+} + \underbrace{\frac{2}{n^3}}_{\rr\, 0^+} + \underbrace{\frac{2^{1/n}}{n^3}}_{\rr\, 0^+} + \underbrace{\frac{3^{-n}}{n^3}}_{\rr\, 0^+} + \underbrace{\frac{9}{n}}_{\rr\, 0^+} \Bigg) = 0^+
        $$

    - La funzione $n \mapsto 3n^2 + \sqrt{n} + \ln n + 5 + 4^{-n} + 10\,n^{1/3}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^3$, poiché:

        $$
        \lim_{n \rr \ip} \frac{3n^2 + \sqrt{n} + \ln n + 5 + 4^{-n} + 10\,n^{1/3}}{n^3}
        = \lim_{n \rr \ip} \Bigg(
        \underbrace{\frac{3}{n}}_{\rr\, 0^+} +
        \underbrace{\frac{1}{n^{5/2}}}_{\rr\, 0^+} +
        \underbrace{\frac{\ln n}{n^3}}_{\rr\, 0^+} +
        \underbrace{\frac{5}{n^3}}_{\rr\, 0^+} +
        \underbrace{\frac{4^{-n}}{n^3}}_{\rr\, 0^+} +
        \underbrace{\frac{10}{n^{8/3}}}_{\rr\, 0^+}
        \Bigg) = 0^+
        $$

    - La funzione $n \mapsto n^{1/4} + \ln^2 n + \frac{7}{\sqrt{n}} + e^{-n} + 20\,n^{1/2}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^2$, poiché:

        $$
        \lim_{n \rr \ip} \frac{n^{1/4} + \ln^2 n + \frac{7}{\sqrt{n}} + e^{-n} + 20\,n^{1/2}}{n^2}
        = \lim_{n \rr \ip} \Bigg(
        \underbrace{\frac{1}{n^{7/4}}}_{\rr\, 0^+} +
        \underbrace{\frac{\ln^2 n}{n^2}}_{\rr\, 0^+} +
        \underbrace{\frac{7}{n^{5/2}}}_{\rr\, 0^+} +
        \underbrace{\frac{e^{-n}}{n^2}}_{\rr\, 0^+} +
        \underbrace{\frac{20}{n^{3/2}}}_{\rr\, 0^+}
        \Bigg) = 0^+
        $$

    In ciascun caso i termini con un logaritmo tendono a $0^+$ per l'[Osservazione 9.10](#box-14-grObsLogPower), e gli altri termini per limiti elementari.

- Ogni funzione esponenziale di variabile naturale con base strettamente maggiore di uno ha un ordine di crescita strettamente minore di quello della funzione fattoriale di variabile naturale.

<a id="box-17-grObsExpFact"></a>

!!! teorema "Osservazione 9.12: esponenziali e fattoriale"

    Per ogni $b \in \R_{>1}$, la funzione $n \mapsto b^{n}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n!$.

??? dimostrazione "Dimostrazione"

    Per la [Proposizione 9.5](#box-7-grPropExpFact), per ogni $b \in \R_{>1}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{b^{n}}{n!} = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- La funzione fattoriale di variabile naturale ha un ordine di crescita strettamente minore di quello della funzione autopotenza di variabile naturale.

<a id="box-18-grObsFactSelf"></a>

!!! teorema "Osservazione 9.13: fattoriale e autopotenza"

    La funzione $n \mapsto n!$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^n$.

??? dimostrazione "Dimostrazione"

    Per la [Proposizione 9.6](#box-8-grPropFactSelf), si ha:

    $$
    \lim_{n \rr \ip} \frac{n!}{n^n} = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

<a id="box-19-gr-exCompare2"></a>

!!! esempio "Esempio 9.4: confronto con la funzione autopotenza"

    La funzione $n \mapsto n! + 2^n + \sqrt{n} + \ln^3 n + n^{n-1} + \frac{1}{n}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^n$, poiché:

    $$
    \lim_{n \rr \ip} \frac{n! + 2^n + \sqrt{n} + \ln^3 n + n^{n-1} + \frac{1}{n}}{n^{n}}
    = \lim_{n \rr \ip} \Bigg(
    \underbrace{\frac{n!}{n^{n}}}_{\rr\, 0^+} +
    \underbrace{\frac{2^n}{n^{n}}}_{\rr\, 0^+} +
    \underbrace{\frac{\sqrt{n}}{n^{n}}}_{\rr\, 0^+} +
    \underbrace{\frac{\ln^3 n}{n^{n}}}_{\rr\, 0^+} +
    \underbrace{\frac{1}{n}}_{\rr\, 0^+} +
    \underbrace{\frac{1}{n^{n+1}}}_{\rr\, 0^+}
    \Bigg) = 0^+
    $$

    Per esempio, $\frac{2^n}{n^n} = \frac{2^n}{n!} \, \frac{n!}{n^n}$ è il prodotto di due funzioni che tendono a $0^+$, per le Proposizioni [9.5](#box-7-grPropExpFact) e [Proposizione 9.6](#box-8-grPropFactSelf).

!!! chiave ""

    <strong>Gerarchia degli ordini di crescita.</strong> Per ogni $a \in \R_{>1}$, $\beta \in \R_{>0}$, $\alpha \in \R_{>0}$ e $b \in \R_{>1}$, ogni funzione della catena

    $$
    \log_a^\beta n \qquad n^\alpha \qquad b^n \qquad n! \qquad n^n
    $$

    ha un ordine di crescita strettamente minore di quello della successiva.

### 9.3.2 Classificazione degli ordini di crescita { #sez-gr-sec-classification }

Le famiglie della gerarchia si usano come metri di paragone per classificare l'ordine di crescita di qualunque altra funzione.

<a id="box-20-grDefBounded"></a>

!!! definizione "Definizione 9.14: ordini di crescita limitati"

    Una funzione di variabile naturale asintoticamente crescente $f$ ha:

    - un <strong>ordine di crescita limitato polilogaritmicamente</strong>, se esiste $\beta \in \R_{>0}$ tale che $f$ ha un ordine di crescita minore o uguale a quello di $n \mapsto \ln^{\beta} n$; e un <strong>ordine di crescita limitato logaritmicamente</strong>, se ciò vale con $\beta = 1$;

    - un <strong>ordine di crescita limitato polinomialmente</strong>, se esiste $\alpha \in \R_{>0}$ tale che $f$ ha un ordine di crescita minore o uguale a quello di $n \mapsto n^{\alpha}$;

    - un <strong>ordine di crescita limitato esponenzialmente</strong>, se esiste $b \in \R_{>1}$ tale che $f$ ha un ordine di crescita minore o uguale a quello di $n \mapsto b^{n}$;

    - un <strong>ordine di crescita limitato fattorialmente</strong>, se $f$ ha un ordine di crescita minore o uguale a quello di $n \mapsto n!$.

<a id="box-21-grDefLinear"></a>

!!! definizione "Definizione 9.15: ordine di crescita lineare, sub-lineare e super-lineare"

    Una funzione di variabile naturale asintoticamente crescente $f$ ha:

    - un <strong>ordine di crescita sub-lineare</strong>, se $f$ ha un ordine di crescita strettamente minore di quello di $n \mapsto n$;

    - un <strong>ordine di crescita lineare</strong>, se $f$ ha lo stesso ordine di crescita di $n \mapsto n$;

    - un <strong>ordine di crescita super-lineare</strong>, se $f$ ha un ordine di crescita strettamente maggiore di quello di $n \mapsto n$.

- Per la gerarchia degli ordini di crescita, una funzione con ordine di crescita limitato polilogaritmicamente ha anche un ordine di crescita limitato polinomialmente, che a sua volta è anche limitato esponenzialmente e fattorialmente.

<a id="box-22-gr-exClassify"></a>

!!! esempio "Esempio 9.5: classificazione degli ordini di crescita"

    Classifichiamo quattro funzioni, disegnate in [Figura 9.3](#box-23-gr-figLinear).

    - $n \mapsto \sqrt n$ ha un ordine di crescita sub-lineare, poiché $\frac{\sqrt n}{n} = \frac{1}{\sqrt n} \rr 0^+$; ha un ordine di crescita limitato polinomialmente (con $\alpha = \frac{1}{2}$), ma non limitato polilogaritmicamente, poiché $\frac{\sqrt n}{\ln^{\beta} n} \rr \ip$ per ogni $\beta \in \R_{>0}$ ([Proposizione 9.3](#box-5-grPropLogPower) e [Osservazione 9.8](#box-10-grObsSymmetry)).

    - $n \mapsto n$ ha un ordine di crescita lineare.

    - $n \mapsto n \ln n$ ha un ordine di crescita super-lineare, poiché $\frac{n \ln n}{n} = \ln n \rr \ip$; ha un ordine di crescita limitato polinomialmente, poiché $\frac{n \ln n}{n^2} = \frac{\ln n}{n} \rr 0^+$.

    - $n \mapsto n^2$ ha un ordine di crescita super-lineare, poiché $\frac{n^2}{n} = n \rr \ip$; ha un ordine di crescita limitato polinomialmente (con $\alpha = 2$).

<a id="box-23-gr-figLinear"></a>

![Figura 3](../img/09-crescita-asintotica/fig03.svg){ .fig loading=lazy  }

<p class="didascalia"><strong>Figura 9.3:</strong> Una funzione sub-lineare (<span class="arithmatex">&#92;(&#92;sqrt n&#92;)</span>), la funzione lineare <span class="arithmatex">&#92;(n&#92;)</span> e due funzioni super-lineari (<span class="arithmatex">&#92;(n &#92;ln n&#92;)</span> e <span class="arithmatex">&#92;(n^2&#92;)</span>) per <span class="arithmatex">&#92;(n &#92;in &#92;{1, 2, &#92;dots, 16&#92;}&#92;)</span> (<span class="arithmatex">&#92;(n^2&#92;)</span> solo fino a <span class="arithmatex">&#92;(n = 8&#92;)</span>, dove raggiunge <span class="arithmatex">&#92;(64&#92;)</span>; i punti sono uniti da segmenti).</p>

### 9.3.3 Proprietà delle funzioni logaritmiche { #sez-gr-sec-log }

- Ogni funzione logaritmica di variabile naturale con base strettamente maggiore di uno ha lo stesso ordine di crescita di ogni altra funzione logaritmica di variabile naturale con base strettamente maggiore di uno; anche moltiplicare l'argomento per una costante positiva non cambia l'ordine di crescita.

<a id="box-24-grObsLogBase"></a>

!!! teorema "Osservazione 9.16: cambio di base"

    Per ogni $a \in \R_{>1}$, $c \in \R_{>1}$ e $\lambda \in \R_{>0}$, la funzione $n \mapsto \log_{a} (\lambda\, n)$ ha lo stesso ordine di crescita della funzione $n \mapsto \log_{c} n$.

??? dimostrazione "Dimostrazione"

    Per ogni $a,c \in \R_{>1}$ e $\lambda \in \R_{>0}$, poiché $\log_a (\lambda\, n) = \log_a \lambda + \log_a n$ e $\log_a n = \frac{\log_c n}{\log_c a}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{\log_{a}(\lambda\, n)}{\log_c n}
    = \lim_{n \rr \ip} \Bigg( \underbrace{\frac{\log_a \lambda}{\log_c n}}_{\rr\, 0} + \frac{\frac{\log_c n}{\log_c a}}{\log_c n} \Bigg)
    = \frac{1}{\log_c a} \in \R_{>0}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Per questo motivo, quando conta solo l'ordine di crescita, la base di un logaritmo si omette spesso. Per esempio, $\log_2 n$ e $\ln n$ hanno lo stesso ordine di crescita, e $\lim_{n \rr \ip} \frac{\log_2 n}{\ln n} = \frac{1}{\ln 2} \approx 1.44$.

- Sommare una costante positiva all'argomento di una funzione logaritmica di variabile naturale non ne cambia l'ordine di crescita.

<a id="box-25-grObsLogShift"></a>

!!! teorema "Osservazione 9.17: traslazione dell'argomento"

    Per ogni $a \in \R_{>1}$ e $\lambda \in \R_{>0}$, la funzione $n \mapsto \log_{a} (n+\lambda)$ ha lo stesso ordine di crescita della funzione $n \mapsto \log_{a} n$.

??? dimostrazione "Dimostrazione"

    Per ogni $a \in \R_{>1}$ e $\lambda \in \R_{>0}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{\log_a (n+\lambda)}{\log_a n}
    = \lim_{n \rr \ip} \frac{\log_a \left(n \left(1 + \frac{\lambda}{n} \right)\right)}{\log_a n}
    = \lim_{n \rr \ip} \frac{\log_a n + \overbrace{\log_a \left(1+\frac{\lambda}{n}\right)}^{\rr\, 0}}{\log_a n}
    = 1
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- La funzione <strong>quasi-lineare</strong> di variabile naturale $n \mapsto n \log_a n$ ha un ordine di crescita strettamente minore di quello di ogni funzione potenza di variabile naturale con esponente strettamente maggiore di uno.

<a id="box-26-grObsQuasiPower"></a>

!!! teorema "Osservazione 9.18: funzione quasi-lineare e potenze"

    Per ogni $\alpha \in \R_{>1}$ e $a \in \R_{>1}$, la funzione $n \mapsto n \log_a n$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto n^{\alpha}$.

??? dimostrazione "Dimostrazione"

    Per ogni $\alpha \in \R_{>1}$ e $a \in \R_{>1}$, si ha $\alpha - 1 \in \R_{>0}$ e, per la [Proposizione 9.3](#box-5-grPropLogPower):

    $$
    \lim_{n \rr \ip} \frac{n \log_a n}{n^{\alpha}} = \lim_{n \rr \ip} \frac{\log_a n}{n^{\alpha-1}} = 0^+
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- La funzione quasi-lineare di variabile naturale $n \mapsto n \log_a n$ ha un ordine di crescita strettamente maggiore di quello della funzione lineare di variabile naturale: ha un ordine di crescita super-lineare.

<a id="box-27-grObsQuasiLinear"></a>

!!! teorema "Osservazione 9.19: funzione quasi-lineare e funzione lineare"

    Per ogni $a \in \R_{>1}$, la funzione $n \mapsto n \log_a n$ ha un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto n$.

??? dimostrazione "Dimostrazione"

    Per ogni $a \in \R_{>1}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{n \log_a n}{n} = \lim_{n \rr \ip} \log_a n = \ip
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

### 9.3.4 Proprietà delle funzioni potenza { #sez-gr-sec-power }

- Sommare una costante positiva all'argomento di una funzione potenza di variabile naturale non ne cambia l'ordine di crescita.

<a id="box-28-grObsPowerShift"></a>

!!! teorema "Osservazione 9.20: traslazione dell'argomento"

    Per ogni $\alpha \in \R_{>0}$ e $\lambda \in \R_{>0}$, la funzione $n \mapsto (n+\lambda)^{\alpha}$ ha lo stesso ordine di crescita della funzione $n \mapsto n^{\alpha}$.

??? dimostrazione "Dimostrazione"

    Per ogni $\alpha \in \R_{>0}$ e $\lambda \in \R_{>0}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{(n+\lambda)^{\alpha}}{n^{\alpha}} = \lim_{n \rr \ip} \Big(1 + \underbrace{\frac{\lambda}{n}}_{\rr\, 0} \Big)^{\alpha} = 1
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Moltiplicare l'argomento di una funzione potenza di variabile naturale per una costante positiva non ne cambia l'ordine di crescita.

<a id="box-29-grObsPowerScale"></a>

!!! teorema "Osservazione 9.21: scalatura dell'argomento"

    Per ogni $\alpha \in \R_{>0}$ e $\lambda \in \R_{>0}$, la funzione $n \mapsto (\lambda\, n)^{\alpha}$ ha lo stesso ordine di crescita della funzione $n \mapsto n^{\alpha}$.

??? dimostrazione "Dimostrazione"

    Per ogni $\alpha \in \R_{>0}$ e $\lambda \in \R_{>0}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{(\lambda\, n)^{\alpha}}{n^{\alpha}} = \lim_{n \rr \ip} \frac{\lambda^{\alpha}\, n^{\alpha}}{n^{\alpha}} = \lambda^{\alpha} \in \R_{>0}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- L'ordine di crescita di una funzione potenza di variabile naturale, confrontato con quello della funzione lineare di variabile naturale, dipende dal fatto che l'esponente sia maggiore o minore di uno.

<a id="box-30-grObsPowerLinear"></a>

!!! teorema "Osservazione 9.22: potenze e funzione lineare"

    Per ogni $\alpha \in \R_{>0}$, la funzione $n \mapsto n^{\alpha}$ ha:

    - un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto n$ (ordine di crescita super-lineare), se $\alpha > 1$;

    - un ordine di crescita strettamente minore di quello della funzione $n \mapsto n$ (ordine di crescita sub-lineare), se $\alpha < 1$.

??? dimostrazione "Dimostrazione"

    Per ogni $\alpha \in \R_{>0}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{n^{\alpha}}{n} = \lim_{n \rr \ip} n^{\alpha - 1} =
    \begin{cases}
    \ip & \text{se} ~~~ \alpha > 1\\[1ex]
    0^+ & \text{se} ~~~ \alpha < 1
    \end{cases}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

### 9.3.5 Proprietà delle funzioni polinomiali { #sez-gr-sec-poly }

- Ogni funzione polinomiale di variabile naturale con coefficiente direttivo positivo ha lo stesso ordine di crescita del suo termine di grado massimo.

<a id="box-31-grObsPoly"></a>

!!! teorema "Osservazione 9.23: polinomi"

    Per ogni $k \in \N_{\ge 1}$ e ogni $a_0, a_1, \dots, a_k \in \R$ con $a_k \in \R_{>0}$, la funzione $n \mapsto \sum_{i=0}^{k} a_i \, n^i$ ha lo stesso ordine di crescita della funzione $n \mapsto n^k$.

??? dimostrazione "Dimostrazione"

    Si ha:

    $$
    \lim_{n \rr \ip} \frac{\sum_{i=0}^{k} a_i \, n^i}{n^{k}} = a_k + \lim_{n \rr \ip} \sum_{i=0}^{k-1} \underbrace{\frac{a_i}{n^{k-i}}}_{\rr\, 0} = a_k \in \R_{>0}
    $$

    In particolare, il polinomio è asintoticamente positivo, quindi si applica il confronto della [Definizione 9.7](#box-9-grDefComparison). <span class="qed">□</span>

### 9.3.6 Proprietà delle funzioni esponenziali { #sez-gr-sec-exp }

- Ogni funzione esponenziale di variabile naturale con base strettamente maggiore di uno ha un ordine di crescita strettamente maggiore di quello delle funzioni esponenziali di variabile naturale con base minore, e strettamente minore di quello delle funzioni esponenziali di variabile naturale con base maggiore.

<a id="box-32-grObsExpBase"></a>

!!! teorema "Osservazione 9.24: basi diverse"

    Per ogni $b \in \R_{>1}$ e $c \in \R_{>1}$, la funzione $n \mapsto b^n$ ha:

    - un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto c^n$, se $b > c$;

    - un ordine di crescita strettamente minore di quello della funzione $n \mapsto c^n$, se $b < c$.

??? dimostrazione "Dimostrazione"

    Per ogni $b \in \R_{>1}$ e $c \in \R_{>1}$, poiché $b = c^{\log_c b}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{b^n}{c^n} = \lim_{n \rr \ip} \frac{c^{n \log_c b}}{c^n} = \lim_{n \rr \ip} \Big(c^{\log_c b-1}\Big)^{n} =
    \begin{cases}
    \ip & \text{se} ~~~ b > c\\[1ex]
    0^+ & \text{se} ~~~ b < c
    \end{cases}
    $$

    poiché $c^{\log_c b - 1} = \frac{b}{c}$ è maggiore di uno se $b > c$ e appartiene a $(0,1)$ se $b < c$ (limite della progressione geometrica). <span class="qed">□</span>

- Moltiplicare l'esponente di una funzione esponenziale di variabile naturale per una costante positiva ne cambia l'ordine di crescita, a meno che la costante sia uguale a uno.

<a id="box-33-grObsExpScale"></a>

!!! teorema "Osservazione 9.25: scalatura dell'esponente"

    Per ogni $b \in \R_{>1}$ e $\lambda \in \R_{>0}$, la funzione $n \mapsto b^{\lambda n}$ ha:

    - un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto b^n$, se $\lambda > 1$;

    - un ordine di crescita strettamente minore di quello della funzione $n \mapsto b^n$, se $0 < \lambda < 1$.

??? dimostrazione "Dimostrazione"

    Per ogni $b \in \R_{>1}$ e $\lambda \in \R_{>0}$, si ha:

    $$
    \lim_{n \rr \ip} \frac{b^{\lambda n}}{b^n}
    = \lim_{n \rr \ip} \left(\frac{b^{\lambda}}{b}\right)^n
    = \lim_{n \rr \ip} \left(b^{\lambda-1}\right)^n
    =
    \begin{cases}
    \ip & \text{se} ~~~ \lambda > 1\\[1ex]
    0^+ & \text{se} ~~~ 0 < \lambda < 1
    \end{cases}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Una dimostrazione alternativa si basa sul fatto che

    $$
    b^{\lambda n} = \big( b^{\lambda} \big)^n
    \qquad \text{e} \qquad
    b^{\lambda}
    \begin{cases}
    > b & \text{se} ~~~ \lambda > 1\\[1ex]
    < b & \text{se} ~~~ 0 < \lambda < 1
    \end{cases}
    $$

    Di conseguenza, per l'[Osservazione 9.24](#box-32-grObsExpBase) applicata alle basi $b^{\lambda}$ e $b$, la funzione $n \mapsto b^{\lambda n}$ ha un ordine di crescita strettamente maggiore di $n \mapsto b^n$ se $\lambda > 1$, e strettamente minore se $0 < \lambda < 1$.

<a id="box-34-gr-exExpScale"></a>

!!! esempio "Esempio 9.6: scalatura dell'esponente"

    - La funzione $n \mapsto 2^{n/2}$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto 2^n$, poiché

        $$
        2^{n/2} = \big(2^{1/2}\big)^{n} \qquad \text{e} \qquad 2^{1/2} = \sqrt 2 < 2.
        $$

    - La funzione $n \mapsto 2^{3n/2}$ ha un ordine di crescita strettamente maggiore di quello della funzione $n \mapsto 2^n$, poiché

        $$
        2^{3n/2} = \big(2^{3/2}\big)^{n} \qquad \text{e} \qquad 2^{3/2} = 2\sqrt 2 > 2.
        $$

- Traslare l'esponente di una funzione esponenziale di variabile naturale di una costante non ne cambia l'ordine di crescita.

<a id="box-35-grObsExpShift"></a>

!!! teorema "Osservazione 9.26: traslazione dell'esponente"

    Per ogni $b \in \R_{>1}$ e $\lambda \in \R$, la funzione $n \mapsto b^{n+\lambda}$ ha lo stesso ordine di crescita della funzione $n \mapsto b^{n}$.

??? dimostrazione "Dimostrazione"

    Per ogni $b \in \R_{>1}$ e $\lambda \in \R$, si ha:

    $$
    \lim_{n \rr \ip} \frac{b^{n+\lambda}}{b^n} = \lim_{n \rr \ip} \frac{b^{n}\, b^{\lambda}}{b^n} = b^{\lambda} \in \R_{>0}
    $$

    <p class="qed-riga"><span class="qed">□</span></p>

- Per esempio, $2^{n+10} = 1024 \cdot 2^n$ ha lo stesso ordine di crescita di $2^n$, mentre $2^{2n} = 4^n$ ha un ordine di crescita strettamente maggiore: una costante sommata all'esponente è un fattore costante, un fattore costante nell'esponente cambia la base.

!!! chiave ""

    <strong>Punti chiave del capitolo</strong>

    - Le funzioni di variabile naturale usate nell'analisi degli algoritmi sono le funzioni logaritmiche ($\log_a n$), potenza ($n^\alpha$), esponenziali ($b^n$), fattoriale ($n!$) e autopotenza ($n^n$), insieme alle loro somme e ai loro prodotti.

    - L'ordine di crescita di $f$ si confronta con quello di $g$ attraverso il limite di $\frac{f(n)}{g(n)}$: $0^+$ (strettamente minore), un numero reale positivo (stesso ordine di crescita), $\ip$ (strettamente maggiore).

    - Gerarchia: $\log_a^\beta n$, $n^\alpha$, $b^n$, $n!$, $n^n$ (con $a, b > 1$ e $\alpha, \beta > 0$), ciascuna con un ordine di crescita strettamente minore di quello della successiva.

    - La base di un logaritmo, una costante sommata all'argomento di un logaritmo o di una potenza, un fattore costante nell'argomento di una potenza e una costante sommata all'esponente di un esponenziale non cambiano l'ordine di crescita; un polinomio ha l'ordine di crescita del suo termine di grado massimo.

    - Un fattore costante nell'esponente di un esponenziale, e una base diversa di un esponenziale, cambiano invece l'ordine di crescita.

    - Una funzione ha un ordine di crescita sub-lineare, lineare o super-lineare se cresce più lentamente di, come, o più velocemente di $n$; per esempio $\sqrt n$, $5n+3$ e $n \ln n$ sono rispettivamente sub-lineare, lineare e super-lineare.

<!-- laboratorio-interattivo: sezione generata da interattivi.py -->

## Laboratorio interattivo { #laboratorio-interattivo }

L'algoritmo del capitolo, un passo alla volta: muovi i cursori e premi ▶.
Tutti i grafici del corso sono nel [laboratorio interattivo](../laboratorio/index.md#cap-9).

<div class="gi" data-grafico="crescita"></div>
