---
title: "Esercizi · Introduzione a Python"
---

# Esercizi · Introduzione a Python

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 7** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 7: Introduzione a Python](../linguaggi/07-introduzione-python.md) · [:material-file-pdf-box: Eserciziario, volume 2 (PDF)](../pdf/esercizi-2-linguaggi-di-programmazione.pdf)

</div>

Negli esercizi di questo capitolo i programmi sono scritti ed eseguiti con le convenzioni del capitolo «Introduzione a <code>Python</code>», riassunte qui sotto.

??? codice "Codice"

    - Il programma di un esercizio è salvato in un file <code>&lt;name&gt;.py</code> ed eseguito con il comando

        ```text
        python3 <name>.py
        ```

    - Le istanze di test sono liste scritte nel codice, ad esempio <code>arr1 = [9, 12, 3, 16, 19, 11, 12]</code>, e sono passate alle funzioni senza la loro dimensione: una funzione ottiene la dimensione $n$ di una lista <code>a</code> con <code>len(a)</code>.

    - Gli elementi di una lista di dimensione $n$ sono <code>a[0]</code>, <code>a[1]</code>, …, <code>a[n-1]</code>: la componente $a[i]$ di un'istanza scritta come $a = [\dots]$ nel testo corrisponde ad <code>a[i-1]</code> nel codice, e gli indici stampati dai programmi partono da $0$.

    - Le istruzioni principali sono scritte nel blocco <code>if \_\_name\_\_ == "\_\_main\_\_":</code>; una lista si stampa con <code>print</code>, che la visualizza fra parentesi quadre.

    - I risultati che una funzione deve restituire insieme sono restituiti come una tupla (<code>return x, y</code>) e ricevuti con un assegnamento multiplo (<code>x, y = f(a)</code>).

    - Il formato <code>:.4f</code> dentro una f-string visualizza un numero in virgola mobile con esattamente $4$ cifre dopo la virgola decimale.

<a id="esercizio-7-1"></a>

!!! esercizio "Esercizio 7.1: Introduzione a {\tt Python} (E1)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il valore massimo nell'array.

    **Domande**

    1. Scrivere un programma <code>Python</code> completo che trova il valore massimo in una lista $a$ di $n$ numeri interi. Il programma deve:

        - definire una funzione <code>array\_max\_value(a)</code> che implementa l'algoritmo;

        - nel blocco <code>\_\_main\_\_</code>, creare le liste di test e chiamare la funzione;

        - stampare i risultati per ogni caso di test.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare il comando che esegue il programma e l'output per tutti i casi di test.

    3. Modificare la funzione in modo che restituisca sia il valore massimo sia il suo indice nella lista. Eseguire la versione modificata sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Python</code> completo:</strong>

        ```python
        def array_max_value(a):
            """Trova e restituisce il valore massimo della lista a."""
            max_val = a[0]  # Inizializza con il primo elemento

            for i in range(1, len(a)):
                if a[i] > max_val:
                    max_val = a[i]  # Aggiorna il massimo

            return max_val

        if __name__ == "__main__":
            # Caso di prova 1
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            print(f"Prova 1 - Lista: {arr1}")
            print(f"Valore massimo: {array_max_value(arr1)}")
            print()

            # Caso di prova 2
            arr2 = [5, 2, 8, 1]
            print(f"Prova 2 - Lista: {arr2}")
            print(f"Valore massimo: {array_max_value(arr2)}")
            print()

            # Caso di prova 3
            arr3 = [42]
            print(f"Prova 3 - Lista: {arr3}")
            print(f"Valore massimo: {array_max_value(arr3)}")
        ```

        Per l'Istanza 3 il ciclo <code>for i in range(1, 1)</code> non esegue nessuna iterazione, e la funzione restituisce l'unico elemento <code>a[0]</code>.

    2. <strong>Esecuzione.</strong> Se il programma è salvato nel file <code>max\_value.py</code>, lo si esegue con il comando

        ```text
        python3 max_value.py
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Lista: [9, 12, 3, 16, 19, 11, 12]
        Valore massimo: 19

        Prova 2 - Lista: [5, 2, 8, 1]
        Valore massimo: 8

        Prova 3 - Lista: [42]
        Valore massimo: 42
        ```

    3. <strong>Funzione modificata che restituisce il valore massimo e il suo indice:</strong>

        ```python
        def array_max_value_with_index(a):
            """Restituisce (valore_massimo, indice) dell'elemento massimo della lista a."""
            max_val = a[0]
            idx = 0

            for i in range(1, len(a)):
                if a[i] > max_val:
                    max_val = a[i]
                    idx = i  # Memorizza l'indice

            return max_val, idx

        if __name__ == "__main__":
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            max_val, idx = array_max_value_with_index(arr1)
            print(f"Valore massimo: {max_val}, all'indice: {idx}")
        ```

        <strong>Output:</strong>

        ```text
        Valore massimo: 19, all'indice: 4
        ```

        Per l'Istanza 1 la funzione restituisce la tupla $(19,\ 4)$: il valore massimo $19$ è all'indice $4$ della lista (indici da $0$), cioè nella posizione $5$ dell'array $a[1..7]$ del testo. Se il valore massimo compare più volte, la funzione restituisce l'indice della sua prima occorrenza, perché <code>max\_val</code> e <code>idx</code> sono aggiornati solo quando <code>a[i] &gt; max\_val</code> (disuguaglianza stretta).

