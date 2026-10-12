---
title: "Esercizi · Notazione asintotica"
---

# Esercizi · Notazione asintotica

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 9** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 9: Notazione asintotica](../notazione-asintotica/09-notazione-asintotica.md) · [:material-file-pdf-box: Eserciziario, volume 3 (PDF)](../pdf/esercizi-3-notazione-asintotica.pdf)

</div>

Negli esercizi di questo capitolo le notazioni asintotiche si usano con le definizioni e i criteri del limite del capitolo «Notazione asintotica», riassunti qui sotto. I limiti di funzioni di variabile naturale (successioni) si calcolano con i risultati del corso di <em>Analisi Matematica 1</em> ([fabiofurini.github.io/analisi-matematica-1/](https://fabiofurini.github.io/analisi-matematica-1/)).

!!! nota ""

    Date due funzioni $f$ e $g$ di variabile naturale,

    - scriviamo $f(n)=o\big(g(n)\big)$ se per ogni $c \in \R_{>0}$ esiste $n_1 \in \N$ tale che

        $$
        0 \le f(n) < c \: g(n),\qquad \forall n \ge n_1;
        $$

    - scriviamo $f(n)=\bigO\big(g(n)\big)$ se esistono $c \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le f(n) \le c \: g(n),\qquad \forall n \ge n_1;
        $$

    - scriviamo $f(n)=\Theta\big(g(n)\big)$ se esistono $c_1,c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: g(n) \le f(n) \le c_2 \: g(n),\qquad \forall n \ge n_1;
        $$

    - scriviamo $f(n)=\Omega\big(g(n)\big)$ se esistono $c \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c \: g(n) \le f(n),\qquad \forall n \ge n_1;
        $$

    - scriviamo $f(n)=\omega\big(g(n)\big)$ se per ogni $c \in \R_{>0}$ esiste $n_1 \in \N$ tale che

        $$
        0 \le c \: g(n) < f(n),\qquad \forall n \ge n_1.
        $$

!!! nota ""

    Criterio del limite: date due funzioni $f$ e $g$ di variabile naturale asintoticamente positive tali che il limite di $\frac{f(n)}{g(n)}$ esista, si ha

    \begin{align*}
    &\lim_{n \rr +\infty} \frac{f(n)}{g(n)} =0^+ ~~\Longleftrightarrow~~ f(n)= o\big(g(n)\big),\\
    &\lim_{n \rr +\infty} \frac{f(n)}{g(n)} = \ell \in \R_{> 0} \text{ oppure } 0^+ ~~\Longleftrightarrow~~ f(n)= \bigO\big(g(n)\big),\\
    &\lim_{n \rr +\infty} \frac{f(n)}{g(n)} = \ell \in \R_{> 0} ~~\Longleftrightarrow~~ f(n)= \Theta\big(g(n)\big),\\
    &\lim_{n \rr +\infty} \frac{f(n)}{g(n)} = \ell \in \R_{>0} \text{ oppure } +\infty ~~\Longleftrightarrow~~ f(n)= \Omega\big(g(n)\big),\\
    &\lim_{n \rr +\infty} \frac{f(n)}{g(n)} =+\infty ~~\Longleftrightarrow~~ f(n)= \omega\big(g(n)\big).
    \end{align*}

    Quando il rapporto $\frac{f(n)}{g(n)}$ non ha limite (per esempio quando contiene $\sin n$ o $\cos n$), questi criteri non si possono applicare e si usano le definizioni.

<a id="esercizio-9-1"></a>

!!! esercizio "Esercizio 9.1: Notazione asintotica (E1)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 5\;n^4 - 19\;n^3 + 12\;n^2
    $$

    **Domande**

    1. Dimostrare che:

        1. $5\;n^4 - 19\;n^3 + 12\;n^2 = \bigO(n^4)$;

        2. $5\;n^4 - 19\;n^3 + 12\;n^2 = \bigO(n^6)$;

        3. $5\;n^4 - 19\;n^3 + 12\;n^2 = \Theta(n^4)$;

        4. $5\;n^4 - 19\;n^3 + 12\;n^2 \neq \Theta(n^6)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 = \bigO(n^4)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le c\;n^4, \qquad \forall n \ge n_1.
            $$

            Per prima cosa osserviamo che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 = n^2\,(5n^2-19n+12) = n^2\,(5n-4)\,(n-3),
            $$

            quindi

            $$
            0 \le 5\;n^4 - 19\;n^3 + 12\;n^2, \qquad \forall n \ge 3
            $$

            (per $n = 2$ il valore è $f(2) = -24$ $< 0$). Con $n \ge 1$, dividendo per $n^4$, la disuguaglianza $f(n) \le c\,n^4$ è equivalente a

            $$
            5 - \frac{19}{n} + \frac{12}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Poiché

            $$
            -\frac{19}{n} + \frac{12}{n^2} = \frac{12-19n}{n^2} \le 0, \qquad \forall n \ge 1,
            $$

            si ha

            $$
            5 - \frac{19}{n} + \frac{12}{n^2} \le 5, \qquad \forall n \ge 1.
            $$

            Scegliendo per esempio $c = 5$ e $n_1 = 3$, si ha

            $$
            0 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\;n^4, \qquad \forall n \ge 3.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{5\;n^4 - 19\;n^3 + 12\;n^2}{n^4} = \lim_{n \to +\infty} \left(5 - \frac{19}{n} + \frac{12}{n^2}\right) = 5 \in \R_{>0}.
            $$

        2. Per dimostrare che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 = \bigO(n^6)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le c\;n^6, \qquad \forall n \ge n_1.
            $$

            Dalla parte (a), $0 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\,n^4$ per ogni $n \ge 3$. Poiché $n^4 \le n^6$ per $n \ge 1$, si ha anche $5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\;n^6$. Scegliendo per esempio $c = 5$ e $n_1 = 3$, si ha

            $$
            0 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\;n^6, \qquad \forall n \ge 3.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{5\;n^4 - 19\;n^3 + 12\;n^2}{n^6} = \lim_{n \to +\infty} \left(\frac{5}{n^2} - \frac{19}{n^3} + \frac{12}{n^4}\right) = 0^+.
            $$

        3. Per dimostrare che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 = \Theta(n^4)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^4 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le c_2\;n^4, \qquad \forall n \ge n_1.
            $$

            Per la limitazione superiore, per la parte (a), $5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\;n^4$ per ogni $n \ge 1$. Per la limitazione inferiore osserviamo che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 - n^4 = 4\,n^4 - 19\,n^3 + 12\,n^2 = n^2\,(4n-3)\,(n-4),
            $$

            che è non negativa per $n \ge 4$ (per $n = 3$ è uguale a $-81 < 0$). Quindi $n^4 \le 5\;n^4 - 19\;n^3 + 12\;n^2$ per ogni $n \ge 4$. Scegliendo per esempio $c_1 = 1$, $c_2 = 5$ e $n_1 = 4$, si ha

            $$
            0 \le n^4 \le 5\;n^4 - 19\;n^3 + 12\;n^2 \le 5\;n^4, \qquad \forall n \ge 4.
            $$

            Il limite calcolato nella parte (a) dà lo stesso risultato: è uguale a $5 \in \R_{>0}$.

        4. Per dimostrare che

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 \neq \Theta(n^6)
            $$

            procediamo per assurdo e supponiamo che esistano $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^6 \le 5\;n^4 - 19\;n^3 + 12\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^6$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{5}{n^2} - \frac{19}{n^3} + \frac{12}{n^4}, \qquad \forall n \ge n_1.
            $$

            Passando al limite per $n \to +\infty$, otteniamo $0 < c_1 \le 0$, il che è impossibile. Quindi

            $$
            5\;n^4 - 19\;n^3 + 12\;n^2 \neq \Theta(n^6).
            $$

            In alternativa, il limite calcolato nella parte (b) è uguale a $0^+$, quindi $f(n) = o(n^6)$ per il criterio del limite. Allora, con la costante $c = c_1$ nella definizione di $o$, avremmo $f(n) < c_1\,n^6$ per ogni $n$ sufficientemente grande, contro la limitazione inferiore $c_1\,n^6 \le f(n)$.

<a id="esercizio-9-2"></a>

!!! esercizio "Esercizio 9.2: Notazione asintotica (E2)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 3\;n^2 + n^3\,(2 - \sin n)
    $$

    **Domande**

    1. Dimostrare che:

        1. $3\;n^2 + n^3\,(2 - \sin n) = \Theta(n^3)$;

        2. $3\;n^2 + n^3\,(2 - \sin n) \neq o(n^3)$;

        3. $3\;n^2 + n^3\,(2 - \sin n) \neq \omega(n^3)$.

??? soluzione "Soluzione"

    Il rapporto

    $$
    \frac{3\;n^2 + n^3\,(2 - \sin n)}{n^3} = \frac{3}{n} + 2 - \sin n, \qquad n \ge 1,
    $$

    non ha limite per $n \to +\infty$, poiché oscilla. Quindi i criteri del limite non si possono applicare, e usiamo le definizioni. Poiché $-1 \le \sin n \le 1$, si ha $1 \le 2 - \sin n \le 3$, e quindi $1 + \frac{3}{n} \le \frac{3}{n} + 2 - \sin n \le 3 + \frac{3}{n}$. Poiché $0 < \frac{3}{n} \le 3$ per $n \ge 1$, otteniamo

    $$
    1 \le \frac{3}{n} + 2 - \sin n \le 6, \qquad \forall n \ge 1.
    $$

    1. 1. Per dimostrare che

            $$
            3\;n^2 + n^3\,(2 - \sin n) = \Theta(n^3)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^3 \le 3\;n^2 + n^3\,(2 - \sin n) \le c_2\;n^3, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^3$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{3}{n} + 2 - \sin n \le c_2, \qquad \forall n \ge n_1.
            $$

            Per le limitazioni precedenti, scegliendo per esempio $c_1 = \frac{1}{2}$, $c_2 = 6$ e $n_1 = 1$, si ha

            $$
            0 \le \frac{1}{2}\;n^3 \le 3\;n^2 + n^3\,(2 - \sin n) \le 6\;n^3, \qquad \forall n \ge 1.
            $$

        2. Per dimostrare che

            $$
            3\;n^2 + n^3\,(2 - \sin n) \neq o(n^3)
            $$

            ricordiamo che $o(n^3)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le 3\;n^2 + n^3\,(2 - \sin n) < c\;n^3, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^3 > 0$, $\frac{3}{n} + 2 - \sin n < c$ per ogni $n \ge n_1$. Poiché $\frac{3}{n} + 2 - \sin n \ge 1$ per ogni $n \ge 1$, per $c = 1$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            3\;n^2 + n^3\,(2 - \sin n) \neq o(n^3).
            $$

            Equivalentemente, il rapporto è limitato dal basso da $1$ e non può convergere a $0$.

        3. Per dimostrare che

            $$
            3\;n^2 + n^3\,(2 - \sin n) \neq \omega(n^3)
            $$

            ricordiamo che $\omega(n^3)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le c\;n^3 < 3\;n^2 + n^3\,(2 - \sin n), \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^3 > 0$, $c < \frac{3}{n} + 2 - \sin n$ per ogni $n \ge n_1$. Poiché $\frac{3}{n} + 2 - \sin n \le 6$ per ogni $n \ge 1$, per $c = 6$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            3\;n^2 + n^3\,(2 - \sin n) \neq \omega(n^3).
            $$

            Equivalentemente, il rapporto è limitato dall'alto da $6$ e non può divergere a $+\infty$.

<a id="esercizio-9-3"></a>

!!! esercizio "Esercizio 9.3: Notazione asintotica (E3)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 3\;n^3 - 7\;n^2 + 2\;n
    $$

    **Domande**

    1. Dimostrare che:

        1. $3\;n^3 - 7\;n^2 + 2\;n = \bigO(n^3)$;

        2. $3\;n^3 - 7\;n^2 + 2\;n = \bigO(n^5)$;

        3. $3\;n^3 - 7\;n^2 + 2\;n = \Theta(n^3)$;

        4. $3\;n^3 - 7\;n^2 + 2\;n \neq \Theta(n^5)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che

            $$
            3\;n^3 - 7\;n^2 + 2\;n = \bigO(n^3)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 3\;n^3 - 7\;n^2 + 2\;n \le c\;n^3, \qquad \forall n \ge n_1.
            $$

            Per prima cosa osserviamo che

            $$
            3\;n^3 - 7\;n^2 + 2\;n = n\,(3n^2-7n+2) = n\,(3n-1)\,(n-2),
            $$

            quindi

            $$
            0 \le 3\;n^3 - 7\;n^2 + 2\;n, \qquad \forall n \ge 2
            $$

            (per $n = 1$ il valore è $f(1) = -2$ $< 0$). Con $n \ge 1$, dividendo per $n^3$, la disuguaglianza $f(n) \le c\,n^3$ è equivalente a

            $$
            3 - \frac{7}{n} + \frac{2}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Poiché

            $$
            -\frac{7}{n} + \frac{2}{n^2} = \frac{2-7n}{n^2} \le 0, \qquad \forall n \ge 1,
            $$

            si ha

            $$
            3 - \frac{7}{n} + \frac{2}{n^2} \le 3, \qquad \forall n \ge 1.
            $$

            Scegliendo per esempio $c = 3$ e $n_1 = 2$, si ha

            $$
            0 \le 3\;n^3 - 7\;n^2 + 2\;n \le 3\;n^3, \qquad \forall n \ge 2.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{3\;n^3 - 7\;n^2 + 2\;n}{n^3} = \lim_{n \to +\infty} \left(3 - \frac{7}{n} + \frac{2}{n^2}\right) = 3 \in \R_{>0}.
            $$

        2. Per dimostrare che

            $$
            3\;n^3 - 7\;n^2 + 2\;n = \bigO(n^5)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 3\;n^3 - 7\;n^2 + 2\;n \le c\;n^5, \qquad \forall n \ge n_1.
            $$

            Dalla parte (a), $0 \le 3\;n^3 - 7\;n^2 + 2\;n \le 3\,n^3$ per ogni $n \ge 2$. Poiché $n^3 \le n^5$ per $n \ge 1$, si ha anche $3\;n^3 - 7\;n^2 + 2\;n \le 3\;n^5$. Scegliendo per esempio $c = 3$ e $n_1 = 2$, si ha

            $$
            0 \le 3\;n^3 - 7\;n^2 + 2\;n \le 3\;n^5, \qquad \forall n \ge 2.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{3\;n^3 - 7\;n^2 + 2\;n}{n^5} = \lim_{n \to +\infty} \left(\frac{3}{n^2} - \frac{7}{n^3} + \frac{2}{n^4}\right) = 0^+.
            $$

        3. Per dimostrare che

            $$
            3\;n^3 - 7\;n^2 + 2\;n = \Theta(n^3)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^3 \le 3\;n^3 - 7\;n^2 + 2\;n \le c_2\;n^3, \qquad \forall n \ge n_1.
            $$

            Per la limitazione superiore, per la parte (a), $3\;n^3 - 7\;n^2 + 2\;n \le 3\;n^3$ per ogni $n \ge 1$. Per la limitazione inferiore osserviamo che

            $$
            3\;n^3 - 7\;n^2 + 2\;n - n^3 = 2\,n^3 - 7\,n^2 + 2\,n = n\,(2n^2-7n+2),
            $$

            dove le radici di $2n^2-7n+2$ sono $\frac{7 \pm \sqrt{33}}{4}$, cioè circa $0.31$ e $3.19$; quindi $2n^2-7n+2 > 0$ per ogni intero $n \ge 4$ (per $n=4$ è uguale a $6$, per $n = 3$ è uguale a $-1$). Quindi $n^3 \le 3\;n^3 - 7\;n^2 + 2\;n$ per ogni $n \ge 4$. Scegliendo per esempio $c_1 = 1$, $c_2 = 3$ e $n_1 = 4$, si ha

            $$
            0 \le n^3 \le 3\;n^3 - 7\;n^2 + 2\;n \le 3\;n^3, \qquad \forall n \ge 4.
            $$

            Il limite calcolato nella parte (a) dà lo stesso risultato: è uguale a $3 \in \R_{>0}$.

        4. Per dimostrare che

            $$
            3\;n^3 - 7\;n^2 + 2\;n \neq \Theta(n^5)
            $$

            procediamo per assurdo e supponiamo che esistano $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^5 \le 3\;n^3 - 7\;n^2 + 2\;n, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^5$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{3}{n^2} - \frac{7}{n^3} + \frac{2}{n^4}, \qquad \forall n \ge n_1.
            $$

            Passando al limite per $n \to +\infty$, otteniamo $0 < c_1 \le 0$, il che è impossibile. Quindi

            $$
            3\;n^3 - 7\;n^2 + 2\;n \neq \Theta(n^5).
            $$

            In alternativa, il limite calcolato nella parte (b) è uguale a $0^+$, quindi $f(n) = o(n^5)$ per il criterio del limite. Allora, con la costante $c = c_1$ nella definizione di $o$, avremmo $f(n) < c_1\,n^5$ per ogni $n$ sufficientemente grande, contro la limitazione inferiore $c_1\,n^5 \le f(n)$.

<a id="esercizio-9-4"></a>

!!! esercizio "Esercizio 9.4: Notazione asintotica (E4)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto n^2\,(3 + \cos n)
    $$

    **Domande**

    1. Dimostrare che:

        1. $n^2\,(3 + \cos n) = \Theta(n^2)$;

        2. $n^2\,(3 + \cos n) \neq o(n^2)$;

        3. $n^2\,(3 + \cos n) \neq \omega(n^2)$.

??? soluzione "Soluzione"

    Il rapporto

    $$
    \frac{n^2\,(3 + \cos n)}{n^2} = 3 + \cos n, \qquad n \ge 1,
    $$

    non ha limite per $n \to +\infty$, poiché oscilla. Quindi i criteri del limite non si possono applicare, e usiamo le definizioni. Poiché $-1 \le \cos n \le 1$, si ha

    $$
    2 \le 3 + \cos n \le 4, \qquad \forall n \ge 1.
    $$

    1. 1. Per dimostrare che

            $$
            n^2\,(3 + \cos n) = \Theta(n^2)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^2 \le n^2\,(3 + \cos n) \le c_2\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le 3 + \cos n \le c_2, \qquad \forall n \ge n_1.
            $$

            Per le limitazioni precedenti, scegliendo per esempio $c_1 = 2$, $c_2 = 4$ e $n_1 = 1$, si ha

            $$
            0 \le 2\;n^2 \le n^2\,(3 + \cos n) \le 4\;n^2, \qquad \forall n \ge 1.
            $$

        2. Per dimostrare che

            $$
            n^2\,(3 + \cos n) \neq o(n^2)
            $$

            ricordiamo che $o(n^2)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le n^2\,(3 + \cos n) < c\;n^2, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^2 > 0$, $3 + \cos n < c$ per ogni $n \ge n_1$. Poiché $3 + \cos n \ge 2$ per ogni $n \ge 1$, per $c = 2$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^2\,(3 + \cos n) \neq o(n^2).
            $$

            Equivalentemente, il rapporto è limitato dal basso da $2$ e non può convergere a $0$.

        3. Per dimostrare che

            $$
            n^2\,(3 + \cos n) \neq \omega(n^2)
            $$

            ricordiamo che $\omega(n^2)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le c\;n^2 < n^2\,(3 + \cos n), \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^2 > 0$, $c < 3 + \cos n$ per ogni $n \ge n_1$. Poiché $3 + \cos n \le 4$ per ogni $n \ge 1$, per $c = 4$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^2\,(3 + \cos n) \neq \omega(n^2).
            $$

            Equivalentemente, il rapporto è limitato dall'alto da $4$ e non può divergere a $+\infty$.

<a id="esercizio-9-5"></a>

!!! esercizio "Esercizio 9.5: Notazione asintotica (E5)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 2\;n^5 - 8\;n^4 + 3\;n^3
    $$

    **Domande**

    1. Dimostrare che:

        1. $2\;n^5 - 8\;n^4 + 3\;n^3 = \bigO(n^5)$;

        2. $2\;n^5 - 8\;n^4 + 3\;n^3 = \Theta(n^5)$;

        3. $2\;n^5 - 8\;n^4 + 3\;n^3 \neq \Theta(n^3)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che

            $$
            2\;n^5 - 8\;n^4 + 3\;n^3 = \bigO(n^5)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 2\;n^5 - 8\;n^4 + 3\;n^3 \le c\;n^5, \qquad \forall n \ge n_1.
            $$

            Per prima cosa fattorizziamo:

            $$
            2\;n^5 - 8\;n^4 + 3\;n^3 = n^3\,(2n^2 - 8n + 3),
            $$

            dove le radici di $2n^2-8n+3$ sono $2 \pm \frac{\sqrt{10}}{2}$, cioè circa $0.42$ e $3.58$. Quindi $f(n) \ge 0$ per ogni intero $n \ge 4$ (per $n = 4$ il fattore $2n^2-8n+3$ è uguale a $3$; per $n = 3$ si ha $f(3) = -81 < 0$). Con $n \ge 1$, dividendo per $n^5$, la disuguaglianza $f(n) \le c\,n^5$ è equivalente a

            $$
            2 - \frac{8}{n} + \frac{3}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Poiché

            $$
            -\frac{8}{n} + \frac{3}{n^2} = \frac{3-8n}{n^2} \le 0, \qquad \forall n \ge 1,
            $$

            si ha

            $$
            2 - \frac{8}{n} + \frac{3}{n^2} \le 2, \qquad \forall n \ge 1.
            $$

            Scegliendo per esempio $c = 2$ e $n_1 = 4$, si ha

            $$
            0 \le 2\;n^5 - 8\;n^4 + 3\;n^3 \le 2\;n^5, \qquad \forall n \ge 4.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{2\;n^5 - 8\;n^4 + 3\;n^3}{n^5} = \lim_{n \to +\infty} \left(2 - \frac{8}{n} + \frac{3}{n^2}\right) = 2 \in \R_{>0}.
            $$

        2. Per dimostrare che

            $$
            2\;n^5 - 8\;n^4 + 3\;n^3 = \Theta(n^5)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^5 \le 2\;n^5 - 8\;n^4 + 3\;n^3 \le c_2\;n^5, \qquad \forall n \ge n_1.
            $$

            Per la limitazione superiore, per la parte (a), $2\;n^5 - 8\;n^4 + 3\;n^3 \le 2\;n^5$ per ogni $n \ge 1$. Per la limitazione inferiore osserviamo che

            $$
            2\;n^5 - 8\;n^4 + 3\;n^3 - n^5 = n^5 - 8\,n^4 + 3\,n^3 = n^3\,(n^2 - 8n + 3),
            $$

            dove le radici di $n^2-8n+3$ sono $4 \pm \sqrt{13}$, cioè circa $0.39$ e $7.61$. Quindi $n^5 \le 2\;n^5 - 8\;n^4 + 3\;n^3$ per ogni intero $n \ge 8$ (per $n = 8$ il fattore $n^2-8n+3$ è uguale a $3$, per $n = 7$ è uguale a $-4$). Scegliendo per esempio $c_1 = 1$, $c_2 = 2$ e $n_1 = 8$, si ha

            $$
            0 \le n^5 \le 2\;n^5 - 8\;n^4 + 3\;n^3 \le 2\;n^5, \qquad \forall n \ge 8.
            $$

            Il limite calcolato nella parte (a) dà lo stesso risultato: è uguale a $2 \in \R_{>0}$.

        3. Per dimostrare che

            $$
            2\;n^5 - 8\;n^4 + 3\;n^3 \neq \Theta(n^3)
            $$

            procediamo per assurdo e supponiamo che esistano $c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 2\;n^5 - 8\;n^4 + 3\;n^3 \le c_2\;n^3, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^3$, questo equivale a

            $$
            0 \le 2\,n^2 - 8\,n + 3 \le c_2, \qquad \forall n \ge n_1.
            $$

            Poiché $2\,n^2 - 8\,n + 3 \rr +\infty$ per $n \rr +\infty$, l'espressione centrale non può restare limitata dalla costante $c_2$: questo è assurdo.

            In alternativa, calcoliamo il limite

            $$
            \lim_{n \to +\infty} \frac{2\;n^5 - 8\;n^4 + 3\;n^3}{n^3} = \lim_{n \to +\infty} \left(2\,n^2 - 8\,n + 3\right) = +\infty,
            $$

            quindi $f(n) = \omega(n^3)$ per il criterio del limite. Allora, con la costante $c = c_2$ nella definizione di $\omega$, avremmo $f(n) > c_2\,n^3$ per ogni $n$ sufficientemente grande, contro la limitazione superiore $f(n) \le c_2\,n^3$. Quindi $f(n) \neq \Theta(n^3)$.

<a id="esercizio-9-6"></a>

!!! esercizio "Esercizio 9.6: Notazione asintotica (E6)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto n^3\,(4 - \sin n) + 5\;n^2
    $$

    **Domande**

    1. Dimostrare che:

        1. $n^3\,(4 - \sin n) + 5\;n^2 = \Theta(n^3)$;

        2. $n^3\,(4 - \sin n) + 5\;n^2 \neq o(n^3)$;

        3. $n^3\,(4 - \sin n) + 5\;n^2 \neq \omega(n^3)$.

??? soluzione "Soluzione"

    Il rapporto

    $$
    \frac{n^3\,(4 - \sin n) + 5\;n^2}{n^3} = 4 - \sin n + \frac{5}{n}, \qquad n \ge 1,
    $$

    non ha limite per $n \to +\infty$, poiché oscilla. Quindi i criteri del limite non si possono applicare, e usiamo le definizioni. Poiché $-1 \le \sin n \le 1$, si ha $3 \le 4 - \sin n \le 5$. Poiché $0 < \frac{5}{n} \le 5$ per $n \ge 1$, otteniamo

    $$
    3 \le 4 - \sin n + \frac{5}{n} \le 10, \qquad \forall n \ge 1.
    $$

    1. 1. Per dimostrare che

            $$
            n^3\,(4 - \sin n) + 5\;n^2 = \Theta(n^3)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^3 \le n^3\,(4 - \sin n) + 5\;n^2 \le c_2\;n^3, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^3$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le 4 - \sin n + \frac{5}{n} \le c_2, \qquad \forall n \ge n_1.
            $$

            Per le limitazioni precedenti, scegliendo per esempio $c_1 = 3$, $c_2 = 10$ e $n_1 = 1$, si ha

            $$
            0 \le 3\;n^3 \le n^3\,(4 - \sin n) + 5\;n^2 \le 10\;n^3, \qquad \forall n \ge 1.
            $$

        2. Per dimostrare che

            $$
            n^3\,(4 - \sin n) + 5\;n^2 \neq o(n^3)
            $$

            ricordiamo che $o(n^3)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le n^3\,(4 - \sin n) + 5\;n^2 < c\;n^3, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^3 > 0$, $4 - \sin n + \frac{5}{n} < c$ per ogni $n \ge n_1$. Poiché $4 - \sin n + \frac{5}{n} \ge 3$ per ogni $n \ge 1$, per $c = 3$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^3\,(4 - \sin n) + 5\;n^2 \neq o(n^3).
            $$

            Equivalentemente, il rapporto è limitato dal basso da $3$ e non può convergere a $0$.

        3. Per dimostrare che

            $$
            n^3\,(4 - \sin n) + 5\;n^2 \neq \omega(n^3)
            $$

            ricordiamo che $\omega(n^3)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le c\;n^3 < n^3\,(4 - \sin n) + 5\;n^2, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^3 > 0$, $c < 4 - \sin n + \frac{5}{n}$ per ogni $n \ge n_1$. Poiché $4 - \sin n + \frac{5}{n} \le 10$ per ogni $n \ge 1$, per $c = 10$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^3\,(4 - \sin n) + 5\;n^2 \neq \omega(n^3).
            $$

            Equivalentemente, il rapporto è limitato dall'alto da $10$ e non può divergere a $+\infty$.

<a id="esercizio-9-7"></a>

!!! esercizio "Esercizio 9.7: Notazione asintotica (E7)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 4\;n^4 - n^3 - 6\;n^2
    $$

    **Domande**

    1. Dimostrare che:

        1. $4\;n^4 - n^3 - 6\;n^2 = \bigO(n^4)$;

        2. $4\;n^4 - n^3 - 6\;n^2 = \Theta(n^4)$;

        3. $4\;n^4 - n^3 - 6\;n^2 \neq \Theta(n^2)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che

            $$
            4\;n^4 - n^3 - 6\;n^2 = \bigO(n^4)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 4\;n^4 - n^3 - 6\;n^2 \le c\;n^4, \qquad \forall n \ge n_1.
            $$

            Per prima cosa fattorizziamo:

            $$
            4\;n^4 - n^3 - 6\;n^2 = n^2\,(4n^2 - n - 6),
            $$

            dove le radici di $4n^2-n-6$ sono $\frac{1 \pm \sqrt{97}}{8}$, cioè circa $-1.11$ e $1.36$. Quindi $f(n) \ge 0$ per ogni intero $n \ge 2$ (per $n = 2$ il fattore $4n^2-n-6$ è uguale a $8$; per $n = 1$ si ha $f(1) = -3 < 0$). Con $n \ge 1$, dividendo per $n^4$, la disuguaglianza $f(n) \le c\,n^4$ è equivalente a

            $$
            4 - \frac{1}{n} - \frac{6}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Poiché

            $$
            -\frac{1}{n} - \frac{6}{n^2} = -\frac{n+6}{n^2} \le 0, \qquad \forall n \ge 1,
            $$

            si ha

            $$
            4 - \frac{1}{n} - \frac{6}{n^2} \le 4, \qquad \forall n \ge 1.
            $$

            Scegliendo per esempio $c = 4$ e $n_1 = 2$, si ha

            $$
            0 \le 4\;n^4 - n^3 - 6\;n^2 \le 4\;n^4, \qquad \forall n \ge 2.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{4\;n^4 - n^3 - 6\;n^2}{n^4} = \lim_{n \to +\infty} \left(4 - \frac{1}{n} - \frac{6}{n^2}\right) = 4 \in \R_{>0}.
            $$

        2. Per dimostrare che

            $$
            4\;n^4 - n^3 - 6\;n^2 = \Theta(n^4)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^4 \le 4\;n^4 - n^3 - 6\;n^2 \le c_2\;n^4, \qquad \forall n \ge n_1.
            $$

            Per la limitazione superiore, per la parte (a), $4\;n^4 - n^3 - 6\;n^2 \le 4\;n^4$ per ogni $n \ge 1$. Per la limitazione inferiore osserviamo che

            $$
            4\;n^4 - n^3 - 6\;n^2 - 3\;n^4 = n^4 - n^3 - 6\,n^2 = n^2\,(n-3)\,(n+2),
            $$

            che è non negativa per ogni intero $n \ge 3$ (è uguale a $0$ per $n = 3$ e positiva per $n \ge 4$). Quindi $3\;n^4 \le 4\;n^4 - n^3 - 6\;n^2$ per ogni $n \ge 3$; scegliamo $n_1 = 4$, ma andrebbe bene anche $n_1 = 3$. Scegliendo per esempio $c_1 = 3$, $c_2 = 4$ e $n_1 = 4$, si ha

            $$
            0 \le 3\;n^4 \le 4\;n^4 - n^3 - 6\;n^2 \le 4\;n^4, \qquad \forall n \ge 4.
            $$

            Il limite calcolato nella parte (a) dà lo stesso risultato: è uguale a $4 \in \R_{>0}$.

        3. Per dimostrare che

            $$
            4\;n^4 - n^3 - 6\;n^2 \neq \Theta(n^2)
            $$

            procediamo per assurdo e supponiamo che esistano $c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 4\;n^4 - n^3 - 6\;n^2 \le c_2\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$, questo equivale a

            $$
            0 \le 4\,n^2 - n - 6 \le c_2, \qquad \forall n \ge n_1.
            $$

            Poiché $4\,n^2 - n - 6 \rr +\infty$ per $n \rr +\infty$, l'espressione centrale non può restare limitata dalla costante $c_2$: questo è assurdo.

            In alternativa, calcoliamo il limite

            $$
            \lim_{n \to +\infty} \frac{4\;n^4 - n^3 - 6\;n^2}{n^2} = \lim_{n \to +\infty} \left(4\,n^2 - n - 6\right) = +\infty,
            $$

            quindi $f(n) = \omega(n^2)$ per il criterio del limite. Allora, con la costante $c = c_2$ nella definizione di $\omega$, avremmo $f(n) > c_2\,n^2$ per ogni $n$ sufficientemente grande, contro la limitazione superiore $f(n) \le c_2\,n^2$. Quindi $f(n) \neq \Theta(n^2)$.

<a id="esercizio-9-8"></a>

!!! esercizio "Esercizio 9.8: Notazione asintotica (E8)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto n^4\,(1 + \sin^2 n)
    $$

    **Domande**

    1. Dimostrare che:

        1. $n^4\,(1 + \sin^2 n) = \Theta(n^4)$;

        2. $n^4\,(1 + \sin^2 n) \neq o(n^4)$;

        3. $n^4\,(1 + \sin^2 n) \neq \omega(n^4)$.

??? soluzione "Soluzione"

    Il rapporto

    $$
    \frac{n^4\,(1 + \sin^2 n)}{n^4} = 1 + \sin^2 n, \qquad n \ge 1,
    $$

    non ha limite per $n \to +\infty$, poiché oscilla. Quindi i criteri del limite non si possono applicare, e usiamo le definizioni. Poiché $0 \le \sin^2 n \le 1$, si ha

    $$
    1 \le 1 + \sin^2 n \le 2, \qquad \forall n \ge 1.
    $$

    1. 1. Per dimostrare che

            $$
            n^4\,(1 + \sin^2 n) = \Theta(n^4)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^4 \le n^4\,(1 + \sin^2 n) \le c_2\;n^4, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^4$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le 1 + \sin^2 n \le c_2, \qquad \forall n \ge n_1.
            $$

            Per le limitazioni precedenti, scegliendo per esempio $c_1 = 1$, $c_2 = 2$ e $n_1 = 1$, si ha

            $$
            0 \le 1\;n^4 \le n^4\,(1 + \sin^2 n) \le 2\;n^4, \qquad \forall n \ge 1.
            $$

        2. Per dimostrare che

            $$
            n^4\,(1 + \sin^2 n) \neq o(n^4)
            $$

            ricordiamo che $o(n^4)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le n^4\,(1 + \sin^2 n) < c\;n^4, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^4 > 0$, $1 + \sin^2 n < c$ per ogni $n \ge n_1$. Poiché $1 + \sin^2 n \ge 1$ per ogni $n \ge 1$, per $c = 1$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^4\,(1 + \sin^2 n) \neq o(n^4).
            $$

            Equivalentemente, il rapporto è limitato dal basso da $1$ e non può convergere a $0$.

        3. Per dimostrare che

            $$
            n^4\,(1 + \sin^2 n) \neq \omega(n^4)
            $$

            ricordiamo che $\omega(n^4)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le c\;n^4 < n^4\,(1 + \sin^2 n), \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^4 > 0$, $c < 1 + \sin^2 n$ per ogni $n \ge n_1$. Poiché $1 + \sin^2 n \le 2$ per ogni $n \ge 1$, per $c = 2$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^4\,(1 + \sin^2 n) \neq \omega(n^4).
            $$

            Equivalentemente, il rapporto è limitato dall'alto da $2$ e non può divergere a $+\infty$.

<a id="esercizio-9-9"></a>

!!! esercizio "Esercizio 9.9: Notazione asintotica (E9)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto 6\;n^3 - 11\;n^2 + 4\;n
    $$

    **Domande**

    1. Dimostrare che:

        1. $6\;n^3 - 11\;n^2 + 4\;n = \bigO(n^3)$;

        2. $6\;n^3 - 11\;n^2 + 4\;n = \bigO(n^4)$;

        3. $6\;n^3 - 11\;n^2 + 4\;n = \Theta(n^3)$;

        4. $6\;n^3 - 11\;n^2 + 4\;n \neq \Theta(n^4)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che

            $$
            6\;n^3 - 11\;n^2 + 4\;n = \bigO(n^3)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 6\;n^3 - 11\;n^2 + 4\;n \le c\;n^3, \qquad \forall n \ge n_1.
            $$

            Per prima cosa osserviamo che

            $$
            6\;n^3 - 11\;n^2 + 4\;n = n\,(6n^2-11n+4) = n\,(2n-1)\,(3n-4),
            $$

            quindi

            $$
            0 \le 6\;n^3 - 11\;n^2 + 4\;n, \qquad \forall n \ge 2
            $$

            (per $n = 1$ il valore è $f(1) = -1$ $< 0$). Con $n \ge 1$, dividendo per $n^3$, la disuguaglianza $f(n) \le c\,n^3$ è equivalente a

            $$
            6 - \frac{11}{n} + \frac{4}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Poiché

            $$
            -\frac{11}{n} + \frac{4}{n^2} = \frac{4-11n}{n^2} \le 0, \qquad \forall n \ge 1,
            $$

            si ha

            $$
            6 - \frac{11}{n} + \frac{4}{n^2} \le 6, \qquad \forall n \ge 1.
            $$

            Scegliendo per esempio $c = 6$ e $n_1 = 2$, si ha

            $$
            0 \le 6\;n^3 - 11\;n^2 + 4\;n \le 6\;n^3, \qquad \forall n \ge 2.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{6\;n^3 - 11\;n^2 + 4\;n}{n^3} = \lim_{n \to +\infty} \left(6 - \frac{11}{n} + \frac{4}{n^2}\right) = 6 \in \R_{>0}.
            $$

        2. Per dimostrare che

            $$
            6\;n^3 - 11\;n^2 + 4\;n = \bigO(n^4)
            $$

            determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le 6\;n^3 - 11\;n^2 + 4\;n \le c\;n^4, \qquad \forall n \ge n_1.
            $$

            Dalla parte (a), $0 \le 6\;n^3 - 11\;n^2 + 4\;n \le 6\,n^3$ per ogni $n \ge 2$. Poiché $n^3 \le n^4$ per $n \ge 1$, si ha anche $6\;n^3 - 11\;n^2 + 4\;n \le 6\;n^4$. Scegliendo per esempio $c = 6$ e $n_1 = 2$, si ha

            $$
            0 \le 6\;n^3 - 11\;n^2 + 4\;n \le 6\;n^4, \qquad \forall n \ge 2.
            $$

            Poiché le funzioni sono asintoticamente positive, un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{6\;n^3 - 11\;n^2 + 4\;n}{n^4} = \lim_{n \to +\infty} \left(\frac{6}{n} - \frac{11}{n^2} + \frac{4}{n^3}\right) = 0^+.
            $$

        3. Per dimostrare che

            $$
            6\;n^3 - 11\;n^2 + 4\;n = \Theta(n^3)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^3 \le 6\;n^3 - 11\;n^2 + 4\;n \le c_2\;n^3, \qquad \forall n \ge n_1.
            $$

            Per la limitazione superiore, per la parte (a), $6\;n^3 - 11\;n^2 + 4\;n \le 6\;n^3$ per ogni $n \ge 1$. Per la limitazione inferiore osserviamo che

            $$
            6\;n^3 - 11\;n^2 + 4\;n - 5\;n^3 = n^3 - 11\,n^2 + 4\,n = n\,(n^2-11n+4),
            $$

            dove le radici di $n^2-11n+4$ sono $\frac{11 \pm \sqrt{105}}{2}$, cioè circa $0.38$ e $10.62$; quindi $n^2-11n+4 > 0$ per ogni intero $n \ge 11$ (per $n=11$ è uguale a $4$, per $n = 10$ è uguale a $-6$). Quindi $5\;n^3 \le 6\;n^3 - 11\;n^2 + 4\;n$ per ogni $n \ge 11$. Scegliendo per esempio $c_1 = 5$, $c_2 = 6$ e $n_1 = 11$, si ha

            $$
            0 \le 5\;n^3 \le 6\;n^3 - 11\;n^2 + 4\;n \le 6\;n^3, \qquad \forall n \ge 11.
            $$

            Il limite calcolato nella parte (a) dà lo stesso risultato: è uguale a $6 \in \R_{>0}$.

        4. Per dimostrare che

            $$
            6\;n^3 - 11\;n^2 + 4\;n \neq \Theta(n^4)
            $$

            procediamo per assurdo e supponiamo che esistano $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^4 \le 6\;n^3 - 11\;n^2 + 4\;n, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^4$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{6}{n} - \frac{11}{n^2} + \frac{4}{n^3}, \qquad \forall n \ge n_1.
            $$

            Passando al limite per $n \to +\infty$, otteniamo $0 < c_1 \le 0$, il che è impossibile. Quindi

            $$
            6\;n^3 - 11\;n^2 + 4\;n \neq \Theta(n^4).
            $$

            In alternativa, il limite calcolato nella parte (b) è uguale a $0^+$, quindi $f(n) = o(n^4)$ per il criterio del limite. Allora, con la costante $c = c_1$ nella definizione di $o$, avremmo $f(n) < c_1\,n^4$ per ogni $n$ sufficientemente grande, contro la limitazione inferiore $c_1\,n^4 \le f(n)$.

<a id="esercizio-9-10"></a>

!!! esercizio "Esercizio 9.10: Notazione asintotica (E10)"

    Consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto n^2\,(2 + \cos^2 n)
    $$

    **Domande**

    1. Dimostrare che:

        1. $n^2\,(2 + \cos^2 n) = \Theta(n^2)$;

        2. $n^2\,(2 + \cos^2 n) \neq o(n^2)$;

        3. $n^2\,(2 + \cos^2 n) \neq \omega(n^2)$.

??? soluzione "Soluzione"

    Il rapporto

    $$
    \frac{n^2\,(2 + \cos^2 n)}{n^2} = 2 + \cos^2 n, \qquad n \ge 1,
    $$

    non ha limite per $n \to +\infty$, poiché oscilla. Quindi i criteri del limite non si possono applicare, e usiamo le definizioni. Poiché $0 \le \cos^2 n \le 1$, si ha

    $$
    2 \le 2 + \cos^2 n \le 3, \qquad \forall n \ge 1.
    $$

    1. 1. Per dimostrare che

            $$
            n^2\,(2 + \cos^2 n) = \Theta(n^2)
            $$

            determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^2 \le n^2\,(2 + \cos^2 n) \le c_2\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le 2 + \cos^2 n \le c_2, \qquad \forall n \ge n_1.
            $$

            Per le limitazioni precedenti, scegliendo per esempio $c_1 = 2$, $c_2 = 3$ e $n_1 = 1$, si ha

            $$
            0 \le 2\;n^2 \le n^2\,(2 + \cos^2 n) \le 3\;n^2, \qquad \forall n \ge 1.
            $$

        2. Per dimostrare che

            $$
            n^2\,(2 + \cos^2 n) \neq o(n^2)
            $$

            ricordiamo che $o(n^2)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le n^2\,(2 + \cos^2 n) < c\;n^2, \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^2 > 0$, $2 + \cos^2 n < c$ per ogni $n \ge n_1$. Poiché $2 + \cos^2 n \ge 2$ per ogni $n \ge 1$, per $c = 2$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^2\,(2 + \cos^2 n) \neq o(n^2).
            $$

            Equivalentemente, il rapporto è limitato dal basso da $2$ e non può convergere a $0$.

        3. Per dimostrare che

            $$
            n^2\,(2 + \cos^2 n) \neq \omega(n^2)
            $$

            ricordiamo che $\omega(n^2)$ richiede che per ogni $c \in \R_{>0}$ esista $n_1 \in \N$ tale che

            $$
            0 \le c\;n^2 < n^2\,(2 + \cos^2 n), \qquad \forall n \ge n_1,
            $$

            cioè, dividendo per $n^2 > 0$, $c < 2 + \cos^2 n$ per ogni $n \ge n_1$. Poiché $2 + \cos^2 n \le 3$ per ogni $n \ge 1$, per $c = 3$ non esiste nessun $n_1$ con questa proprietà. Quindi

            $$
            n^2\,(2 + \cos^2 n) \neq \omega(n^2).
            $$

            Equivalentemente, il rapporto è limitato dall'alto da $3$ e non può divergere a $+\infty$.

<a id="esercizio-9-11"></a>

!!! esercizio "Esercizio 9.11: Notazione asintotica (E11)"

    Dati $a \in \R_{>0}$ e $b \in \R$, consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto a\;n + b.
    $$

    **Domande**

    1. Dimostrare, usando le definizioni, che per ogni $a \in \R_{>0}$ e $b \in \R$:

        1. $a\;n + b = \bigO(n)$;

        2. $a\;n + b = \bigO(n^2)$;

        3. $a\;n + b = \Theta(n)$;

        4. $a\;n + b \neq \Theta(n^2)$.

??? soluzione "Soluzione"

    L'osservazione chiave è la seguente: se $n \ge \frac{2\,|b|}{a}$, allora $|b| \le \frac{a}{2}\,n$, e quindi

    $$
    \frac{1}{2}\,a\,n = a\,n - \frac{a}{2}\,n \le a\,n - |b| \le a\,n + b \le a\,n + |b| \le a\,n + \frac{a}{2}\,n = \frac{3}{2}\,a\,n.
    $$

    Per avere anche $n \ge 1$ (così da poter dividere per $n$), usiamo la soglia

    $$
    n_1 = \max\left\{1, \left\lceil \frac{2\,|b|}{a} \right\rceil\right\}.
    $$

    1. 1. Per dimostrare che $a\;n + b = \bigO(n)$, determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le a\;n + b \le c\;n, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n$, questo equivale a

            $$
            0 \le a + \frac{b}{n} \le c, \qquad \forall n \ge n_1.
            $$

            Per l'osservazione chiave, $\frac{a}{2} \le a + \frac{b}{n} \le \frac{3}{2}\,a$ per ogni $n \ge \frac{2|b|}{a}$ (il valore superiore è raggiunto quando $b > 0$ e $n = \frac{2b}{a}$). Quindi, scegliendo per esempio $c = \frac{3}{2}\,a > 0$ e $n_1 = \max\left\{1, \left\lceil \frac{2|b|}{a} \right\rceil\right\}$, si ha

            $$
            0 \le a\;n + b \le \frac{3}{2}\,a\;n, \qquad \forall n \ge \max\left\{1, \left\lceil \frac{2\,|b|}{a} \right\rceil\right\}.
            $$

        2. Per dimostrare che $a\;n + b = \bigO(n^2)$, determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le a\;n + b \le c\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$, questo equivale a

            $$
            0 \le \frac{a}{n} + \frac{b}{n^2} \le c, \qquad \forall n \ge n_1.
            $$

            Per la disuguaglianza di sinistra serve $a\,n + b \ge 0$, cioè $n \ge -\frac{b}{a}$; insieme a $n \ge 1$ ciò dà la soglia $\max\left\{1, -\frac{b}{a}\right\}$. Per la disuguaglianza di destra, per ogni $n \ge 1$ si ha

            $$
            \frac{a}{n} + \frac{b}{n^2} \le \frac{a}{n} + \frac{|b|}{n^2} \le a + |b|.
            $$

            Quindi, scegliendo per esempio $c = a + |b| > 0$ e $n_1 = \left\lceil \max\left\{1, -\frac{b}{a}\right\} \right\rceil$, si ha

            $$
            0 \le a\;n + b \le (a + |b|)\;n^2, \qquad \forall n \ge \left\lceil \max\left\{1, -\frac{b}{a}\right\} \right\rceil.
            $$

        3. Per dimostrare che $a\;n + b = \Theta(n)$, determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n \le a\;n + b \le c_2\;n, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le a + \frac{b}{n} \le c_2, \qquad \forall n \ge n_1.
            $$

            Per l'osservazione chiave, $\frac{a}{2} \le a + \frac{b}{n} \le \frac{3}{2}\,a$ per ogni $n \ge \frac{2|b|}{a}$ (il valore inferiore è raggiunto quando $b < 0$ e $n = \frac{2|b|}{a}$, quello superiore quando $b > 0$ e $n = \frac{2b}{a}$). Quindi, scegliendo per esempio $c_1 = \frac{1}{2}\,a > 0$, $c_2 = \frac{3}{2}\,a > 0$ e $n_1 = \max\left\{1, \left\lceil \frac{2|b|}{a} \right\rceil\right\}$, si ha

            $$
            0 \le \frac{1}{2}\,a\;n \le a\;n + b \le \frac{3}{2}\,a\;n, \qquad \forall n \ge \max\left\{1, \left\lceil \frac{2\,|b|}{a} \right\rceil\right\}.
            $$

            Un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{a\;n + b}{n} = a + \lim_{n \to +\infty} \underbrace{\frac{b}{n}}_{\rr 0} = a \in \R_{>0}.
            $$

        4. Per dimostrare che $a\;n + b \neq \Theta(n^2)$, procediamo per assurdo e supponiamo che esistano $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^2 \le a\;n + b, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{a}{n} + \frac{b}{n^2}, \qquad \forall n \ge n_1.
            $$

            Passando al limite per $n \to +\infty$, otteniamo $0 < c_1 \le 0$, il che è impossibile: la disuguaglianza non può valere per $n$ arbitrariamente grande, poiché $c_1$ è una costante positiva.

<a id="esercizio-9-12"></a>

!!! esercizio "Esercizio 9.12: Notazione asintotica (E12)"

    Dati $a \in \R_{>0}$, $b \in \R$ e $c \in \R$, consideriamo la seguente funzione di variabile naturale asintoticamente non negativa:

    $$
    f: \N \rightarrow \R, \qquad f: n \mapsto a\;n^2 + b\;n + c.
    $$

    **Domande**

    1. Dimostrare, usando le definizioni, che per ogni $a \in \R_{>0}$, $b \in \R$ e $c \in \R$:

        1. $a\;n^2 + b\;n + c = \Theta(n^2)$;

        2. $a\;n^2 + b\;n + c \neq \Theta(n^3)$.

??? soluzione "Soluzione"

    1. 1. Per dimostrare che $a\;n^2 + b\;n + c = \Theta(n^2)$, determiniamo $c_1, c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^2 \le a\;n^2 + b\;n + c \le c_2\;n^2, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^2$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le a + \frac{b}{n} + \frac{c}{n^2} \le c_2, \qquad \forall n \ge n_1.
            $$

            Limitiamo separatamente i due termini $\frac{b}{n}$ e $\frac{c}{n^2}$.

            - Se $n \ge \frac{2\,|b|}{a}$, allora $\frac{|b|}{n} \le \frac{a}{2}$, quindi $-\frac{a}{2} \le \frac{b}{n} \le \frac{a}{2}$.

            - Se $n \ge 2\sqrt{\frac{|c|}{a}}$, allora $n^2 \ge \frac{4\,|c|}{a}$ e $\frac{|c|}{n^2} \le \frac{a}{4}$, quindi $-\frac{a}{4} \le \frac{c}{n^2} \le \frac{a}{4}$.

            Quindi, per ogni $n \ge 2\,\max\left\{\frac{|b|}{a}, \sqrt{\frac{|c|}{a}}\right\}$,

            $$
            0 < \underbrace{a - \frac{1}{2}\,a - \frac{1}{4}\,a}_{=\frac{1}{4}\,a} \le a + \frac{b}{n} + \frac{c}{n^2} \le \underbrace{a + \frac{1}{2}\,a + \frac{1}{4}\,a}_{=\frac{7}{4}\,a}.
            $$

            Quindi, scegliendo per esempio $c_1 = \frac{1}{4}\,a > 0$, $c_2 = \frac{7}{4}\,a > 0$ e

            $$
            n_1 = \max\left\{1, \left\lceil 2\,\max\left\{\frac{|b|}{a}, \sqrt{\frac{|c|}{a}}\right\} \right\rceil\right\},
            $$

            si ha

            $$
            0 \le \frac{1}{4}\,a\;n^2 \le a\;n^2 + b\;n + c \le \frac{7}{4}\,a\;n^2, \qquad \forall n \ge n_1.
            $$

            Un modo alternativo è calcolare il limite

            $$
            \lim_{n \to +\infty} \frac{a\;n^2 + b\;n + c}{n^2} = a + \lim_{n \to +\infty} \underbrace{\frac{b}{n}}_{\rr 0} + \lim_{n \to +\infty} \underbrace{\frac{c}{n^2}}_{\rr 0} = a \in \R_{>0}.
            $$

        2. Per dimostrare che $a\;n^2 + b\;n + c \neq \Theta(n^3)$, procediamo per assurdo e supponiamo che esistano $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1\;n^3 \le a\;n^2 + b\;n + c, \qquad \forall n \ge n_1.
            $$

            Con $n \ge 1$, dividendo per $n^3$ e poiché $c_1 > 0$, questo equivale a

            $$
            0 < c_1 \le \frac{a}{n} + \frac{b}{n^2} + \frac{c}{n^3}, \qquad \forall n \ge n_1.
            $$

            Passando al limite per $n \to +\infty$, otteniamo $0 < c_1 \le 0$, il che è impossibile: la disuguaglianza non può valere per $n$ arbitrariamente grande, poiché $c_1$ è una costante positiva.

<a id="esercizio-9-13"></a>

!!! esercizio "Esercizio 9.13: Notazione asintotica (E13)"

    Consideriamo quattro funzioni $f$, $g$, $p$ e $q$ di variabile naturale asintoticamente positive e le seguenti implicazioni:

    \begin{equation*}
    \label{eq:n13-prod}
    f(n)=\Theta\big(p(n)\big) \ \text{ e } \ g(n)=\Theta\big(q(n)\big) ~~\Longrightarrow~~ f(n) \cdot g(n) = \Theta\big( p(n) \cdot q(n) \big), \tag{9.1}
    \end{equation*}

    \begin{equation*}
    \label{eq:n13-sum}
    f(n)=\Theta\big(p(n)\big) \ \text{ e } \ g(n)=\Theta\big(q(n)\big) ~~\Longrightarrow~~ f(n) + g(n) = \Theta\big( p(n) + q(n) \big). \tag{9.2}
    \end{equation*}

    **Domande**

    1. Dimostrare che l'implicazione $\eqref{eq:n13-prod}$ è vera e scriverne la contronominale.

    2. Dimostrare che l'inversa dell'implicazione $\eqref{eq:n13-prod}$ non è vera, cioè

        $$
        f(n) \cdot g(n) = \Theta\big( p(n) \cdot q(n) \big) ~~\nRightarrow~~ f(n)=\Theta\big(p(n)\big) \ \text{ e } \ g(n)=\Theta\big(q(n)\big).
        $$

    3. Dimostrare che l'implicazione $\eqref{eq:n13-sum}$ è vera e scriverne la contronominale.

    4. Dimostrare che l'inversa dell'implicazione $\eqref{eq:n13-sum}$ non è vera, cioè

        $$
        f(n) + g(n) = \Theta\big( p(n) + q(n) \big) ~~\nRightarrow~~ f(n)=\Theta\big(p(n)\big) \ \text{ e } \ g(n)=\Theta\big(q(n)\big).
        $$

??? soluzione "Soluzione"

    1. Se $f(n)=\Theta\big(p(n)\big)$ e $g(n)=\Theta\big(q(n)\big)$, esistono $c_1,c_2 \in \R_{>0}$, $n_0\in \N$ e $c_3,c_4 \in \R_{>0}$, $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: p(n) \le f(n) \le c_2 \: p(n),~~ \forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le c_3 \: q(n) \le g(n) \le c_4 \: q(n),~~ \forall n \ge n_1.
        $$

        Poiché tutti i termini sono non negativi, possiamo moltiplicare termine a termine le due catene di disuguaglianze:

        $$
        0 \le \underbrace{c_1 \, c_3}_{>0} \: p(n) \: q(n) \le f(n)\cdot g(n) \le \underbrace{c_2 \, c_4}_{>0} \: p(n) \: q(n),\qquad \forall n \ge \max\{n_0,n_1\},
        $$

        e, di conseguenza, $f(n) \cdot g(n) = \Theta\big( p(n) \cdot q(n) \big)$.

        Ne segue che «$f(n)=\Theta\big(p(n)\big)$ e $g(n)=\Theta\big(q(n)\big)$» è una condizione sufficiente per «$f(n) \cdot g(n) = \Theta\big( p(n) \cdot q(n) \big)$», e quest'ultima è una condizione necessaria per la prima. Per contrapposizione di $\eqref{eq:n13-prod}$ si ha

        $$
        f(n) \cdot g(n) \neq \Theta\big( p(n) \cdot q(n) \big) ~~\Longrightarrow~~ f(n)\neq\Theta\big(p(n)\big) \ \text{ oppure } \ g(n)\neq\Theta\big(q(n)\big).
        $$

    2. Basta un controesempio. Siano

        $$
        f(n)= n^2 +1,\qquad g(n)= n^2 -1,\qquad p(n)= n,\qquad q(n)= n^3.
        $$

        Le quattro funzioni sono asintoticamente positive ($g(n) > 0$ per $n \ge 2$). Si ha

        $$
        f(n) \cdot g(n) = (n^2 +1) \, (n^2 -1) = n^4 - 1 \qquad\text{e}\qquad p(n) \cdot q(n) = n^4,
        $$

        e $n^4 - 1 = \Theta(n^4)$: scegliendo $c_1 = \frac{1}{2}$, $c_2 = 1$ e $n_1 = 2$, si ha $0 \le \frac{1}{2}\,n^4 \le n^4 - 1 \le n^4$ per ogni $n \ge 2$ (la limitazione inferiore equivale a $n^4 \ge 2$). D'altra parte,

        $$
        \lim_{n \to +\infty} \frac{n^2+1}{n} = +\infty \qquad\text{e}\qquad \lim_{n \to +\infty} \frac{n^2-1}{n^3} = 0^+,
        $$

        quindi $n^2 + 1 = \omega(n)$ e $n^2 - 1 = o(n^3)$; dunque

        $$
        n^2 +1 \neq \Theta(n) \qquad \text{e} \qquad n^2 -1 \neq \Theta(n^3)
        $$

        (una funzione che è $\omega(n)$ supera $c_2\,n$ per ogni costante $c_2$, e una funzione che è $o(n^3)$ è minore di $c_1\,n^3$ per ogni costante $c_1$, per ogni $n$ sufficientemente grande).

    3. Se $f(n)=\Theta\big(p(n)\big)$ e $g(n)=\Theta\big(q(n)\big)$, esistono $c_1,c_2 \in \R_{>0}$, $n_0\in \N$ e $c_3,c_4 \in \R_{>0}$, $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: p(n) \le f(n)\le c_2 \: p(n),~~ \forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le c_3 \: q(n) \le g(n)\le c_4 \: q(n),~~ \forall n \ge n_1.
        $$

        Sommando le due catene di disuguaglianze, otteniamo

        $$
        0 \le c_1 \: p(n) + c_3 \: q(n) \le f(n) + g(n) \le c_2 \: p(n) + c_4 \: q(n),\qquad \forall n \ge \max\{n_0,n_1\}.
        $$

        Poiché $p(n) \ge 0$ e $q(n) \ge 0$ per questi valori di $n$, ciò implica

        $$
        0 \le \underbrace{\min\{c_1,c_3\}}_{> 0} \big( p(n) + q(n) \big) \le f(n) + g(n) \le \underbrace{\max\{c_2,c_4\}}_{> 0} \big( p(n) + q(n) \big),\qquad \forall n \ge \max\{n_0,n_1\},
        $$

        e, di conseguenza, $f(n) + g(n) =\Theta\big( p(n) + q(n) \big)$.

        Ne segue che «$f(n)=\Theta\big(p(n)\big)$ e $g(n)=\Theta\big(q(n)\big)$» è una condizione sufficiente per «$f(n) + g(n) = \Theta\big( p(n) + q(n) \big)$», e quest'ultima è una condizione necessaria per la prima. Per contrapposizione di $\eqref{eq:n13-sum}$ si ha

        $$
        f(n) + g(n) \neq \Theta\big( p(n) + q(n) \big) ~~\Longrightarrow~~ f(n)\neq\Theta\big(p(n)\big) \ \text{ oppure } \ g(n)\neq\Theta\big(q(n)\big).
        $$

    4. Basta un controesempio. Siano

        $$
        f(n)= 5\;n^3,\qquad g(n)= 7\;n,\qquad p(n)= n^3,\qquad q(n)= n^2.
        $$

        Si ha $5\;n^3 + 7\;n = \Theta( n^3 + n^2)$: scegliendo $c_1 = \frac{5}{2}$, $c_2 = 7$ e $n_1 = 1$, si ha

        $$
        0 \le \frac{5}{2}\,(n^3 + n^2) \le 5\;n^3 + 7\;n \le 7\,(n^3 + n^2), \qquad \forall n \ge 1,
        $$

        poiché $\frac{5}{2}\,(n^3 + n^2) \le \frac{5}{2} \cdot 2\,n^3 = 5\,n^3$ e $7\,n \le 2\,n^3 + 7\,n^2$ per $n \ge 1$. D'altra parte, $5\;n^3 = \Theta(n^3)$ (con $c_1 = c_2 = 5$), ma

        $$
        \lim_{n \to +\infty} \frac{7\,n}{n^2} = 0^+,
        $$

        quindi $7\;n = o(n^2)$ e perciò $7\;n \neq \Theta(n^2)$.

<a id="esercizio-9-14"></a>

!!! esercizio "Esercizio 9.14: Notazione asintotica (E14)"

    Consideriamo due funzioni $f$ e $g$ di variabile naturale asintoticamente non negative e le seguenti equivalenze:

    \begin{align*}
    \label{eq:n14-a}
    &f(n)= \Theta\big(g(n)\big) ~~\Longleftrightarrow~~ f(n)= \bigO\big(g(n)\big) \ \text{ e } \ f(n)= \Omega\big(g(n)\big), \tag{9.3}\\[1ex]
    \label{eq:n14-b}
    &f(n)= \bigO\big(g(n)\big) ~~\Longleftrightarrow~~ g(n)= \Omega\big(f(n)\big), \tag{9.4}\\[1ex]
    \label{eq:n14-c}
    &f(n)= o\big(g(n)\big) ~~\Longleftrightarrow~~ g(n)= \omega\big(f(n)\big), \tag{9.5}\\[1ex]
    \label{eq:n14-d}
    &f(n)= \Theta\big(g(n)\big) ~~\Longleftrightarrow~~ g(n)= \Theta\big(f(n)\big). \tag{9.6}
    \end{align*}

    **Domande**

    1. Dimostrare che l'equivalenza $\eqref{eq:n14-a}$ è vera.

    2. Dimostrare che l'equivalenza $\eqref{eq:n14-b}$ è vera.

    3. Dimostrare che l'equivalenza $\eqref{eq:n14-c}$ è vera.

    4. Dimostrare che l'equivalenza $\eqref{eq:n14-d}$ è vera.

??? soluzione "Soluzione"

    1. Se $f(n)= \Theta\big(g(n)\big)$, esistono $c_1,c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: g(n) \le f(n)\le c_2 \: g(n),\qquad\forall n \ge n_1,
        $$

        e quindi

        $$
        0 \le f(n)\le c_2 \: g(n), ~~\forall n \ge n_1 ~~\Longrightarrow~~ f(n)= \bigO\big(g(n)\big),
        $$

        $$
        0 \le c_1 \: g(n) \le f(n), ~~\forall n \ge n_1 ~~\Longrightarrow~~ f(n)= \Omega\big(g(n)\big).
        $$

        Viceversa, se $f(n)= \Omega\big(g(n)\big)$, esistono $c_1 \in \R_{>0}$ e $n_1 \in \N$ tali che $0 \le c_1 \: g(n) \le f(n)$ per ogni $n \ge n_1$, e se $f(n)= \bigO\big(g(n)\big)$, esistono $c_2 \in \R_{>0}$ e $n_2 \in \N$ tali che $0 \le f(n) \le c_2 \: g(n)$ per ogni $n \ge n_2$. Combinando le due disuguaglianze, si ha

        $$
        0 \le c_1 \: g(n) \le f(n)\le c_2 \: g(n),\qquad\forall n \ge \max\{n_1, n_2\} ~~\Longrightarrow~~ f(n)= \Theta\big(g(n)\big).
        $$

        Ne segue che «$f(n) = \Theta\big(g(n)\big)$» è una condizione necessaria e sufficiente per «$f(n)= \bigO\big(g(n)\big)$ e $f(n)= \Omega\big(g(n)\big)$».

    2. 1. Se $f(n)= \bigO\big(g(n)\big)$, esistono $c \in \R_{>0}$ e $n_1 \in \N$ tali che $0 \le f(n)\le c \: g(n)$ per ogni $n \ge n_1$. Dividendo per $c > 0$,

            $$
            0 \le \frac{1}{c}\, f(n)\le g(n), \qquad\forall n \ge n_1 ~~\Longrightarrow~~ g(n)= \Omega\big(f(n)\big),
            $$

            con la costante $\frac{1}{c} > 0$.

        2. Se $g(n)= \Omega\big(f(n)\big)$, esistono $c \in \R_{>0}$ e $n_1 \in \N$ tali che $0 \le c \; f(n)\le g(n)$ per ogni $n \ge n_1$. Dividendo per $c > 0$,

            $$
            0 \le f(n)\le \frac{1}{c} \: g(n), \qquad\forall n \ge n_1 ~~\Longrightarrow~~ f(n)= \bigO\big(g(n)\big).
            $$

        Ne segue che «$f(n)= \bigO\big(g(n)\big)$» è una condizione necessaria e sufficiente per «$g(n)= \Omega\big(f(n)\big)$».

    3. 1. Sia $f(n)= o\big(g(n)\big)$. Per dimostrare che $g(n)= \omega\big(f(n)\big)$, fissiamo $c \in \R_{>0}$. Per la definizione di $f(n)= o\big(g(n)\big)$ con la costante $\frac{1}{c} > 0$, esiste $n_1 \in \N$ tale che

            $$
            0 \le f(n) < \frac{1}{c}\, g(n),\qquad\forall n \ge n_1 ~~\Longrightarrow~~ 0 \le c\, f(n) < g(n), \qquad\forall n \ge n_1.
            $$

            Poiché $c$ è arbitraria, $g(n)= \omega\big(f(n)\big)$.

        2. Sia $g(n)= \omega\big(f(n)\big)$. Per dimostrare che $f(n)= o\big(g(n)\big)$, fissiamo $c \in \R_{>0}$. Per la definizione di $g(n)= \omega\big(f(n)\big)$ con la costante $\frac{1}{c} > 0$, esiste $n_1 \in \N$ tale che

            $$
            0 \le \frac{1}{c}\, f(n) < g(n),\qquad\forall n \ge n_1 ~~\Longrightarrow~~ 0 \le f(n) < c\, g(n), \qquad\forall n \ge n_1.
            $$

            Poiché $c$ è arbitraria, $f(n)= o\big(g(n)\big)$.

        Ne segue che «$f(n)= o\big(g(n)\big)$» è una condizione necessaria e sufficiente per «$g(n)= \omega\big(f(n)\big)$».

    4. 1. Se $f(n)= \Theta\big(g(n)\big)$, esistono $c_1,c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

            $$
            0 \le c_1 \: g(n) \le f(n) \le c_2 \: g(n),\qquad\forall n \ge n_1.
            $$

            Dividendo la disuguaglianza di sinistra per $c_1$ e quella di destra per $c_2$, otteniamo

            $$
            0 \le \frac{1}{c_2}\: f(n) \le g(n) \le \frac{1}{c_1}\: f(n),\qquad\forall n \ge n_1.
            $$

            Poiché $\frac{1}{c_2} > 0$ e $\frac{1}{c_1} > 0$, questo dimostra che $g(n)= \Theta\big(f(n)\big)$.

        2. Se $g(n)= \Theta\big(f(n)\big)$, lo stesso argomento, con i ruoli di $f$ e $g$ scambiati, dà $f(n)= \Theta\big(g(n)\big)$.

        Ne segue che «$f(n)= \Theta\big(g(n)\big)$» è una condizione necessaria e sufficiente per «$g(n)= \Theta\big(f(n)\big)$».

<a id="esercizio-9-15"></a>

!!! esercizio "Esercizio 9.15: Notazione asintotica (E15)"

    Consideriamo tre funzioni $f$, $g$ e $h$ di variabile naturale asintoticamente non negative e le seguenti implicazioni (<strong>transitività</strong>):

    \begin{align*}
    \label{eq:n15-1}
    &f(n)= \Theta\big(g(n)\big) \ \text{ e } \ g(n) = \Theta\big(h(n)\big) ~~\Longrightarrow~~ f(n)= \Theta\big(h(n)\big), \tag{9.7}\\[1ex]
    \label{eq:n15-2}
    &f(n)= \bigO\big(g(n)\big) \ \text{ e } \ g(n) = \bigO\big(h(n)\big) ~~\Longrightarrow~~ f(n)= \bigO\big(h(n)\big), \tag{9.8}\\[1ex]
    \label{eq:n15-3}
    &f(n)= \Omega\big(g(n)\big) \ \text{ e } \ g(n) = \Omega\big(h(n)\big) ~~\Longrightarrow~~ f(n)= \Omega\big(h(n)\big), \tag{9.9}\\[1ex]
    \label{eq:n15-4}
    &f(n)= o\big(g(n)\big) \ \text{ e } \ g(n) = o\big(h(n)\big) ~~\Longrightarrow~~ f(n)= o\big(h(n)\big), \tag{9.10}\\[1ex]
    \label{eq:n15-5}
    &f(n)= \omega\big(g(n)\big) \ \text{ e } \ g(n) = \omega\big(h(n)\big) ~~\Longrightarrow~~ f(n)= \omega\big(h(n)\big). \tag{9.11}
    \end{align*}

    **Domande**

    1. Dimostrare che l'implicazione $\eqref{eq:n15-1}$ è vera e scriverne la contronominale.

    2. Dimostrare che l'implicazione $\eqref{eq:n15-2}$ è vera e scriverne la contronominale.

    3. Dimostrare che l'implicazione $\eqref{eq:n15-3}$ è vera e scriverne la contronominale.

    4. Dimostrare che l'implicazione $\eqref{eq:n15-4}$ è vera e scriverne la contronominale.

    5. Dimostrare che l'implicazione $\eqref{eq:n15-5}$ è vera e scriverne la contronominale.

??? soluzione "Soluzione"

    1. Se $f(n)=\Theta\big(g(n)\big)$ e $g(n)=\Theta\big(h(n)\big)$, esistono $c_1,c_2 \in \R_{>0}$, $n_0 \in \N$ e $c_3,c_4 \in \R_{>0}$, $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: g(n) \le f(n) \le c_2 \: g(n),~~\forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le c_3 \: h(n) \le g(n) \le c_4 \: h(n),~~\forall n \ge n_1.
        $$

        Ne segue che, per ogni $n \ge \max\{n_0,n_1\}$,

        $$
        f(n) \ge c_1 \: g(n) \ge c_1 \, c_3 \: h(n)
        \qquad\text{e}\qquad
        f(n) \le c_2 \: g(n) \le c_2 \, c_4 \: h(n),
        $$

        quindi

        $$
        0 \le \underbrace{c_1 c_3}_{>0} \: h(n) \le f(n) \le \underbrace{c_2 c_4}_{>0} \: h(n),\qquad\forall n \ge \max\{n_0,n_1\},
        $$

        che dimostra $f(n)=\Theta\big(h(n)\big)$. Per contrapposizione di $\eqref{eq:n15-1}$:

        $$
        f(n) \neq \Theta\big(h(n)\big) ~~\Longrightarrow~~ f(n)\neq\Theta\big(g(n)\big) \ \text{ oppure } \ g(n)\neq\Theta\big(h(n)\big).
        $$

    2. Se $f(n)=\bigO\big(g(n)\big)$ e $g(n)=\bigO\big(h(n)\big)$, esistono $c_1 \in \R_{>0}$, $n_0 \in \N$ e $c_2 \in \R_{>0}$, $n_1 \in \N$ tali che

        $$
        0 \le f(n) \le c_1 \: g(n),~~\forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le g(n) \le c_2 \: h(n),~~\forall n \ge n_1.
        $$

        Ne segue che

        $$
        0 \le f(n) \le c_1 \: g(n) \le \underbrace{c_1 c_2}_{>0} \: h(n),\qquad\forall n \ge \max\{n_0,n_1\},
        $$

        che dimostra $f(n)=\bigO\big(h(n)\big)$. Per contrapposizione di $\eqref{eq:n15-2}$:

        $$
        f(n) \neq \bigO\big(h(n)\big) ~~\Longrightarrow~~ f(n)\neq \bigO\big(g(n)\big) \ \text{ oppure } \ g(n)\neq \bigO\big(h(n)\big).
        $$

    3. Se $f(n)=\Omega\big(g(n)\big)$ e $g(n)=\Omega\big(h(n)\big)$, esistono $c_1 \in \R_{>0}$, $n_0 \in \N$ e $c_2 \in \R_{>0}$, $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: g(n) \le f(n),~~\forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le c_2 \: h(n) \le g(n),~~\forall n \ge n_1.
        $$

        Ne segue che

        $$
        0 \le \underbrace{c_1 c_2}_{>0} \: h(n) \le c_1 \: g(n) \le f(n),\qquad\forall n \ge \max\{n_0,n_1\},
        $$

        che dimostra $f(n)=\Omega\big(h(n)\big)$. Per contrapposizione di $\eqref{eq:n15-3}$:

        $$
        f(n) \neq \Omega\big(h(n)\big) ~~\Longrightarrow~~ f(n)\neq\Omega\big(g(n)\big) \ \text{ oppure } \ g(n)\neq\Omega\big(h(n)\big).
        $$

    4. Siano $f(n)=o\big(g(n)\big)$ e $g(n)=o\big(h(n)\big)$, e sia $c \in \R_{>0}$. Per la definizione di $f(n)=o\big(g(n)\big)$ con la costante $1$, e per la definizione di $g(n)=o\big(h(n)\big)$ con la costante $c$, esistono $n_0,n_1 \in \N$ tali che

        $$
        0 \le f(n) < g(n),~~\forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le g(n) < c \: h(n),~~\forall n \ge n_1.
        $$

        Ne segue che

        $$
        0 \le f(n) < g(n) < c \: h(n),\qquad\forall n \ge \max\{n_0,n_1\},
        $$

        cioè $0 \le f(n) < c \: h(n)$. Poiché $c \in \R_{>0}$ è arbitraria, questo dimostra $f(n)=o\big(h(n)\big)$. Per contrapposizione di $\eqref{eq:n15-4}$:

        $$
        f(n) \neq o\big(h(n)\big) ~~\Longrightarrow~~ f(n)\neq o\big(g(n)\big) \ \text{ oppure } \ g(n)\neq o\big(h(n)\big).
        $$

    5. Siano $f(n)=\omega\big(g(n)\big)$ e $g(n)=\omega\big(h(n)\big)$, e sia $c \in \R_{>0}$. Per la definizione di $f(n)=\omega\big(g(n)\big)$ con la costante $1$, e per la definizione di $g(n)=\omega\big(h(n)\big)$ con la costante $c$, esistono $n_0,n_1 \in \N$ tali che

        $$
        0 \le g(n) < f(n),~~\forall n \ge n_0
        \qquad\text{e}\qquad
        0 \le c \: h(n) < g(n),~~\forall n \ge n_1.
        $$

        Ne segue che

        $$
        0 \le c \: h(n) < g(n) < f(n),\qquad\forall n \ge \max\{n_0,n_1\},
        $$

        cioè $0 \le c \: h(n) < f(n)$. Poiché $c \in \R_{>0}$ è arbitraria, questo dimostra $f(n)=\omega\big(h(n)\big)$. Per contrapposizione di $\eqref{eq:n15-5}$:

        $$
        f(n) \neq \omega\big(h(n)\big) ~~\Longrightarrow~~ f(n)\neq\omega\big(g(n)\big) \ \text{ oppure } \ g(n)\neq\omega\big(h(n)\big).
        $$

<a id="esercizio-9-16"></a>

!!! esercizio "Esercizio 9.16: Notazione asintotica (E16)"

    Consideriamo una funzione $f$ di variabile naturale asintoticamente non negativa e le seguenti proprietà di <strong>riflessività</strong>:

    \begin{align*}
    \label{eq:n16-1}
    &f(n)= \Theta\big(f(n)\big), \tag{9.12}\\[1ex]
    \label{eq:n16-2}
    &f(n)= \bigO\big(f(n)\big), \tag{9.13}\\[1ex]
    \label{eq:n16-3}
    &f(n)= \Omega\big(f(n)\big). \tag{9.14}
    \end{align*}

    **Domande**

    1. Dimostrare che la proprietà $\eqref{eq:n16-1}$ è vera.

    2. Dimostrare che la proprietà $\eqref{eq:n16-2}$ è vera.

    3. Dimostrare che la proprietà $\eqref{eq:n16-3}$ è vera.

??? soluzione "Soluzione"

    Poiché $f$ è asintoticamente non negativa, esiste $\tilde n \in \N$ tale che $f(n) \ge 0$ per ogni $n \ge \tilde n$. Nelle tre dimostrazioni usiamo $n_1 = \tilde n$.

    1. Per dimostrare che $f(n)= \Theta\big(f(n)\big)$, determiniamo $c_1,c_2 \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c_1 \: f(n) \le f(n) \le c_2 \: f(n), \qquad \forall n \ge n_1.
        $$

        Per $n \ge \tilde n$ la disuguaglianza $0 \le 1 \cdot f(n) \le f(n) \le 1 \cdot f(n)$ vale banalmente. Scegliendo $c_1 = 1$, $c_2 = 1$ e $n_1 = \tilde n$, si ha

        $$
        0 \le f(n) \le f(n) \le f(n), \qquad \forall n \ge \tilde n,
        $$

        che dimostra $f(n)= \Theta\big(f(n)\big)$.

    2. Per dimostrare che $f(n)= \bigO\big(f(n)\big)$, determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le f(n) \le c \: f(n), \qquad \forall n \ge n_1.
        $$

        Scegliendo $c = 1$ e $n_1 = \tilde n$, si ha $0 \le f(n) \le f(n)$ per ogni $n \ge \tilde n$, il che dimostra $f(n)= \bigO\big(f(n)\big)$.

    3. Per dimostrare che $f(n)= \Omega\big(f(n)\big)$, determiniamo $c \in \R_{>0}$ e $n_1 \in \N$ tali che

        $$
        0 \le c \: f(n) \le f(n), \qquad \forall n \ge n_1.
        $$

        Scegliendo $c = 1$ e $n_1 = \tilde n$, si ha $0 \le f(n) \le f(n)$ per ogni $n \ge \tilde n$, il che dimostra $f(n)= \Omega\big(f(n)\big)$.

    Osserviamo che l'ipotesi su $f$ è necessaria: se $f(n) < 0$ per infiniti $n$, la disuguaglianza $0 \le f(n)$ richiesta dalle tre definizioni non vale per $n$ arbitrariamente grande, e nessuna delle tre proprietà vale.
