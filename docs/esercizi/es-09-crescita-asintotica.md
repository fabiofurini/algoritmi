---
title: "Esercizi · Crescita asintotica"
---

# Esercizi · Crescita asintotica

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 9** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 9](../notazione-asintotica/09-crescita-asintotica.md) · [:material-file-pdf-box: Eserciziario, volume 3 (PDF)](../pdf/esercizi-3-notazione-asintotica.pdf)

</div>

Negli esercizi di questo capitolo gli ordini di crescita si confrontano con le definizioni e i risultati del capitolo «Crescita asintotica», riassunti qui sotto. I limiti di funzioni di variabile naturale (successioni) si calcolano con i risultati del corso di <em>Analisi Matematica 1</em> ([fabiofurini.github.io/analisi-matematica-1/](https://fabiofurini.github.io/analisi-matematica-1/)).

!!! nota ""

    Date due funzioni di variabile naturale asintoticamente positive $f$ e $g$ tali che il limite $L = \lim_{n \rr \ip} \frac{f(n)}{g(n)}$ esista:

    - se $L = 0^+$, $f$ ha un <strong>ordine di crescita strettamente minore</strong> di quello di $g$ ($f$ cresce più lentamente di $g$);

    - se $L = 0^+$ oppure $L \in \R_{>0}$, $f$ ha un <strong>ordine di crescita minore o uguale</strong> a quello di $g$;

    - se $L \in \R_{>0}$, $f$ ha lo <strong>stesso ordine di crescita</strong> di $g$ ($f$ cresce come $g$);

    - se $L \in \R_{>0}$ oppure $L = \ip$, $f$ ha un <strong>ordine di crescita maggiore o uguale</strong> a quello di $g$;

    - se $L = \ip$, $f$ ha un <strong>ordine di crescita strettamente maggiore</strong> di quello di $g$ ($f$ cresce più velocemente di $g$).

!!! nota ""

    - <strong>Limitazioni sul rapporto.</strong> Se $f$ e $g$ hanno lo stesso ordine di crescita, esistono $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 < c_1 \, g(n) \le f(n) \le c_2 \, g(n), \quad \forall n \in \N_{\ge n_1}.
        $$

        Di conseguenza, se tali costanti non esistono, $f$ e $g$ non hanno lo stesso ordine di crescita.

    - <strong>Gerarchia.</strong> Per ogni $a, b \in \R_{>1}$ e $\alpha, \beta \in \R_{>0}$, ogni funzione della catena

        $$
        \log_a^\beta n \qquad n^\alpha \qquad b^n \qquad n! \qquad n^n
        $$

        ha un ordine di crescita strettamente minore di quello della successiva.

<a id="esercizio-9-1"></a>

!!! esercizio "Esercizio 9.1: Crescita asintotica (E1)"

    Dati $\lambda \in \R_{>0}$ e $\alpha \in \R_{>0}$, consideriamo la seguente funzione di variabile naturale asintoticamente positiva:

    $$
    f: \N \rightarrow \R, ~~f: n \mapsto (n+\lambda)^{\alpha}
    $$

    !!! chiave ""

        Dati $b \in \R_{>1}$ e $\lambda \in \R_{>0}$, consideriamo la seguente funzione di variabile naturale asintoticamente positiva:

        $$
        f: \N \rightarrow \R, ~~f: n \mapsto b^{\lambda n}
        $$

    !!! chiave ""

        Dato $a \in \R_{>1}$, consideriamo la seguente funzione di variabile naturale asintoticamente positiva:

        $$
        f: \N_{\ge 1} \rightarrow \R, ~~f: n \mapsto n \log_a n
        $$

    **Domande**

    1. Dimostrare che esistono $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \, n^{\alpha} \le (n+\lambda)^{\alpha} \le c_2 \, n^{\alpha}, \quad \forall n \in \N_{\ge n_1},
        $$

        e verificare, calcolando il limite del rapporto, che la funzione $n \mapsto (n+\lambda)^{\alpha}$ e la funzione $n \mapsto n^{\alpha}$ hanno lo stesso ordine di crescita.

    2. Dimostrare che, per ogni $\lambda \in \R_{>0}$ con $\lambda \neq 1$, non esistono $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \, b^{n} \le b^{\lambda n} \le c_2 \, b^{n}, \quad \forall n \in \N_{\ge n_1},
        $$

        e di conseguenza che la funzione $n \mapsto b^{\lambda n}$ e la funzione $n \mapsto b^{n}$ non hanno lo stesso ordine di crescita.

    3. Dimostrare che, per ogni $\alpha \in \R_{>1}$, non esistono $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N_{\ge 1}$ tali che

        $$
        0 \le c_1 \, n^{\alpha} \le n \log_a n \le c_2 \, n^{\alpha}, \quad \forall n \in \N_{\ge n_1},
        $$

        e di conseguenza che la funzione $n \mapsto n \log_a n$ e la funzione $n \mapsto n^{\alpha}$ non hanno lo stesso ordine di crescita.

??? soluzione "Soluzione"

    1. Cerchiamo costanti $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \, n^{\alpha} \le (n+\lambda)^{\alpha} \le c_2 \, n^{\alpha}, \quad \forall n \in \N_{\ge n_1}.
        $$

        Poiché $\lambda > 0$, si ha

        $$
        0 \le \frac{n}{2} \le n + \lambda \quad \forall n \in \N
        \qquad\text{e}\qquad
        n + \lambda \le 2\, n \quad \text{se } n \ge \lambda,
        $$

        così che, per ogni $n \ge 2\lambda$ (il che implica $n \ge \lambda$), si ha:

        $$
        0 \le \frac{n}{2} \le n + \lambda \le 2\,n
        $$

        Poiché $\alpha > 0$, la funzione $x \mapsto x^\alpha$ è crescente su $\R_{\ge 0}$, e possiamo elevare i tre termini alla potenza $\alpha$ senza cambiare le disuguaglianze:

        $$
        \left(\frac{n}{2}\right)^{\alpha} \le (n+\lambda)^{\alpha} \le (2\,n)^{\alpha}
        \quad \Longleftrightarrow \quad
        \frac{1}{2^{\alpha}}\, n^{\alpha} \le (n+\lambda)^{\alpha} \le 2^{\alpha}\, n^{\alpha}
        $$

        Dunque, scegliendo per esempio $c_1 = \frac{1}{2^{\alpha}} > 0$, $c_2 = 2^{\alpha} > 0$ e $n_1 = \lceil 2\lambda \rceil \ge 1$, si ha:

        $$
        0 \le \frac{1}{2^{\alpha}}\, n^{\alpha} \le (n+\lambda)^{\alpha} \le 2^{\alpha}\, n^{\alpha}, \quad \forall n \in \N_{\ge \lceil 2\lambda \rceil}
        $$

        Queste limitazioni da sole non danno il limite del rapporto, che calcoliamo direttamente:

        $$
        \lim_{n \rr \ip} \frac{(n+\lambda)^{\alpha}}{n^{\alpha}} = \lim_{n \rr \ip} \Big(1 + \underbrace{\frac{\lambda}{n}}_{\rr\, 0}\Big)^{\alpha} = 1 \in \R_{>0}
        $$

        Quindi le due funzioni hanno lo stesso ordine di crescita.

    2. Procediamo per assurdo, e supponiamo che esistano $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \, b^{n} \le b^{\lambda n} \le c_2 \, b^{n}, \quad \forall n \in \N_{\ge n_1}.
        $$

        Poiché $b^n > 0$ per ogni $n \in \N$ (essendo $b \in \R_{>1}$), dividendo per $b^n$ otteniamo le disuguaglianze equivalenti

        $$
        0 < c_1 \le \underbrace{\frac{b^{\lambda n}}{b^n}}_{=\left(\frac{b^{\lambda}}{b}\right)^n = \left(b^{\lambda-1}\right)^n} \le c_2, \quad \forall n \in \N_{\ge n_1},
        $$

        che non possono valere per $n$ arbitrariamente grande, poiché $c_1$ e $c_2$ sono costanti positive e:

        - se $\lambda > 1$, allora $b^{\lambda - 1} > 1$ e $\lim_{n \rr \ip} \left(b^{\lambda-1}\right)^n = \ip$, quindi la disuguaglianza di destra è violata per $n$ abbastanza grande;

        - se $0 < \lambda < 1$, allora $0 < b^{\lambda - 1} < 1$ e $\lim_{n \rr \ip} \left(b^{\lambda-1}\right)^n = 0^+$, quindi la disuguaglianza di sinistra è violata per $n$ abbastanza grande.

        Ne segue che, per ogni $b \in \R_{>1}$ e ogni $\lambda \in \R_{>0}$ con $\lambda \neq 1$, la funzione $n \mapsto b^{\lambda n}$ e la funzione $n \mapsto b^{n}$ non hanno lo stesso ordine di crescita (altrimenti varrebbero le limitazioni sul rapporto).

    3. Procediamo per assurdo, e supponiamo che esistano $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N_{\ge 1}$ tali che

        $$
        0 \le c_1 \, n^{\alpha} \le n \log_a n \le c_2 \, n^{\alpha}, \quad \forall n \in \N_{\ge n_1}.
        $$

        Poiché $n^{\alpha} > 0$ per ogni $n \in \N_{\ge 1}$, dividendo per $n^{\alpha}$ otteniamo le disuguaglianze equivalenti

        $$
        0 < c_1 \le \underbrace{\frac{n \log_a n}{n^{\alpha}}}_{= \frac{\log_a n}{n^{\alpha-1}}} \le c_2, \quad \forall n \in \N_{\ge n_1},
        $$

        che non possono valere per $n$ arbitrariamente grande, poiché $c_1$ è una costante positiva e, per la gerarchia degli ordini di crescita (essendo $a > 1$ e $\alpha - 1 > 0$):

        $$
        \lim_{n \rr \ip} \frac{\log_a n}{n^{\alpha-1}} = 0^+
        $$

        Ne segue che, per ogni $\alpha \in \R_{>1}$ e ogni $a \in \R_{>1}$, la funzione $n \mapsto n \log_a n$ e la funzione $n \mapsto n^{\alpha}$ non hanno lo stesso ordine di crescita: lo stesso limite mostra che $n \mapsto n \log_a n$ ha un ordine di crescita strettamente minore.

<a id="esercizio-9-2"></a>

!!! esercizio "Esercizio 9.2: Crescita asintotica (E2)"

    Consideriamo la seguente funzione di variabile naturale:

    $$
    f: \N_{\ge 2} \rightarrow \R, ~~f: n \mapsto \ln\big(\ln n\big)
    $$

    **Domande**

    1. Dimostrare che la funzione $f$ è asintoticamente positiva e asintoticamente crescente.

    2. Dimostrare che la funzione $n \mapsto \ln(\ln n)$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto \ln n$.

??? soluzione "Soluzione"

    1. La funzione $x \mapsto \ln x$ è strettamente crescente su $\R_{>0}$, quindi $n \mapsto \ln(\ln n)$ è strettamente crescente su $\N_{\ge 2}$. Non è positiva su tutto il dominio, poiché $\ln 2 < 1$ e quindi $f(2) = \ln(\ln 2) < 0$; ma $\ln 3 > 1$, dunque

        $$
        f(n) = \ln(\ln n) \ge \ln(\ln 3) > 0, \quad \forall n \in \N_{\ge 3}.
        $$

        La funzione $f$ è quindi asintoticamente positiva (con $n_1 = 3$) e asintoticamente crescente.

    2. Entrambe le funzioni sono positive per ogni $n \in \N_{\ge 3}$. Calcoliamo il limite del rapporto estendendo il dominio ai numeri reali, cioè calcolando il limite della funzione di variabile reale $x \mapsto \frac{\ln(\ln x)}{\ln x}$ per $x \rr \ip$: se questo limite esiste, il limite della funzione di variabile naturale è lo stesso. Poiché sia il numeratore sia il denominatore tendono a $\ip$, possiamo usare il teorema di De l'Hospital (corso di <em>Analisi Matematica 1</em>, capitolo <em>Teorema di De l'Hospital e derivabilità</em>):

        $$
        \lim_{x \rr \ip} \frac{\ln\big(\ln x\big)}{\ln x} = \lim_{x \rr \ip} \frac{\frac{d}{dx}\left[\ln\big(\ln x\big)\right]}{\frac{d}{dx}\left[\ln x\right]}
        $$

        La derivata del numeratore è

        $$
        \frac{d}{dx}\left[\ln\big(\ln x\big)\right] = \frac{1}{\ln x} \cdot \frac{1}{x} = \frac{1}{x \ln x},
        $$

        e la derivata del denominatore è

        $$
        \frac{d}{dx}\left[\ln x\right] = \frac{1}{x}.
        $$

        Sostituendo, si ha:

        $$
        \lim_{x \rr \ip} \frac{\ln\big(\ln x\big)}{\ln x} = \lim_{x \rr \ip} \frac{\frac{1}{x \ln x}}{\frac{1}{x}} = \lim_{x \rr \ip} \frac{1}{\ln x} = 0^+
        $$

        Ne segue che

        $$
        \lim_{n \rr \ip} \frac{\ln\big(\ln n\big)}{\ln n} = 0^+,
        $$

        cioè la funzione $n \mapsto \ln(\ln n)$ ha un ordine di crescita strettamente minore di quello della funzione $n \mapsto \ln n$.

<a id="esercizio-9-3"></a>

!!! esercizio "Esercizio 9.3: Crescita asintotica (E3)"

    Consideriamo le seguenti dodici funzioni di variabile naturale, definite per $n \in \N_{\ge 1}$:

    $$
    \begin{array}{llll}
    f_1(n) = \log_2\big(n^5\big) & f_2(n) = \ln^3 n & f_3(n) = \sqrt n & f_4(n) = n \ln n \\[1ex]
    f_5(n) = (n+7)^2 & f_6(n) = 3n^2 + 100\,n & f_7(n) = n^{10} & f_8(n) = 2^{n/2} \\[1ex]
    f_9(n) = 2^{n+10} & f_{10}(n) = 3^n & f_{11}(n) = n! & f_{12}(n) = n^n
    \end{array}
    $$

    **Domande**

    1. Ordinare le dodici funzioni per ordine di crescita crescente, raggruppando le funzioni che hanno lo stesso ordine di crescita. Giustificare ogni confronto fra due gruppi consecutivi con i risultati del capitolo «Crescita asintotica».

    2. Classificare ogni funzione: ha un ordine di crescita sub-lineare, lineare o super-lineare? Quali funzioni hanno un ordine di crescita limitato polilogaritmicamente, e quali un ordine di crescita limitato polinomialmente?

    3. L'ordine di crescita descrive il comportamento delle funzioni per valori grandi di $n$. Verificare che $f_2(4) > f_3(4)$ e che $f_7(n) > f_8(n)$ per $n = 100$, e spiegare perché ciò non contraddice la risposta alla prima domanda.

??? soluzione "Soluzione"

    1. L'ordine è il seguente (le funzioni dello stesso gruppo hanno lo stesso ordine di crescita):

        $$
        f_1 \;\prec\; f_2 \;\prec\; f_3 \;\prec\; f_4 \;\prec\; \{f_5, f_6\} \;\prec\; f_7 \;\prec\; f_8 \;\prec\; f_9 \;\prec\; f_{10} \;\prec\; f_{11} \;\prec\; f_{12}
        $$

        dove qui $f \prec g$ è un'abbreviazione di «$f$ ha un ordine di crescita strettamente minore di quello di $g$». Le giustificazioni sono le seguenti.

        - $f_1(n) = \log_2(n^5) = 5\log_2 n$, che ha lo stesso ordine di crescita di $\ln n$ (cambio di base). Inoltre $\frac{f_1(n)}{f_2(n)} = \frac{5 \log_2 n}{\ln^3 n} = \frac{5}{\ln 2} \cdot \frac{1}{\ln^2 n} \rr 0^+$, quindi $f_1 \prec f_2$.

        - $f_2 \prec f_3$: polilogaritmi e potenze, con $\beta = 3$ e $\alpha = \frac{1}{2}$.

        - $f_3 \prec f_4$: $\frac{\sqrt n}{n \ln n} = \frac{1}{\sqrt n \, \ln n} \rr 0^+$.

        - $f_4 \prec f_5$: per la proprietà della funzione quasi-lineare e delle potenze (con $\alpha = 2$) e per la traslazione dell'argomento di una potenza,

            $$
            \frac{n \ln n}{(n+7)^2} = \underbrace{\frac{n \ln n}{n^2}}_{\rr\, 0^+} \cdot \underbrace{\frac{n^2}{(n+7)^2}}_{\rr\, 1} \rr 0^+.
            $$

        - $f_5$ e $f_6$ hanno lo stesso ordine di crescita: entrambe hanno lo stesso ordine di crescita di $n^2$ (traslazione dell'argomento; polinomio con termine di grado massimo $3n^2$), e infatti

            $$
            \lim_{n \rr \ip} \frac{(n+7)^2}{3n^2+100\,n} = \lim_{n \rr \ip} \frac{1 + \frac{14}{n} + \frac{49}{n^2}}{3 + \frac{100}{n}} = \frac{1}{3} \in \R_{>0}.
            $$

        - $f_6 \prec f_7$: $\frac{3n^2+100\,n}{n^{10}} = \frac{3}{n^8} + \frac{100}{n^9} \rr 0^+$.

        - $f_7 \prec f_8$: potenze ed esponenziali, poiché $2^{n/2} = \big(\sqrt 2\big)^n$ con base $\sqrt 2 > 1$.

        - $f_8 \prec f_9$: $f_9(n) = 2^{n+10}$ ha lo stesso ordine di crescita di $2^n$ (traslazione dell'esponente), e $2^{n/2}$ ha un ordine di crescita strettamente minore di quello di $2^n$ (scalatura dell'esponente con $\lambda = \frac{1}{2}$); direttamente,

            $$
            \frac{2^{n/2}}{2^{n+10}} = \frac{1}{1024} \left(\frac{1}{\sqrt 2}\right)^{n} \rr 0^+.
            $$

        - $f_9 \prec f_{10}$: $\frac{2^{n+10}}{3^n} = 1024 \left(\frac{2}{3}\right)^n \rr 0^+$ (basi diverse).

        - $f_{10} \prec f_{11} \prec f_{12}$: esponenziali e fattoriale, fattoriale e autopotenza.

    2. Confrontando ogni funzione con $n$:

        - $f_1$, $f_2$ e $f_3$ hanno un ordine di crescita sub-lineare ($f_1 \prec f_2 \prec f_3$ e $\frac{\sqrt n}{n} \rr 0^+$);

        - nessuna funzione dell'elenco ha un ordine di crescita lineare;

        - $f_4, f_5, \dots, f_{12}$ hanno un ordine di crescita super-lineare ($f_4$ è quasi-lineare, e tutte le altre crescono più velocemente di $f_4$).

        Le funzioni $f_1$ (limitata logaritmicamente, con $\beta = 1$) e $f_2$ (con $\beta = 3$) hanno un ordine di crescita limitato polilogaritmicamente; $f_3$ no, poiché cresce più velocemente di ogni funzione polilogaritmica. Le funzioni $f_1, f_2, \dots, f_7$ hanno un ordine di crescita limitato polinomialmente (per esempio $f_4$ con $\alpha = 2$, e $f_7$ con $\alpha = 10$); le funzioni $f_8, f_9, \dots, f_{12}$ no, poiché crescono più velocemente di ogni funzione potenza. Fra queste, $f_8$, $f_9$ e $f_{10}$ hanno un ordine di crescita limitato esponenzialmente.

    3. Per $n = 4$ si ha

        $$
        f_2(4) = \ln^3 4 \approx 2.66 > 2 = \sqrt 4 = f_3(4),
        $$

        e per $n = 100$ si ha

        $$
        f_7(100) = 100^{10} = 10^{20} > 2^{50} \approx 1.1 \cdot 10^{15} = f_8(100).
        $$

        Ciò non contraddice la prima risposta: il confronto fra gli ordini di crescita riguarda il limite del rapporto, cioè il comportamento per $n$ grande. La disuguaglianza $\ln^3 n \ge \sqrt n$ vale per ogni $n$ da $4$ a $24{,}128{,}091$, e $\ln^3 n < \sqrt n$ per ogni $n \ge 24{,}128{,}092$; analogamente, $n^{10} \ge 2^{n/2}$ vale per ogni $n$ da $2$ a $143$, e $n^{10} < 2^{n/2}$ per ogni $n \ge 144$. Queste soglie sono state calcolate numericamente.

<a id="esercizio-9-4"></a>

!!! esercizio "Esercizio 9.4: Crescita asintotica (E4)"

    Consideriamo le seguenti coppie di funzioni di variabile naturale $(f, g)$, definite per $n \in \N_{\ge 1}$:

    $$
    \begin{array}{lll}
    \text{(a)}~~ f(n) = 2^{n/2}, & g(n) = 2^n; & \qquad \text{(b)}~~ f(n) = 2^{3n/2}, ~~ g(n) = 2^n; \\[1ex]
    \text{(c)}~~ f(n) = 4^n, & g(n) = 2^{2n}; & \qquad \text{(d)}~~ f(n) = \log_2 n, ~~ g(n) = \log_{10} n; \\[1ex]
    \text{(e)}~~ f(n) = \ln\big(n^2+1\big), & g(n) = \ln n; & \qquad \text{(f)}~~ f(n) = n \ln n, ~~ g(n) = n^{3/2}.
    \end{array}
    $$

    **Domande**

    1. Per ogni coppia, calcolare $\lim_{n \rr \ip} \frac{f(n)}{g(n)}$ (per la coppia (d), considerare $n \in \N_{\ge 2}$, dove $g(n) > 0$) e stabilire se $f$ ha un ordine di crescita strettamente minore, uguale o strettamente maggiore di quello di $g$.

    2. Per ogni coppia, indicare, quando è possibile, quale proprietà del capitolo «Crescita asintotica» dà la stessa risposta senza calcolare il limite.

??? soluzione "Soluzione"

    1. I limiti sono i seguenti.

        - **(a)** $\displaystyle \lim_{n \rr \ip} \frac{2^{n/2}}{2^n} = \lim_{n \rr \ip} \left(\frac{1}{\sqrt 2}\right)^{n} = 0^+$: $f$ ha un ordine di crescita strettamente minore di quello di $g$.

        - **(b)** $\displaystyle \lim_{n \rr \ip} \frac{2^{3n/2}}{2^n} = \lim_{n \rr \ip} \big(\sqrt 2\big)^{n} = \ip$: $f$ ha un ordine di crescita strettamente maggiore di quello di $g$.

        - **(c)** $4^n = \big(2^2\big)^n = 2^{2n}$, quindi $\displaystyle \lim_{n \rr \ip} \frac{4^n}{2^{2n}} = 1$: $f$ e $g$ hanno lo stesso ordine di crescita (sono la stessa funzione).

        - **(d)** Poiché $\log_2 n = \frac{\log_{10} n}{\log_{10} 2}$, si ha $\displaystyle \lim_{n \rr \ip} \frac{\log_2 n}{\log_{10} n} = \frac{1}{\log_{10} 2} = \log_2 10 \approx 3.32$: $f$ e $g$ hanno lo stesso ordine di crescita.

        - **(e)** Poiché $\ln(n^2+1) = \ln\big(n^2 (1 + \frac{1}{n^2})\big) = 2\ln n + \ln\big(1+\frac{1}{n^2}\big)$, si ha

            $$
            \lim_{n \rr \ip} \frac{\ln(n^2+1)}{\ln n} = \lim_{n \rr \ip} \Bigg( 2 + \frac{\overbrace{\ln\left(1+\frac{1}{n^2}\right)}^{\rr\, 0}}{\ln n} \Bigg) = 2:
            $$

            $f$ e $g$ hanno lo stesso ordine di crescita.

        - **(f)** $\displaystyle \lim_{n \rr \ip} \frac{n \ln n}{n^{3/2}} = \lim_{n \rr \ip} \frac{\ln n}{n^{1/2}} = 0^+$: $f$ ha un ordine di crescita strettamente minore di quello di $g$.

    2. Le proprietà sono le seguenti.

        - **(a), (b)** Scalatura dell'esponente di un esponenziale, con $\lambda = \frac{1}{2} < 1$ e $\lambda = \frac{3}{2} > 1$ (oppure basi diverse, $\sqrt 2 < 2$ e $2\sqrt 2 > 2$).

        - **(c)** La scalatura dell'esponente con $\lambda = 2$ direbbe che $2^{2n}$ cresce più velocemente di $2^n$; qui, invece, la base $4 = 2^2$ assorbe già il fattore $2$, e le due funzioni coincidono.

        - **(d)** Cambio di base di un logaritmo.

        - **(e)** Nessuna proprietà del capitolo si applica direttamente, poiché l'argomento $n^2+1$ non è né della forma $n+\lambda$ né della forma $\lambda\, n$. L'identità $\ln(n^2+1) = 2\ln n + \ln\big(1+\frac{1}{n^2}\big)$ della prima risposta svolge lo stesso ruolo della traslazione dell'argomento: il termine $\ln\big(1+\frac{1}{n^2}\big)$ tende a $0$, e ciò che resta, $2 \ln n$, ha lo stesso ordine di crescita di $\ln n$.

        - **(f)** Funzione quasi-lineare e potenze, con $\alpha = \frac{3}{2} > 1$.