<a id="esercizio-7-2"></a>

!!! esercizio "Esercizio 7.2: Introduzione a {\tt Python} (E2)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il valore minimo nell'array.

    **Domande**

    1. Scrivere un programma <code>Python</code> completo che trova il valore minimo in una lista $a$ di $n$ numeri interi. Il programma deve:

        - definire una funzione <code>array\_min\_value(a)</code> che implementa l'algoritmo;

        - nel blocco <code>\_\_main\_\_</code>, creare le liste di test e chiamare la funzione;

        - stampare i risultati per ogni caso di test.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare il comando che esegue il programma e l'output per tutti i casi di test.

    3. Modificare la funzione in modo che restituisca sia il valore minimo sia il suo indice nella lista. Eseguire la versione modificata sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Python</code> completo:</strong>

        ```python
        def array_min_value(a):
            """Trova e restituisce il valore minimo della lista a."""
            min_val = a[0]  # Inizializza con il primo elemento

            for i in range(1, len(a)):
                if a[i] < min_val:
                    min_val = a[i]  # Aggiorna il minimo

            return min_val

        if __name__ == "__main__":
            # Caso di prova 1
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            print(f"Prova 1 - Lista: {arr1}")
            print(f"Valore minimo: {array_min_value(arr1)}")
            print()

            # Caso di prova 2
            arr2 = [5, 2, 8, 1]
            print(f"Prova 2 - Lista: {arr2}")
            print(f"Valore minimo: {array_min_value(arr2)}")
            print()

            # Caso di prova 3
            arr3 = [42]
            print(f"Prova 3 - Lista: {arr3}")
            print(f"Valore minimo: {array_min_value(arr3)}")
        ```

        Per l'Istanza 3 il ciclo <code>for i in range(1, 1)</code> non esegue nessuna iterazione, e la funzione restituisce l'unico elemento <code>a[0]</code>.

    2. <strong>Esecuzione.</strong> Se il programma è salvato nel file <code>min\_value.py</code>, lo si esegue con il comando

        ```text
        python3 min_value.py
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Lista: [9, 12, 3, 16, 19, 11, 12]
        Valore minimo: 3

        Prova 2 - Lista: [5, 2, 8, 1]
        Valore minimo: 1

        Prova 3 - Lista: [42]
        Valore minimo: 42
        ```

    3. <strong>Funzione modificata che restituisce il valore minimo e il suo indice:</strong>

        ```python
        def array_min_value_with_index(a):
            """Restituisce (valore_minimo, indice) dell'elemento minimo della lista a."""
            min_val = a[0]
            idx = 0

            for i in range(1, len(a)):
                if a[i] < min_val:
                    min_val = a[i]
                    idx = i  # Memorizza l'indice

            return min_val, idx

        if __name__ == "__main__":
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            min_val, idx = array_min_value_with_index(arr1)
            print(f"Valore minimo: {min_val}, all'indice: {idx}")
        ```

        <strong>Output:</strong>

        ```text
        Valore minimo: 3, all'indice: 2
        ```

        Per l'Istanza 1 la funzione restituisce la tupla $(3,\ 2)$: il valore minimo $3$ è all'indice $2$ della lista (indici da $0$), cioè nella posizione $3$ dell'array $a[1..7]$ del testo. Se il valore minimo compare più volte, la funzione restituisce l'indice della sua prima occorrenza, perché <code>min\_val</code> e <code>idx</code> sono aggiornati solo quando <code>a[i] &lt; min\_val</code> (disuguaglianza stretta).

