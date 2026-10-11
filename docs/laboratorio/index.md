---
hide:
  - navigation
---

# Laboratorio interattivo

Qui gli algoritmi si vedono lavorare. Scegli un'app: si apre a tutta pagina, con **cursori** e pulsanti.
Trascina i cursori, oppure premi ▶ per eseguire un passo alla volta e «Esegui» per l'animazione. La notazione
è quella delle dispense: array \(a[1..n]\) con gli indici da 1, gli stessi nomi di algoritmi e variabili.

## Algoritmi di base

<div class="grid cards" markdown>

-   :material-numeric: **Rappresentazione dei numeri**

    ---

    Lo stesso intero in binario, in complemento a due, in modulo e segno e in IEEE 754: cambia il numero e guarda i bit.

    [Apri l'app →](rappresentazione-numeri.md)

-   :material-sort-ascending: **Ordinamento passo per passo**

    ---

    Insertion, exchange e selection sort: confronti e spostamenti, un passo alla volta, con la riga di pseudocodice in esecuzione.

    [Apri l'app →](ordinamento.md)

-   :material-magnify: **Ricerca lineare e binaria**

    ---

    Lo stesso array ordinato, cercato in due modi: conta quanti confronti servono alla ricerca lineare e a quella binaria.

    [Apri l'app →](ricerca.md)

-   :material-grid: **Euclide e crivello di Eratostene**

    ---

    Il massimo comun divisore con i resti successivi e i numeri primi che emergono cancellando i multipli.

    [Apri l'app →](euclide-crivello.md)

</div>

## Notazione e crescita asintotica

<div class="grid cards" markdown>

-   :material-chart-line: **Ordini di crescita**

    ---

    Logaritmo, polinomi, esponenziale: quanti passi (e quanto tempo) servono al crescere di n, confrontando le funzioni.

    [Apri l'app →](crescita.md)

</div>

## Analisi degli algoritmi

<div class="grid cards" markdown>

-   :material-check-decagram: **L'invariante di ciclo**

    ---

    FindMaximum iterazione per iterazione: verifica che l'invariante valga all'inizio, a ogni passo e alla fine.

    [Apri l'app →](invariante.md)

</div>

## Ricorsione

<div class="grid cards" markdown>

-   :material-file-tree: **Alberi delle chiamate ricorsive**

    ---

    L'albero delle chiamate di una funzione ricorsiva e la pila: i nodi contano i passi, la profondità la memoria.

    [Apri l'app →](alberi-ricorsione.md)

-   :material-layers-triple: **Il Master theorem**

    ---

    La ricorrenza T(n) = a T(n/b) + n^d livello per livello: il costo dei livelli è una progressione geometrica e decide l'ordine di T(n).

    [Apri l'app →](master-theorem.md)

-   :material-call-merge: **Merge sort**

    ---

    Si divide fino a un elemento, poi si fondono le metà ordinate con Merge: guarda le chiamate e le fusioni una alla volta.

    [Apri l'app →](merge-sort.md)

</div>
