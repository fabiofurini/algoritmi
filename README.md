<h3 align="center">Materiale didattico di
<a href="https://fabiofurini.github.io/">Fabio Furini</a></h3>
<p align="center">
  Professore associato di Ricerca Operativa ·
  <a href="https://www.diag.uniroma1.it/">DIAG</a>, Sapienza Università di Roma ·
  <a href="https://fabiofurini.github.io/">sito personale</a>
</p>

# Algoritmi

Le dispense del corso di Algoritmi online: definizioni, teoremi con le loro dimostrazioni,
pseudocodice con le righe numerate, codice C++, esempi eseguiti passo per passo ed esercizi con le
soluzioni, con la stessa numerazione e gli stessi colori dei PDF. C'è anche un **laboratorio interattivo**
che esegue gli algoritmi passo per passo. **Il sito è in costruzione**: le slide arriveranno più avanti.

**📖 Sito: [fabiofurini.github.io/algoritmi](https://fabiofurini.github.io/algoritmi/)**

## Contenuti

| Parte | Argomenti |
|---|---|
| 1 · Fondamenti e algoritmi di base | rappresentazione dei numeri, pseudocodice, introduzione a C++, ordinamento (insertion, exchange, selection sort), ricerca lineare e binaria, algoritmi numerici (cambio di base, primalità, crivello di Eratostene, MCD) |
| 2 · Analisi e ricorsione | dimensione dell'input, tempo di esecuzione e notazione asintotica, correttezza e invarianti di ciclo, ricorsione, equazioni di ricorrenza, Master theorem, algoritmi ricorsivi (somma di un array, merge sort, ricerca binaria, sotto-array di somma massima), algoritmi ricorsivi e iterativi a confronto |
| Esercizi | esercizi per ogni capitolo, con le soluzioni svolte |
| Laboratorio | grafici interattivi: rappresentazione dei numeri, ordinamento, ricerca, Euclide e crivello, ordini di crescita, invarianti di ciclo, alberi di ricorsione, Master theorem, merge sort |

Le dispense e gli eserciziari in PDF (due volumi ciascuno) si scaricano dalla
[pagina del materiale](https://fabiofurini.github.io/algoritmi/materiale/).

## English version

The course is available in English:
**[fabiofurini.github.io/algorithms](https://fabiofurini.github.io/algorithms/)**
([repository](https://github.com/fabiofurini/algorithms)).

## Come è costruito

Pagine, figure e PDF sono generati in locale dai sorgenti LaTeX (privati) delle note;
questo repository contiene il sito generato (`docs/`, `mkdocs.yml`). Per vederlo in locale:

```bash
python3 -m pip install mkdocs-material
python3 -m mkdocs serve            # anteprima su http://127.0.0.1:8000
```

## Licenza

- **Testi e figure** (`docs/`): [CC BY 4.0](LICENSE).
- **Codice** (il codice C++ delle pagine e `docs/javascripts/`): [MIT](LICENSE-CODE).

Per citare questo materiale, vedi [`CITATION.cff`](CITATION.cff).

## Della stessa collana

- [Programmazione lineare](https://fabiofurini.github.io/programmazione-lineare/)
- [Laboratorio di Ricerca Operativa](https://fabiofurini.github.io/laboratorio-ricerca-operativa/)
- [Modellazione MIP](https://fabiofurini.github.io/modellazione-mip/)
- [Analisi Matematica 1](https://fabiofurini.github.io/analisi-matematica-1/)
- [Algebra lineare](https://fabiofurini.github.io/algebra-lineare/)
- [Ottimizzazione convessa](https://fabiofurini.github.io/ottimizzazione-convessa/)

---

Materiale didattico di [Fabio Furini](https://fabiofurini.github.io/) — [DIAG](https://www.diag.uniroma1.it/), Sapienza Università di Roma.