<a id="esercizio-7-3"></a>

!!! esercizio "Esercizio 7.3: Introduzione a {\tt Python} (E3)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare la somma e la media di tutti i suoi elementi.

    **Domande**

    1. Scrivere un programma <code>Python</code> completo che calcola la somma e la media degli elementi di una lista $a$ di $n$ numeri interi. Il programma deve:

        - definire una funzione <code>array\_sum(a)</code> che restituisce la somma di tutti gli elementi;

        - definire una funzione <code>array\_average(a)</code> che restituisce la media di tutti gli elementi;

        - nel blocco <code>\_\_main\_\_</code>, creare le liste di test, chiamare entrambe le funzioni e stampare i risultati, con la media arrotondata a $4$ cifre decimali.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare il comando che esegue il programma e l'output per tutti i casi di test.

    3. Riunire le due funzioni in un'unica funzione <code>array\_sum\_and\_average(a)</code> che restituisce sia la somma sia la media come una tupla. Eseguirla sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Python</code> completo:</strong>

        ```python
        def array_sum(a):
            """Calcola e restituisce la somma di tutti gli elementi della lista a."""
            total = 0
            for x in a:
                total += x
            return total

        def array_average(a):
            """Calcola e restituisce la media di tutti gli elementi della lista a."""
            return array_sum(a) / len(a)

        if __name__ == "__main__":
            # Caso di prova 1
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            print(f"Prova 1 - Lista: {arr1}")
            print(f"Somma: {array_sum(arr1)}")
            print(f"Media: {array_average(arr1):.4f}")
            print()

            # Caso di prova 2
            arr2 = [5, 2, 8, 1]
            print(f"Prova 2 - Lista: {arr2}")
            print(f"Somma: {array_sum(arr2)}")
            print(f"Media: {array_average(arr2):.4f}")
            print()

            # Caso di prova 3
            arr3 = [42]
            print(f"Prova 3 - Lista: {arr3}")
            print(f"Somma: {array_sum(arr3)}")
            print(f"Media: {array_average(arr3):.4f}")
        ```

        Il ciclo <code>for x in a</code> visita direttamente gli elementi della lista. L'operatore <code>/</code> restituisce sempre un <code>float</code>, quindi non serve alcuna conversione di tipo (in <code>C++</code> la somma deve essere convertita in <code>double</code> prima della divisione). La funzione <code>array\_average</code> richiede $n \ge 1$: per una lista vuota la divisione per <code>len(a)</code> $= 0$ ferma il programma con una <code>ZeroDivisionError</code>.

    2. <strong>Esecuzione.</strong> Se il programma è salvato nel file <code>array\_sum.py</code>, lo si esegue con il comando

        ```text
        python3 array_sum.py
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Lista: [9, 12, 3, 16, 19, 11, 12]
        Somma: 82
        Media: 11.7143

        Prova 2 - Lista: [5, 2, 8, 1]
        Somma: 16
        Media: 4.0000

        Prova 3 - Lista: [42]
        Somma: 42
        Media: 42.0000
        ```

        Per l'Istanza 1 la media esatta è $82/7 = 11.714285\ldots$, visualizzata come $11.7143$.

    3. <strong>Funzione combinata:</strong>

        ```python
        def array_sum_and_average(a):
            """Restituisce (somma, media) della lista a."""
            total = 0
            for x in a:
                total += x
            avg = total / len(a)
            return total, avg

        if __name__ == "__main__":
            arr1 = [9, 12, 3, 16, 19, 11, 12]
            s, avg = array_sum_and_average(arr1)
            print(f"Somma: {s}, Media: {avg:.4f}")
        ```

        <strong>Output:</strong>

        ```text
        Somma: 82, Media: 11.7143
        ```

        La funzione combinata visita la lista una sola volta, mentre <code>array\_average</code> del primo programma chiama <code>array\_sum</code> e visita la lista una seconda volta.

<a id="esercizio-7-4"></a>

