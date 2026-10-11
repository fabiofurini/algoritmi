---
title: Algoritmi
hide:
  - navigation
  - toc
---

<div class="hero" markdown>

![Lavori in corso: sito e materiale didattico sono ancora in costruzione](img/cantiere.svg){ width="560" }

**Sito in costruzione.** Il materiale è ancora in lavorazione: le slide arriveranno più
avanti; il laboratorio interattivo è già aperto e crescerà.

# Algoritmi

Materiale didattico ideato e sviluppato da **[Fabio Furini](https://fabiofurini.github.io/)**, professore
associato al [DIAG](https://www.diag.uniroma1.it/), Sapienza Università di Roma.

**Le dispense del corso, online**, in quattro parti: algoritmi di base (rappresentazione dei numeri,
pseudocodice, ordinamento, ricerca, algoritmi numerici), linguaggi di programmazione (C++, Python
e Java), crescita e notazione asintotica, analisi e ricorsione (tempo di esecuzione, correttezza,
equazioni di ricorrenza, Master theorem), con definizioni, teoremi con le loro dimostrazioni,
pseudocodice, esempi eseguiti passo per passo, notebook Colab in Python, C++ e Java ed esercizi
con le soluzioni.

[Comincia dagli algoritmi di base :material-arrow-right:](algoritmi-di-base/index.md){ .md-button .md-button--primary }
[Gli esercizi](esercizi/index.md){ .md-button }
[Prova un grafico interattivo](laboratorio/index.md){ .md-button }
[:material-download: Scarica le dispense (PDF)](materiale.md){ .md-button }

</div>

## Come è organizzato ogni capitolo

Ogni capitolo è una delle note del corso, con gli stessi numeri e gli stessi colori della
dispensa: sul sito e nel PDF trovi tutto allo stesso posto.

<div class="grid" markdown>

!!! definizione "Definizione"
    Il significato preciso di un concetto nuovo.

!!! teorema "Teorema, proposizione, osservazione"
    Un risultato da ricordare, con le sue ipotesi.

!!! esempio "Esempio"
    Un calcolo svolto per intero, un passo alla volta.

!!! chiave ""
    **In verde** il punto chiave da portare a casa.

!!! algoritmo "Algoritmo"
    Lo pseudocodice, con le righe numerate come nella dispensa.

!!! codice "Codice"
    I programmi in C++, Python e Java nei capitoli dei linguaggi; gli algoritmi si eseguono
    nei notebook Colab, con i pulsanti sotto lo pseudocodice.

</div>

??? dimostrazione "Dimostrazione — si apre con un clic"
    Le dimostrazioni ci sono tutte, ma chiuse: prima leggi l'enunciato, poi apri la
    dimostrazione quando vuoi studiarla. Lo stesso vale per le soluzioni degli esercizi.

## Le parti del corso

<div class="grid cards" markdown>

-   :material-code-braces: **1 · Algoritmi di base**

    ---

    La rappresentazione dei numeri e lo pseudocodice, il linguaggio in cui sono scritti tutti gli algoritmi del corso; i primi algoritmi: ordinamento (insertion, exchange e selection sort), ricerca lineare e binaria, algoritmi numerici (cambio di base, test di primalità, crivello di Eratostene, massimo comune divisore). Ogni algoritmo con lo pseudocodice ed esempi eseguiti passo per passo.

    1\. Rappresentazione dei numeri · 2\. Pseudocodice · 3\. Algoritmi di ordinamento · 4\. Ricerca lineare e binaria · 5\. Algoritmi numerici

    [:octicons-arrow-right-24: I capitoli](algoritmi-di-base/index.md)

-   :material-console: **2 · Linguaggi di programmazione**

    ---

    Dallo pseudocodice ai programmi: tre linguaggi di programmazione, C++ (compilato), Python (interpretato) e Java (compilato in bytecode ed eseguito da una macchina virtuale). Per ciascuno: variabili e tipi di dato, input e output, operatori, istruzioni condizionali, cicli, array e liste, funzioni, operatori bit a bit e un algoritmo completo, con il confronto fra i tre linguaggi.

    6\. Introduzione a C++ · 7\. Introduzione a Python · 8\. Introduzione a Java

    [:octicons-arrow-right-24: I capitoli](linguaggi/index.md)

-   :material-chart-line: **3 · Notazione e crescita asintotica**

    ---

    Come si confrontano le funzioni di variabile naturale che contano i passi di un algoritmo: le notazioni asintotiche Theta, O grande, Omega, o piccolo e omega, le loro proprietà e il criterio del limite; poi le famiglie di funzioni crescenti (logaritmi, potenze, esponenziali, fattoriale), la gerarchia degli infiniti e il confronto degli ordini di crescita scritto con i simboli. Limiti e funzioni di variabile naturale si danno per noti dal corso di Analisi Matematica 1.

    9\. Notazione asintotica · 10\. Crescita asintotica

    [:octicons-arrow-right-24: I capitoli](notazione-asintotica/index.md)

-   :material-timer-sand: **4 · Analisi degli algoritmi**

    ---

    L'analisi degli algoritmi: la dimensione dell'input, il tempo di esecuzione nel caso migliore, peggiore e medio, e la correttezza dimostrata con le invarianti di ciclo.

    11\. Dimensione dell'input · 12\. Tempo di esecuzione · 13\. Correttezza

    [:octicons-arrow-right-24: I capitoli](analisi/index.md)

-   :material-file-tree: **5 · Ricorsione**

    ---

    La ricorsione: algoritmi ricorsivi classici, equazioni di ricorrenza, il Master theorem, algoritmi ricorsivi (somma di un array, merge sort, ricerca binaria, sotto-array di somma massima) e il confronto fra versioni ricorsive e iterative.

    14\. Ricorsione · 15\. Equazioni di ricorrenza · 16\. Il Master theorem · 17\. Algoritmi ricorsivi · 18\. Algoritmi ricorsivi e iterativi a confronto

    [:octicons-arrow-right-24: I capitoli](ricorsione/index.md)

</div>

## Da non perdere

<div class="grid cards" markdown>

-   :material-pencil-box-multiple: **Esercizi con le soluzioni**

    ---

    Esercizi per ogni capitolo, ciascuno con la soluzione svolta che si apre con un clic.

    [:octicons-arrow-right-24: Gli esercizi](esercizi/index.md)

-   :material-gesture-tap: **Laboratorio interattivo**

    ---

    Esegui gli algoritmi un passo alla volta: ordinamento, ricerca, Euclide e crivello,
    bit dei numeri, crescita delle funzioni, alberi di ricorsione e Master theorem.

    [:octicons-arrow-right-24: I grafici](laboratorio/index.md)

-   :simple-googlecolab: **Notebook in Python, C++ e Java**

    ---

    Gli algoritmi di ogni capitolo da eseguire in Google Colab, nel linguaggio che preferisci.

    [:octicons-arrow-right-24: I notebook](notebook.md)

-   :material-download: **Dispense ed eserciziari in PDF**

    ---

    Cinque volumi di dispense e cinque eserciziari, con la stessa numerazione del sito.

    [:octicons-arrow-right-24: Il materiale](materiale.md)

-   :material-format-list-numbered: **Indice completo**

    ---

    Tutti i capitoli con le loro sezioni, in una pagina.

    [:octicons-arrow-right-24: L’indice](indice.md)

</div>

---

Dello stesso autore:

- **[Programmazione lineare](https://fabiofurini.github.io/programmazione-lineare/)** — poliedri, algoritmo del simplesso, dualità e modellazione, con il laboratorio interattivo;
- **[Laboratorio di Ricerca Operativa](https://fabiofurini.github.io/laboratorio-ricerca-operativa/)** — il laboratorio di modellazione e risoluzione di problemi di ottimizzazione, con Python e i solver;
- **[Modellazione MIP](https://fabiofurini.github.io/modellazione-mip/)** — il modulo sui modelli a variabili intere, con gli stessi strumenti e lo stesso stile;
- **[Analisi Matematica 1](https://fabiofurini.github.io/analisi-matematica-1/)** — le dispense di analisi, con i grafici interattivi;
- **[Algebra lineare](https://fabiofurini.github.io/algebra-lineare/)** — il corso propedeutico, con il laboratorio di calcolo passo per passo;
- **[Ottimizzazione convessa](https://fabiofurini.github.io/ottimizzazione-convessa/)** — insiemi e funzioni convesse, problemi di ottimizzazione, con grafici interattivi.

Materiale didattico di **[Fabio Furini](https://fabiofurini.github.io/)** —
[DIAG](https://www.diag.uniroma1.it/), Sapienza Università di Roma.

*This website is also available in [English](https://fabiofurini.github.io/algorithms/).*