!!! esercizio "Esercizio 7.4: Introduzione a {\tt Python} (E4)"

    Dato un array $a$ di $n$ numeri interi e un valore $m$, consideriamo il problema di determinare se il valore $m$ è presente o no nell'array.

    **Domande**

    1. Scrivere un programma <code>Python</code> completo che esegue una <strong>ricerca lineare</strong> in una lista $a$. Il programma deve:

        - definire una funzione <code>linear\_search(a, m)</code> che cerca il valore <code>m</code> nella lista <code>a</code>;

        - restituire l'indice della prima occorrenza di <code>m</code> se viene trovato, oppure <code>-1</code> se non viene trovato;

        - nel blocco <code>\_\_main\_\_</code>, eseguire i casi di test e stampare i risultati.

    2. Eseguire il programma sulla lista $a = [9, 12, 3, 16, 19, 11, 12]$ con i seguenti valori:

        - $m = 16$ (presente nella lista)

        - $m = 12$ (presente due volte: si restituisce l'indice della prima occorrenza)

        - $m = 7$ (non presente nella lista)

        Mostrare il comando che esegue il programma e l'output per tutti i casi di test.

    3. Modificare la funzione in modo che restituisca la <strong>lista di tutti gli indici</strong> in cui compare il valore $m$ (invece della sola prima occorrenza). Eseguirla con $m = 12$ e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Python</code> completo:</strong>

        ```python
        def linear_search(a, m):
            """Cerca il valore m nella lista a.
            Restituisce l'indice della prima occorrenza, oppure -1 se non è presente."""
            for i in range(len(a)):
                if a[i] == m:
                    return i  # Trovato: restituisce l'indice
            return -1         # Non trovato

        def print_result(a, m):
            """Cerca m in a e stampa il risultato."""
            idx = linear_search(a, m)
            if idx != -1:
                print(f"Valore {m} trovato all'indice {idx}")
            else:
                print(f"Valore {m} non trovato")

        if __name__ == "__main__":
            a = [9, 12, 3, 16, 19, 11, 12]
            print(f"Lista: {a}")
            print()

            print_result(a, 16)
            print_result(a, 12)
            print_result(a, 7)
        ```

        L'istruzione <code>return i</code> termina la funzione, e quindi il ciclo, alla prima occorrenza di <code>m</code>; l'istruzione <code>return -1</code> viene raggiunta solo quando il ciclo ha visitato l'intera lista senza trovare <code>m</code>. Si usa il valore <code>-1</code> perché non può essere un indice della lista. La funzione ausiliaria <code>print\_result</code> evita di scrivere tre volte le stesse istruzioni.

    2. <strong>Esecuzione.</strong> Se il programma è salvato nel file <code>linear\_search.py</code>, lo si esegue con il comando

        ```text
        python3 linear_search.py
        ```

        <strong>Output:</strong>

        ```text
        Lista: [9, 12, 3, 16, 19, 11, 12]

        Valore 16 trovato all'indice 3
        Valore 12 trovato all'indice 1
        Valore 7 non trovato
        ```

        Il valore $12$ si trova negli indici $1$ e $6$, e la funzione restituisce il primo. Nell'array $a[1..7]$ del testo, gli indici $3$ e $1$ corrispondono alle posizioni $4$ e $2$.

    3. <strong>Funzione che restituisce tutte le occorrenze:</strong>

        ```python
        def linear_search_all(a, m):
            """Restituisce la lista di tutti gli indici in cui il valore m compare in a.
            Restituisce una lista vuota se m non è presente."""
            indices = []
            for i in range(len(a)):
                if a[i] == m:
                    indices.append(i)
            return indices

        if __name__ == "__main__":
            a = [9, 12, 3, 16, 19, 11, 12]

            m = 12
            result = linear_search_all(a, m)
            if result:  # Una lista non vuota è vera, una lista vuota è falsa
                print(f"Valore {m} trovato agli indici: {result}")
            else:
                print(f"Valore {m} non trovato")
        ```

        <strong>Output:</strong>

        ```text
        Valore 12 trovato agli indici: [1, 6]
        ```

        A differenza di <code>linear\_search</code>, questa funzione visita sempre l'intera lista, perché non può fermarsi alla prima occorrenza. La lista <code>indices</code> parte vuota e cresce con <code>append</code>; quando è usata come condizione, una lista vuota vale <code>False</code>.

<a id="esercizio-7-5"></a>

!!! esercizio "Esercizio 7.5: Introduzione a {\tt Python} (E5)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare in un solo passaggio il massimo, il minimo, la somma e la media di tutti gli elementi dell'array.

    **Domande**

    1. Scrivere un programma <code>Python</code> completo che calcola in un <strong>solo passaggio</strong> le quattro statistiche (massimo, minimo, somma, media) di una lista $a$ di $n$ numeri interi. Il programma deve:

        - definire una funzione <code>array\_stats(a)</code> che calcola i quattro valori con un solo ciclo;

        - restituire i quattro valori come una tupla <code>(max\_val, min\_val, total, avg)</code>;

        - nel blocco <code>\_\_main\_\_</code>, eseguire i casi di test e stampare i risultati.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare il comando che esegue il programma e l'output per tutti i casi di test.

    3. Modificare la funzione in modo che restituisca anche gli indici dell'elemento massimo e dell'elemento minimo. Eseguirla sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Python</code> completo:</strong>

        ```python
        def array_stats(a):
            """Calcola massimo, minimo, somma e media in un solo passaggio.
            Restituisce (max_val, min_val, total, avg)."""
            max_val = a[0]
            min_val = a[0]
            total = a[0]

            for i in range(1, len(a)):
                if a[i] > max_val:
                    max_val = a[i]
                if a[i] < min_val:
                    min_val = a[i]
                total += a[i]

            avg = total / len(a)
            return max_val, min_val, total, avg

        def print_stats(k, a):
            """Stampa le statistiche del caso di prova k."""
            max_v, min_v, s, avg = array_stats(a)
            print(f"Prova {k} - Lista: {a}")
            print(f"  Massimo: {max_v}")
            print(f"  Minimo:  {min_v}")
            print(f"  Somma:   {s}")
            print(f"  Media:   {avg:.4f}")

        if __name__ == "__main__":
            print_stats(1, [9, 12, 3, 16, 19, 11, 12])
            print()
            print_stats(2, [5, 2, 8, 1])
            print()
            print_stats(3, [42])
        ```

        Le tre variabili sono inizializzate con il primo elemento, e il ciclo visita una sola volta gli altri $n-1$ elementi: a ogni iterazione l'elemento corrente è confrontato con il massimo e con il minimo, e viene sommato alla somma.

    2. <strong>Esecuzione.</strong> Se il programma è salvato nel file <code>array\_stats.py</code>, lo si esegue con il comando

        ```text
        python3 array_stats.py
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Lista: [9, 12, 3, 16, 19, 11, 12]
          Massimo: 19
          Minimo:  3
          Somma:   82
          Media:   11.7143

        Prova 2 - Lista: [5, 2, 8, 1]
          Massimo: 8
          Minimo:  1
          Somma:   16
          Media:   4.0000

        Prova 3 - Lista: [42]
          Massimo: 42
          Minimo:  42
          Somma:   42
          Media:   42.0000
        ```

    3. <strong>Funzione estesa che restituisce anche gli indici:</strong>

        ```python
        def array_stats_with_indices(a):
            """Calcola tutte le statistiche, comprese le posizioni.
            Restituisce (max_val, max_idx, min_val, min_idx, total, avg)."""
            max_val = a[0]
            max_idx = 0
            min_val = a[0]
            min_idx = 0
            total = a[0]

            for i in range(1, len(a)):
                if a[i] > max_val:
                    max_val = a[i]
                    max_idx = i
                if a[i] < min_val:
                    min_val = a[i]
                    min_idx = i
                total += a[i]

            avg = total / len(a)
            return max_val, max_idx, min_val, min_idx, total, avg

        if __name__ == "__main__":
            a = [9, 12, 3, 16, 19, 11, 12]
            max_v, max_i, min_v, min_i, s, avg = array_stats_with_indices(a)
            print(f"Lista:   {a}")
            print(f"Max:     {max_v} all'indice {max_i}")
            print(f"Min:     {min_v} all'indice {min_i}")
            print(f"Somma:   {s}")
            print(f"Media:   {avg:.4f}")
        ```

        <strong>Output:</strong>

        ```text
        Lista:   [9, 12, 3, 16, 19, 11, 12]
        Max:     19 all'indice 4
        Min:     3 all'indice 2
        Somma:   82
        Media:   11.7143
        ```

        Il massimo $19$ è all'indice $4$ e il minimo $3$ all'indice $2$ (indici da $0$), cioè nelle posizioni $5$ e $3$ dell'array $a[1..7]$ del testo.
