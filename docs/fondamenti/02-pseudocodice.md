---
title: "Pseudocodice"
---

# Pseudocodice

<div class="info-capitolo" markdown>

**Parte 1 · Fondamenti e algoritmi di base · Capitolo 2** · [:material-file-pdf-box: Dispensa, volume 1 (PDF)](../pdf/dispensa-1-fondamenti.pdf) · [:material-pencil: Esercizi](../esercizi/es-02-pseudocodice.md)

</div>

## Introduzione

Nel capitolo precedente abbiamo visto come sono rappresentati i dati di un algoritmo, i numeri. In questo capitolo fissiamo il linguaggio usato in queste note per descrivere gli algoritmi stessi: lo <strong>pseudocodice</strong>. Lo pseudocodice è abbastanza preciso da descrivere senza ambiguità ogni passo di un algoritmo, e abbastanza semplice da poter essere letto senza conoscere alcun linguaggio di programmazione.

Il capitolo introduce gli elementi dello pseudocodice uno alla volta, dal più semplice al più strutturato:

- variabili, dichiarazioni e assegnamenti, e le operazioni di base su di essi;

- i costrutti di base che controllano l'ordine di esecuzione: istruzioni condizionali, cicli, e le istruzioni di controllo dei cicli <strong>break</strong> e <strong>continue</strong>;

- array con uno, due o più indici;

- funzioni, che danno un nome a un algoritmo, con il suo input e il suo output;

- insiemi.

Ogni costrutto è seguito da esempi, eseguiti passo per passo su piccole istanze. Eseguire un algoritmo a mano, tenendo traccia dei valori delle sue variabili, è il modo migliore per capire che cosa fa.

## 2.1 Introduzione allo pseudocodice

<a id="box-1-defAlgorithm"></a>

!!! definizione "Definizione 2.1: algoritmo"

    Un <strong>algoritmo</strong> è una sequenza finita di istruzioni non ambigue che, a partire da alcuni dati forniti come <strong>input</strong>, produce in un numero finito di passi un risultato fornito come <strong>output</strong>.

<a id="box-2-defPseudoCode"></a>

!!! definizione "Definizione 2.2: pseudocodice"

    Lo <strong>pseudocodice</strong> è una descrizione di alto livello di un algoritmo che usa un misto di linguaggio naturale e di strutture simili a quelle dei linguaggi di programmazione.

- Lo pseudocodice non è fatto per essere eseguito da un calcolatore, ma per comunicare agli esseri umani la logica di un algoritmo.

- Lo pseudocodice permette di concentrarsi sulla logica e sulla struttura di un algoritmo senza preoccuparsi della sintassi di uno specifico linguaggio di programmazione.

- <strong>Convenzione:</strong> in queste note tutte le parole riservate (parole chiave) dello pseudocodice sono scritte in grassetto, ad esempio <strong>if</strong>, <strong>while</strong>, <strong>for</strong>, <strong>return</strong>, ecc.

!!! chiave ""

    <strong>Vantaggi dello pseudocodice:</strong>

    - Indipendente dal linguaggio: può essere compreso da programmatori che usano linguaggi diversi

    - Facile da scrivere e da modificare

    - Si concentra sulla logica dell'algoritmo anziché sui dettagli di implementazione

    - Facilita la comunicazione tra sviluppatori e persone non tecniche

    - Utile per la pianificazione prima della scrittura effettiva del codice

    <strong>Principi fondamentali:</strong>

    - Usare nomi di variabili chiari e descrittivi

    - Mantenere le istruzioni semplici e concise

    - Usare l'indentazione per mostrare la struttura e l'annidamento

    - Usare costrutti standard (<strong>if-then-else</strong>, <strong>while</strong>, <strong>for</strong>, ecc.)

    - Inserire commenti quando necessario per chiarire le operazioni complesse

!!! chiave ""

    <strong>Buone pratiche:</strong>

    - <strong>Indentazione:</strong> usare un'indentazione coerente per mostrare la struttura a blocchi

    - <strong>Variabili:</strong> usare nomi descrittivi in corsivo o in testo normale

    - <strong>Commenti:</strong> aggiungere commenti (in linguaggio naturale) per spiegare i passi complessi

    - <strong>Input/Output:</strong> specificare chiaramente i parametri di input e l'output (valori restituiti)

    - <strong>Numeri di riga:</strong> utili per fare riferimento a righe specifiche

    - <strong>Coerenza:</strong> mantenere la stessa notazione e lo stesso stile in tutto il testo

## 2.2 Variabili e assegnamenti

I dati di un algoritmo sono memorizzati in <strong>variabili</strong>: contenitori dotati di un nome, il cui valore può cambiare durante l'esecuzione. Una variabile viene prima creata con una dichiarazione e poi modificata con degli assegnamenti.

### 2.2.1 Variabili

!!! chiave ""

    - Le variabili devono essere dichiarate prima dell'uso

    - L'operatore di dichiarazione è “$:=$”

    - La dichiarazione specifica il nome della variabile e il suo valore iniziale

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">variabile := valore_iniziale</span></span></div>
    </div>

<a id="box-3-texexpbox1"></a>

!!! esempio "Esempio 2.1: dichiarazione di variabili"

    Sette variabili dichiarate con i loro valori iniziali: sono ammessi valori interi, razionali, $-\infty$ e logici (<strong>true</strong>/<strong>false</strong>).

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(n := 5&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(m := 10&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(x := -3/5&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(count := 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(max := -&#92;infty&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(status&#92;)</span> := true</span></span></div>
    </div>

### 2.2.2 Assegnamento

!!! chiave ""

    - L'operatore di assegnamento è “$\leftarrow$”

    - Assegna il valore di un'espressione a una variabile dichiarata in precedenza: prima si valuta l'espressione a destra, poi il suo valore sostituisce il vecchio valore della variabile

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">variabile <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> espressione</span></span></div>
    </div>

<a id="box-4-texexpbox2"></a>

!!! esempio "Esempio 2.2: assegnamento"

    Con le variabili dell'[Esempio 2.1](#box-3-texexpbox1):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(n &#92;leftarrow 10&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow n + m&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(count &#92;leftarrow count + 1&#92;)</span></span></span></div>
    </div>

    Dopo i tre assegnamenti si ha $n = 10$, $sum = 10 + 10 = 20$ e $count = 1 + 1 = 2$. Nell'ultimo assegnamento la stessa variabile compare in entrambi i membri: il vecchio valore $1$ viene usato per calcolare il nuovo valore $2$.

<a id="box-5-texexpbox2b"></a>

!!! esempio "Esempio 2.3: scambio dei valori di due variabili"

    Per scambiare i valori di due variabili $x$ e $y$ serve una terza variabile temporanea $tmp$: il solo assegnamento $x \leftarrow y$ sovrascriverebbe il vecchio valore di $x$.

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(tmp := x&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(x &#92;leftarrow y&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(y &#92;leftarrow tmp&#92;)</span></span></span></div>
    </div>

    <strong>Esecuzione passo per passo</strong> con $x = 3$ e $y = 8$:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th>istruzione</th>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(y&#92;)</span></th>
    <th><span class="arithmatex">&#92;(tmp&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td>–</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(tmp := x&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(x &#92;leftarrow y&#92;)</span></td>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(y &#92;leftarrow tmp&#92;)</span></td>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    </table></div>

## 2.3 Operazioni di base

Le espressioni combinano variabili e valori con le seguenti operazioni.

!!! chiave ""

    <strong>Operazioni matematiche:</strong>

    - $+, -, \times, /$: aritmetica di base

    - $a \bmod b$: modulo, cioè il resto della divisione intera di $a$ per $b$

    - $\lfloor x \rfloor$: parte intera inferiore (il più grande intero $\le x$)

    - $\lceil x \rceil$: parte intera superiore (il più piccolo intero $\ge x$)

    - $|x|$: valore assoluto

    - $\max(a, b)$, $\min(a, b)$: massimo e minimo

    <strong>Operatori di confronto:</strong>

    - $=, \neq$: uguale, diverso

    - $<, \le, >, \ge$: minore, minore o uguale, maggiore, maggiore o uguale

    <strong>Operatori logici:</strong>

    - <strong>and</strong>, <strong>or</strong>, <strong>not</strong>: operazioni logiche

    <strong>Input/Output:</strong>

    - <strong>read</strong>(variabile): legge un input dall'utente

    - <strong>print</strong>(espressione): stampa un valore

<a id="box-6-texexpbox2c"></a>

!!! esempio "Esempio 2.4: valutazione di espressioni"

    - $17 \bmod 5 = 2$, poiché $17 = 3 \cdot 5 + 2$; in particolare, un intero $i$ è multiplo di $3$ se e solo se $i \bmod 3 = 0$.

    - $\lfloor 7/2 \rfloor = \lfloor 3.5 \rfloor = 3$ e $\lceil 7/2 \rceil = \lceil 3.5 \rceil = 4$.

    - $|-3| = 3$, $\max(-3, 2) = 2$ e $\min(-3, 2) = -3$.

    - $(5 > 3)$ <strong>and</strong> $(2 > 4)$ è <strong>false</strong>, mentre $(5 > 3)$ <strong>or</strong> $(2 > 4)$ è <strong>true</strong>.

## 2.4 Costrutti di base

Le istruzioni dello pseudocodice vengono eseguite una dopo l'altra, dall'alto verso il basso. Due tipi di costrutti cambiano quest'ordine: le <strong>istruzioni condizionali</strong>, che eseguono un blocco solo quando vale una condizione, e i <strong>cicli</strong>, che eseguono un blocco più volte.

### 2.4.1 Istruzioni condizionali

#### If-then

!!! chiave ""

    - Esegue un blocco di istruzioni solo se una condizione è vera

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>if</strong> condizione <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-7-texexpbox3"></a>

!!! esempio "Esempio 2.5: if-then"

    Verifica se un numero $x$ è positivo:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(positive&#92;)</span> := false</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(x &gt; 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(positive&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> true</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>print</strong>(<span class="arithmatex">&#92;(x&#92;)</span> è positivo)</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $x = 5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &gt; 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(positive&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>false</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>Sì</td>
    <td>true</td>
    </tr>
    </table></div>

    <strong>Output:</strong> <code>5 è positivo</code>

    <strong>Istanza 2:</strong> $x = -3$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &gt; 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(positive&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>false</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(-3&#92;)</span></td>
    <td>No</td>
    <td>false</td>
    </tr>
    </table></div>

    <strong>Output:</strong> non viene stampato nulla.

#### If-then-else

!!! chiave ""

    - Esegue un blocco se la condizione è vera, e un altro blocco se è falsa

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>if</strong> condizione <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni se vera</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>else</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni se falsa</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-8-texexpbox4"></a>

!!! esempio "Esempio 2.6: if-then-else"

    Calcolo del valore assoluto di un numero $x$:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(result&#92;)</span> := 0</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(x &#92;ge 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(result&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(x&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><strong>else</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(result&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(-x&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $x = 7$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &#92;ge 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(result&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $result = 7$

    <strong>Istanza 2:</strong> $x = -4$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &#92;ge 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(result&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(-4&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $result = 4$

### 2.4.2 Cicli

#### Ciclo while

!!! chiave ""

    - Ripete un blocco di istruzioni finché una condizione è vera

    - La condizione viene controllata prima di ogni iterazione

    - Se la condizione è inizialmente falsa, il corpo del ciclo non viene mai eseguito

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> condizione <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-9-texexpbox6"></a>

!!! esempio "Esempio 2.7: ciclo while"

    Calcolo della somma dei numeri da $1$ a $n$:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza:</strong> $n = 5$. Ogni riga mostra il valore di $i$ quando la condizione viene controllata, l'esito del controllo, e i valori di $sum$ e $i$ alla fine dell'iterazione.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(i &#92;le n&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
    <th><span class="arithmatex">&#92;(i&#92;)</span> (dopo)</th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    <td>–</td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $sum = 15$

Nell'esempio precedente il numero di iterazioni è noto in anticipo. Il ciclo while è necessario quando non lo è, come nell'esempio seguente.

<a id="box-10-texexpbox7b"></a>

!!! esempio "Esempio 2.8: ciclo while"

    Calcolo di quante volte un numero $x$ va dimezzato prima che diventi minore o uguale a una soglia $\varepsilon > 0$:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(count := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(x &gt; &#92;varepsilon&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(x &#92;leftarrow x / 2&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count &#92;leftarrow count + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $x = 10$, $\varepsilon = 1$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(count&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &gt; &#92;varepsilon&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(x&#92;)</span> (dopo)</th>
    <th><span class="arithmatex">&#92;(count&#92;)</span> (dopo)</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(2.5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2.5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(1.25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1.25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(0.625&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(0.625&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>No <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> uscita</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $count = 4$

    <strong>Istanza 2:</strong> $x = 100$, $\varepsilon = 10$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(x&#92;)</span></th>
    <th><span class="arithmatex">&#92;(count&#92;)</span></th>
    <th><span class="arithmatex">&#92;(x &gt; &#92;varepsilon&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(x&#92;)</span> (dopo)</th>
    <th><span class="arithmatex">&#92;(count&#92;)</span> (dopo)</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(100&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(50&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(50&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(12.5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(12.5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(6.25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6.25&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>No <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> uscita</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $count = 4$

#### Ciclo for

!!! chiave ""

    - Ripete un blocco di istruzioni per un numero di volte specificato

    - Di solito si usa quando il numero di iterazioni è noto in anticipo

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> variabile := valore_iniziale <strong>to</strong>  valore_finale <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

Il ciclo for è un modo compatto di scrivere un particolare ciclo while: la variabile del ciclo viene dichiarata con il valore iniziale, la condizione la confronta con il valore finale, e viene incrementata di $1$ alla fine di ogni iterazione.

!!! chiave ""

    Il ciclo a sinistra è equivalente al ciclo a destra:

    <div class="minipage" style="width:45%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := s&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(e&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <div class="minipage" style="width:45%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(i := s&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le e&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    In particolare, il corpo viene eseguito $e - s + 1$ volte se $s \le e$, e non viene mai eseguito se $s > e$.

<a id="box-11-texexpbox7"></a>

!!! esempio "Esempio 2.9: ciclo for"

    Calcolo della somma dei numeri da $1$ a $n$ con un ciclo for (confrontare con l'[Esempio 2.7](#box-9-texexpbox6)):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza:</strong> $n = 5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(i &#92;le n&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $sum = 15$

!!! chiave ""

    Il ciclo for può usare facoltativamente un valore di <strong>passo</strong> (<em>step</em>), per incrementare la variabile del ciclo di valori diversi da $1$.

<a id="box-12-texexpbox8"></a>

!!! esempio "Esempio 2.10: ciclo for con passo"

    Calcolo della somma dei primi $n$ numeri pari ($2, 4, \ldots, 2n$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(2n&#92;)</span> <strong>step</strong>  <span class="arithmatex">&#92;(2&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum&#92;)</span> <span class="arithmatex">&#92;(&#92;leftarrow&#92;)</span> <span class="arithmatex">&#92;(sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza:</strong> $n = 4$ (even numbers: $2, 4, 6, 8$)

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(i &#92;le 2n&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(8&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(20&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(20&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $sum = 20$

### 2.4.3 Istruzioni di controllo dei cicli

A volte un ciclo deve essere interrotto prima della sua fine naturale, oppure una singola iterazione deve essere saltata. A questi scopi servono due istruzioni.

#### Istruzione break

!!! chiave ""

    - L'istruzione <strong>break</strong> esce immediatamente dal ciclo corrente

    - L'esecuzione continua con la prima istruzione dopo il ciclo

    - Utile quando una condizione di terminazione si verifica prima del completamento naturale del ciclo

    <div class="minipage" style="width:47%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> condizione <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> condizione_di_uscita <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>break</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <div class="minipage" style="width:47%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> variabile := valore_iniziale <strong>to</strong>  valore_finale <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> condizione_di_uscita <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>break</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

<a id="box-13-texexpbox11"></a>

!!! esempio "Esempio 2.11: istruzione break"

    Calcolo della somma dei numeri da $1$ a $n$, fermandosi non appena la somma supera una soglia $t$.

    <div class="minipage" style="width:47%" markdown>

    Con un ciclo while:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(sum &gt; t&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>break</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <div class="minipage" style="width:47%" markdown>

    Con un ciclo for:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(sum &gt; t&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>break</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <strong>Esecuzione passo per passo (entrambi i cicli):</strong>

    <strong>Istanza:</strong> $n = 6$, $t = 10$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
    <th><span class="arithmatex">&#92;(sum &gt; t&#92;)</span>?</th>
    </tr>
    <tr>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td>–</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(15&#92;)</span></td>
    <td>Sì <span class="arithmatex">&#92;(&#92;Rightarrow&#92;)</span> <strong>break</strong></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $sum = 15$; l'iterazione con $i = 6$ non viene mai eseguita.

#### Istruzione continue

!!! chiave ""

    - L'istruzione <strong>continue</strong> salta il resto dell'iterazione corrente

    - L'esecuzione prosegue subito con l'iterazione successiva del ciclo (in un ciclo while, con il controllo della condizione)

    - Utile quando alcune iterazioni vanno saltate in base a una condizione

    <div class="minipage" style="width:47%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> condizione <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> condizione_di_salto <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>continue</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <div class="minipage" style="width:47%" markdown>

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> variabile := valore_iniziale <strong>to</strong>  valore_finale <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> condizione_di_salto <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>continue</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

<a id="box-14-texexpbox12"></a>

!!! esempio "Esempio 2.12: istruzione continue"

    Calcolo della somma dei numeri da $1$ a $n$, saltando i multipli di $3$.

    <div class="minipage" style="width:47%" markdown>

    Con un ciclo while:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(i := 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>while</strong> <span class="arithmatex">&#92;(i &#92;le n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(i &#92;bmod 3 = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>continue</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(i &#92;leftarrow i + 1&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    <div class="minipage" style="width:47%" markdown>

    Con un ciclo for:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(sum := 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(i &#92;bmod 3 = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>continue</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(sum &#92;leftarrow sum + i&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    </div>

    Nel ciclo while la variabile $i$ deve essere incrementata prima di <strong>continue</strong>: altrimenti la condizione $i \bmod 3 = 0$ resterebbe vera per sempre e il ciclo non terminerebbe mai. Nel ciclo for l'incremento è automatico.

    <strong>Esecuzione passo per passo (entrambi i cicli):</strong>

    <strong>Istanza:</strong> $n = 7$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(i &#92;bmod 3 = 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(sum&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Risultato:</strong> $sum = 19 = 1 + 2 + 4 + 5 + 7$

!!! chiave ""

    <strong>Punti chiave sui costrutti di base.</strong>

    - <strong>if-then</strong> e <strong>if-then-else</strong> scelgono quale blocco eseguire in base a una condizione.

    - <strong>while</strong> ripete un blocco finché una condizione è vera, controllandola prima di ogni iterazione; <strong>for</strong> ripete un blocco per ogni valore di una variabile del ciclo da un valore iniziale a un valore finale.

    - <strong>break</strong> esce dal ciclo; <strong>continue</strong> passa all'iterazione successiva.

    - Eseguire un costrutto passo per passo su una piccola istanza, con una tabella dei valori delle variabili, mostra esattamente che cosa fa.

## 2.5 Array

Molti algoritmi lavorano su una collezione di valori dello stesso tipo, ad esempio una lista di $n$ numeri. Invece di dichiarare $n$ variabili diverse, si usa un array.

!!! chiave ""

    - Gli array sono collezioni indicizzate di variabili e devono essere dichiarati prima dell'uso

    - L'operatore di dichiarazione è “new array” seguito dall'intervallo degli indici

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">nome_array := new array[inizio..fine]</span></span></div>
    </div>

<a id="box-15-texexpbox13"></a>

!!! esempio "Esempio 2.13: dichiarazione di un array"

    Creazione di un array di dimensione $n$, indicizzato da $1$ a $n$:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(a := &#92;text{new array}&#91;1..n&#93;&#92;)</span></span></span></div>
    </div>

!!! chiave ""

    - La notazione $a[i]$ indica la variabile di indice $i$

    - Gli array sono di solito indicizzati a partire da $0$ o da $1$: nello pseudocodice di queste note gli indici partono da $1$, quindi un array di $n$ elementi è $a[1..n]$; in molti linguaggi di programmazione, come il C++, gli indici partono da $0$

    - Ogni variabile dell'array deve essere inizializzata prima di essere letta e usata

    - Per inizializzare tutti gli elementi allo stesso valore, si usa un ciclo <strong>for</strong>:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i :=&#92;)</span> inizio <strong>to</strong>  fine <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">nome_array<span class="arithmatex">&#92;(&#91;i&#93; &#92;leftarrow&#92;)</span> valore_iniziale</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-16-texexpbox14"></a>

!!! esempio "Esempio 2.14: assegnamento in un array"

    Inizializzazione e accesso alle variabili di un array $a[1..n]$ (con $n \ge 5$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Inizializza a zero tutte le variabili dell'array</span></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;i&#93; &#92;leftarrow 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Accesso e modifica</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(x := a&#91;5&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(a&#91;3&#93; &#92;leftarrow 42&#92;)</span></span></span></div>
    </div>

    Con $n = 5$ l'array vale $[0, 0, 0, 0, 0]$ dopo il ciclo, $x = 0$, e alla fine l'array vale $[0, 0, 42, 0, 0]$.

### 2.5.1 Array bidimensionali

!!! chiave ""

    - Gli array bidimensionali sono collezioni indicizzate di variabili con due indici e devono essere dichiarati prima dell'uso

    - L'operatore di dichiarazione è “new array” seguito dai due intervalli degli indici

    - Gli array bidimensionali sono di solito indicizzati a partire da $0$ o da $1$ (da $1$ in queste note)

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">nome_array := new array[inizio<span class="arithmatex">&#92;(&#95;1&#92;)</span>..fine<span class="arithmatex">&#92;(&#95;1&#92;)</span>][inizio<span class="arithmatex">&#92;(&#95;2&#92;)</span>..fine<span class="arithmatex">&#92;(&#95;2&#92;)</span>]</span></span></div>
    </div>

<a id="box-17-texexpbox15"></a>

!!! esempio "Esempio 2.15: dichiarazione di un array bidimensionale"

    Creazione di un array bidimensionale di dimensione $m \times n$ (indicizzato da $1$ a $m$ e da $1$ a $n$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(b := &#92;text{new array}&#91;1..m&#93;&#91;1..n&#93;&#92;)</span></span></span></div>
    </div>

!!! chiave ""

    - La notazione $b[i][j]$ indica la variabile nella riga $i$ e nella colonna $j$

    - Ogni variabile dell'array deve essere inizializzata prima di essere letta e usata

    - Per inizializzare tutti gli elementi allo stesso valore, si usano cicli <strong>for</strong> annidati:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i :=&#92;)</span> inizio<span class="arithmatex">&#92;(&#95;1&#92;)</span> <strong>to</strong>  fine<span class="arithmatex">&#92;(&#95;1&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j :=&#92;)</span> inizio<span class="arithmatex">&#92;(&#95;2&#92;)</span> <strong>to</strong>  fine<span class="arithmatex">&#92;(&#95;2&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">nome_array<span class="arithmatex">&#92;(&#91;i&#93;&#91;j&#93; &#92;leftarrow&#92;)</span> valore_iniziale</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-18-texexpbox16"></a>

!!! esempio "Esempio 2.16: assegnamento in un array bidimensionale"

    Inizializzazione e accesso alle variabili di un array bidimensionale $b[1..m][1..n]$ (con $m \ge 2$ e $n \ge 3$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Inizializza a zero tutte le variabili dell'array bidimensionale</span></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(m&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(b&#91;i&#93;&#91;j&#93; &#92;leftarrow 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Accesso e modifica</span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(x := b&#91;2&#93;&#91;3&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(b&#91;1&#93;&#91;1&#93; &#92;leftarrow 42&#92;)</span></span></span></div>
    </div>

    Il ciclo esterno scorre le righe e, per ogni riga $i$, il ciclo interno scorre tutte le colonne: gli elementi vengono visitati nell'ordine $b[1][1], b[1][2], \dots, b[1][n], b[2][1], \dots, b[m][n]$, per un totale di $m \cdot n$ assegnamenti.

### 2.5.2 Array multidimensionali

!!! chiave ""

    - Gli array multidimensionali sono collezioni indicizzate di variabili con più indici e devono essere dichiarati prima dell'uso

    - L'operatore di dichiarazione è “new array” seguito dagli intervalli degli indici per ciascuna dimensione

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">nome_array := new array[inizio<span class="arithmatex">&#92;(&#95;1&#92;)</span>..fine<span class="arithmatex">&#92;(&#95;1&#92;)</span>][inizio<span class="arithmatex">&#92;(&#95;2&#92;)</span>..fine<span class="arithmatex">&#92;(&#95;2&#92;)</span>]<span class="arithmatex">&#92;(&#92;cdots&#92;)</span>[inizio<span class="arithmatex">&#92;(&#95;k&#92;)</span>..fine<span class="arithmatex">&#92;(&#95;k&#92;)</span>]</span></span></div>
    </div>

<a id="box-19-texexpbox17"></a>

!!! esempio "Esempio 2.17: dichiarazione di un array multidimensionale"

    Creazione di un array a $3$ dimensioni di dimensione $p \times q \times r$ (indicizzato da $1$ a $p$, da $1$ a $q$ e da $1$ a $r$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(t := &#92;text{new array}&#91;1..p&#93;&#91;1..q&#93;&#91;1..r&#93;&#92;)</span></span></span></div>
    </div>

!!! chiave ""

    - La notazione $t[i_1][i_2]\cdots[i_k]$ indica la variabile di indici $i_1, i_2, \ldots, i_k$

    - Gli array multidimensionali sono di solito indicizzati a partire da $0$ o da $1$ (da $1$ in queste note)

    - Ogni variabile dell'array deve essere inizializzata prima di essere letta e usata

    - Per inizializzare tutti gli elementi allo stesso valore, si usano cicli <strong>for</strong> annidati (uno per dimensione):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i&#95;1 :=&#92;)</span> inizio<span class="arithmatex">&#92;(&#95;1&#92;)</span> <strong>to</strong>  fine<span class="arithmatex">&#92;(&#95;1&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i&#95;2 :=&#92;)</span> inizio<span class="arithmatex">&#92;(&#95;2&#92;)</span> <strong>to</strong>  fine<span class="arithmatex">&#92;(&#95;2&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(&#92;vdots&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i&#95;k :=&#92;)</span> inizio<span class="arithmatex">&#92;(&#95;k&#92;)</span> <strong>to</strong>  fine<span class="arithmatex">&#92;(&#95;k&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t">nome_array<span class="arithmatex">&#92;(&#91;i&#95;1&#93;&#91;i&#95;2&#93;&#92;cdots&#91;i&#95;k&#93; &#92;leftarrow&#92;)</span> valore_iniziale</span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-20-texexpbox18"></a>

!!! esempio "Esempio 2.18: assegnamento in un array multidimensionale"

    Inizializzazione e accesso a un array a $3$ dimensioni $t[1..p][1..q][1..r]$ (con $p \ge 2$, $q \ge 2$ e $r \ge 3$):

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Inizializza a zero tutte le variabili dell'array a <span class="arithmatex">&#92;(3&#92;)</span> dimensioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(p&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(j := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(q&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(k := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(r&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(t&#91;i&#93;&#91;j&#93;&#91;k&#93; &#92;leftarrow 0&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Accesso e modifica</span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(x := t&#91;1&#93;&#91;2&#93;&#91;3&#93;&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(t&#91;2&#93;&#91;1&#93;&#91;3&#93; &#92;leftarrow 42&#92;)</span></span></span></div>
    </div>

## 2.6 Funzioni

Gli esempi visti finora sono frammenti di pseudocodice che lavorano su variabili supposte esistenti. Una funzione trasforma un frammento di questo tipo in un algoritmo completo, con un nome, un input e un output.

!!! chiave ""

    - Una <strong>funzione</strong> è un blocco di codice dotato di nome e riutilizzabile che svolge un compito specifico

    - Una funzione riceve dati di <strong>input</strong> attraverso i suoi <strong>parametri</strong> e produce dati di <strong>output</strong>

    - L'istruzione <strong>return</strong> termina la funzione e ne specifica i risultati

    - Le funzioni si usano di solito per realizzare <strong>algoritmi</strong> o per eseguire calcoli specifici che possono essere riutilizzati in parti diverse di un programma

    <strong>Sintassi:</strong>

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>descrizione dei parametri di input</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>descrizione dell'output / del valore restituito</span></div>
    <div class="pc-sep"></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FunctionName(parametro<span class="arithmatex">&#92;(&#95;1&#92;)</span>, parametro<span class="arithmatex">&#92;(&#95;2&#92;)</span>, …, parametro<span class="arithmatex">&#92;(&#95;k&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t">istruzioni</span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> risultato</span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

Nel resto di queste note ogni algoritmo è scritto come una funzione, dentro un riquadro rosso. L'input indica le <strong>precondizioni</strong> sui dati (ad esempio, che un array abbia almeno un elemento): la funzione è garantita funzionare solo quando esse valgono.

<a id="box-21-texexpbox21"></a>

!!! esempio "Esempio 2.19: valore massimo in un array"

    Una funzione che restituisce il valore massimo di un array: la variabile $max$ parte dal primo elemento e viene aggiornata ogni volta che si trova un elemento più grande.

    !!! algoritmo "Algoritmo: FindMaximum"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il valore massimo nell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> FindMaximum(a, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max := a&#91;1&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(max &#92;leftarrow a&#91;i&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(max&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $a = [9, 12, 3, 16, 19, 11, 12]$, $n=7$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(max&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(16&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(16&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(11&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $max = 19$

    <strong>Istanza 2:</strong> $a = [3, 7, 2, 9, 1]$, $n=5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; max&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(max&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $max = 9$

<a id="box-22-texexpbox23"></a>

!!! esempio "Esempio 2.20: conteggio degli elementi positivi di un array"

    Una funzione che conta il numero di elementi positivi in un array:

    !!! algoritmo "Algoritmo: CountPositive"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il numero di elementi positivi nell'array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> CountPositive(a, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count := 0&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; 0&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(count &#92;leftarrow count + 1&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(count&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $a = [-2, 5, -1, 3, 0]$, $n = 5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(count&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-2&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-1&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $count = 2$

    <strong>Istanza 2:</strong> $a = [4, -3, 7, 2]$, $n = 4$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; 0&#92;)</span>?</th>
    <th><span class="arithmatex">&#92;(count&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-3&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $count = 3$

<a id="box-23-texexpbox24"></a>

!!! esempio "Esempio 2.21: verifica se un array è ordinato"

    Una funzione che verifica se un array è ordinato in ordine non decrescente. L'istruzione <strong>return</strong> dentro il ciclo termina la funzione non appena si trovano due elementi consecutivi nell'ordine sbagliato.

    !!! algoritmo "Algoritmo: IsSorted"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> numeri interi</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span><strong>true</strong> se i valori dell'array <span class="arithmatex">&#92;(a&#92;)</span> sono ordinati in ordine non decrescente e <strong>false</strong> altrimenti</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> IsSorted(a, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n-1&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(a&#91;i&#93; &gt; a&#91;i+1&#93;&#92;)</span> <strong>then</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>false</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <strong>true</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $a = [2, 5, 7, 9]$, $n = 4$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i{+}1&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; a&#91;i{+}1&#93;&#92;)</span>?</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>No</td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    <td>No</td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> <strong>true</strong>

    <strong>Istanza 2:</strong> $a = [3, 1, 4, 2]$, $n = 4$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i{+}1&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93; &gt; a&#91;i{+}1&#93;&#92;)</span>?</th>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>Sì</td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> <strong>false</strong>, dopo un solo confronto.

<a id="box-24-texexpbox27"></a>

!!! esempio "Esempio 2.22: prodotto scalare di due array"

    Una funzione che calcola il prodotto scalare $\sum_{i=1}^{n} a[i] \cdot b[i]$ di due array:

    !!! algoritmo "Algoritmo: ScalarProduct"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Due array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> e <span class="arithmatex">&#92;(b&#91;1..n&#93;&#92;)</span> di dimensione <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span></span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Il prodotto scalare dei due array</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ScalarProduct(a, b, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prod := a&#91;1&#93; &#92;cdot b&#91;1&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 2&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(prod &#92;leftarrow prod + a&#91;i&#93; &#92;cdot b&#91;i&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(prod&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $a = [1, 2, 3]$, $b = [4, 5, 6]$, $n = 3$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(b&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;cdot b&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(prod&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(1 &#92;cdot 4 = 4&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(10&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4 + 10 = 14&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(18&#92;)</span></td>
    <td><span class="arithmatex">&#92;(14 + 18 = 32&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $prod = 32$

    <strong>Istanza 2:</strong> $a = [2, 0, -1]$, $b = [3, 4, 5]$, $n = 3$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(b&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(a&#91;i&#93;&#92;cdot b&#91;i&#93;&#92;)</span></th>
    <th><span class="arithmatex">&#92;(prod&#92;)</span></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(2 &#92;cdot 3 = 6&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(0&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6 + 0 = 6&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(-5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6 + (-5) = 1&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $prod = 1$

<a id="box-25-texexpbox28"></a>

!!! esempio "Esempio 2.23: inversione di un array"

    Una funzione che inverte l'ordine degli elementi di un array: l'elemento $a[i]$ viene scambiato con il suo simmetrico $a[n-i+1]$, con la variabile temporanea dell'[Esempio 2.3](#box-5-texexpbox2b). Bastano $\lfloor n/2 \rfloor$ scambi: con $n$ dispari, l'elemento centrale resta al suo posto.

    !!! algoritmo "Algoritmo: ReverseArray"

        <div class="pseudocodice" markdown="0">
        <div class="pc-io"><span class="pc-kw">Input:</span> <span>Un array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> di <span class="arithmatex">&#92;(n&#92;)</span> numeri</span></div>
        <div class="pc-io"><span class="pc-kw">Output:</span> <span>Lo stesso array <span class="arithmatex">&#92;(a&#92;)</span> con gli elementi in ordine inverso</span></div>
        <div class="pc-sep"></div>
        <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
        <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>function</strong> ReverseArray(a, n)</span></span></div>
        <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i := 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(&#92;lfloor n/2 &#92;rfloor&#92;)</span> <strong>do</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(tmp := a&#91;i&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;i&#93; &#92;leftarrow a&#91;n - i + 1&#93;&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><span class="arithmatex">&#92;(a&#91;n - i + 1&#93; &#92;leftarrow tmp&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
        <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>return</strong> <span class="arithmatex">&#92;(a&#92;)</span></span></span></div>
        <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
        </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza 1:</strong> $a = [1, 2, 3, 4, 5]$, $n = 5$, $\lfloor 5/2 \rfloor = 2$ iterazioni

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th>scambio</th>
    <th>array <span class="arithmatex">&#92;(a&#92;)</span> (dopo lo scambio)</th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(&#91;1, 2, 3, 4, 5&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;1&#93; &#92;leftrightarrow a&#91;5&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;5, 2, 3, 4, 1&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;2&#93; &#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;5, 4, 3, 2, 1&#93;&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $a = [5, 4, 3, 2, 1]$

    <strong>Istanza 2:</strong> $a = [10, 20, 30, 40]$, $n = 4$, $\lfloor 4/2 \rfloor = 2$ iterazioni

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span></th>
    <th>scambio</th>
    <th>array <span class="arithmatex">&#92;(a&#92;)</span> (dopo lo scambio)</th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(&#91;10, 20, 30, 40&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;1&#93; &#92;leftrightarrow a&#91;4&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;40, 20, 30, 10&#93;&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(a&#91;2&#93; &#92;leftrightarrow a&#91;3&#93;&#92;)</span></td>
    <td><span class="arithmatex">&#92;(&#91;40, 30, 20, 10&#93;&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> $a = [40, 30, 20, 10]$

## 2.7 Insiemi

Gli array memorizzano valori in posizioni. Quando conta soltanto l'appartenenza dei valori, e non la loro posizione o le loro ripetizioni, si usa un insieme.

!!! chiave ""

    - Un <strong>insieme</strong> (<em>set</em>) è una collezione non ordinata di elementi <em>distinti</em>

    - Gli insiemi devono essere dichiarati prima dell'uso con l'operatore <strong>new set</strong>; non occorre specificare alcuna dimensione; appena creato, un insieme è vuoto

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t">nome_insieme <span class="arithmatex">&#92;(:=&#92;)</span> <strong>new set</strong></span></span></div>
    </div>

    I principali operatori sugli insiemi sono:

    - <strong>add</strong>: inserisce un elemento nell'insieme (ignorato se già presente)

        $$
        \textbf{add} \ x \ \textbf{to} \ \text{nome\_insieme}
        $$

    - <strong>remove</strong>: elimina un elemento dall'insieme (ignorato se non presente)

        $$
        \textbf{remove} \ x \ \textbf{from} \ \text{nome\_insieme}
        $$

    - <strong>in</strong>: test di appartenenza, che vale <strong>true</strong> se $x$ appartiene all'insieme

        $$
        x \ \textbf{in} \ \text{nome\_insieme}
        $$

    - <strong>size</strong>: cardinalità (numero di elementi attualmente nell'insieme)

        $$
        \textbf{size}(\text{nome\_insieme})
        $$

    - <strong>foreach</strong>: ciclo sugli elementi dell'insieme; per convenzione, in queste note gli elementi vengono visitati nell'ordine di inserimento

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>foreach</strong> <span class="arithmatex">&#92;(x&#92;)</span> <strong>in</strong> nome_insieme <strong>do</strong></span></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"></span><span class="pc-c">// elabora <span class="arithmatex">&#92;(x&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    - È possibile scorrere gli elementi di un insieme in un ordine specifico indicando un criterio di ordinamento:

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><strong>foreach</strong> <span class="arithmatex">&#92;(x&#92;)</span> <strong>in</strong> nome_insieme <strong>sorted by</strong> criterio <strong>do</strong></span></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"></span><span class="pc-c">// elabora <span class="arithmatex">&#92;(x&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

<a id="box-26-texexpbox29"></a>

!!! esempio "Esempio 2.24: dichiarazione e uso di un insieme"

    <div class="pseudocodice" markdown="0">
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Dichiara un insieme vuoto</span></span></div>
    <div class="pc-riga"><span class="pc-n">1</span><span class="pc-corpo"><span class="pc-t"><span class="arithmatex">&#92;(s := &#92;textbf{new set}&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Riempie l'insieme con i numeri pari da 1 a n</span></span></div>
    <div class="pc-riga"><span class="pc-n">2</span><span class="pc-corpo"><span class="pc-t"><strong>for</strong> <span class="arithmatex">&#92;(i:= 1&#92;)</span> <strong>to</strong>  <span class="arithmatex">&#92;(n&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">3</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(i &#92;bmod 2 = 0&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">4</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-l"></span><span class="pc-t"><strong>add</strong> <span class="arithmatex">&#92;(i&#92;)</span> <strong>to</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
    <div class="pc-riga"><span class="pc-n">5</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">6</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Test di appartenenza</span></span></div>
    <div class="pc-riga"><span class="pc-n">7</span><span class="pc-corpo"><span class="pc-t"><strong>if</strong> <span class="arithmatex">&#92;(4&#92;)</span> <strong>in</strong> <span class="arithmatex">&#92;(s&#92;)</span> <strong>then</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">8</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>print</strong>(4 appartiene a s)</span></span></div>
    <div class="pc-riga"><span class="pc-n">9</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Rimuove un elemento</span></span></div>
    <div class="pc-riga"><span class="pc-n">10</span><span class="pc-corpo"><span class="pc-t"><strong>remove</strong> <span class="arithmatex">&#92;(4&#92;)</span> <strong>from</strong> <span class="arithmatex">&#92;(s&#92;)</span></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Scorre e stampa tutti gli elementi rimasti</span></span></div>
    <div class="pc-riga"><span class="pc-n">11</span><span class="pc-corpo"><span class="pc-t"><strong>foreach</strong> <span class="arithmatex">&#92;(x&#92;)</span> <strong>in</strong> <span class="arithmatex">&#92;(s&#92;)</span> <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">12</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>print</strong>(<span class="arithmatex">&#92;(x&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">13</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Stampa la cardinalità</span></span></div>
    <div class="pc-riga"><span class="pc-n">14</span><span class="pc-corpo"><span class="pc-t"><strong>print</strong>(<strong>size</strong>(<span class="arithmatex">&#92;(s&#92;)</span>))</span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Stampa gli elementi in ordine non crescente</span></span></div>
    <div class="pc-riga"><span class="pc-n">15</span><span class="pc-corpo"><span class="pc-t"><strong>foreach</strong> <span class="arithmatex">&#92;(x&#92;)</span> <strong>in</strong> <span class="arithmatex">&#92;(s&#92;)</span> <strong>sorted by</strong> valore non crescente <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">16</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>print</strong>(<span class="arithmatex">&#92;(x&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">17</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    <div class="pc-riga pc-vuota"><span class="pc-n"></span><span class="pc-corpo"></span></div>
    <div class="pc-riga pc-solo-commento"><span class="pc-n"></span><span class="pc-corpo"><span class="pc-t"></span><span class="pc-c">// Stampa gli elementi in ordine non decrescente</span></span></div>
    <div class="pc-riga"><span class="pc-n">18</span><span class="pc-corpo"><span class="pc-t"><strong>foreach</strong> <span class="arithmatex">&#92;(x&#92;)</span> <strong>in</strong> <span class="arithmatex">&#92;(s&#92;)</span> <strong>sorted by</strong> valore non decrescente <strong>do</strong></span></span></div>
    <div class="pc-riga"><span class="pc-n">19</span><span class="pc-corpo"><span class="pc-l"></span><span class="pc-t"><strong>print</strong>(<span class="arithmatex">&#92;(x&#92;)</span>)</span></span></div>
    <div class="pc-riga"><span class="pc-n">20</span><span class="pc-corpo"><span class="pc-t"><strong>end</strong></span></span></div>
    </div>

    <strong>Esecuzione passo per passo:</strong>

    <strong>Istanza:</strong> $n = 8$

    - Passo 1: il ciclo for aggiunge $2, 4, 6, 8$, quindi $s = \{2, 4, 6, 8\}$.

    - Passo 2: $4$ appartiene a $s$: l'output è <code>4 appartiene a s</code>.

    - Passo 3: dopo la rimozione, $s = \{2, 6, 8\}$.

    - Passo 4: il primo <strong>foreach</strong> stampa $2, 6, 8$ (ordine di inserimento), poi viene stampata la cardinalità $3$.

    - Passo 5: gli ultimi due cicli stampano $8, 6, 2$ e $2, 6, 8$.

## 2.8 Convenzioni di stile

Concludiamo con un riepilogo della notazione usata in queste note, confrontata con altre scelte comuni.

!!! chiave ""

    Autori diversi possono usare convenzioni leggermente diverse:

    - Dichiarazione: $:=$ (usata in queste note) oppure $=$ (alcuni autori usano lo stesso simbolo sia per la dichiarazione sia per l'assegnamento)

    - Assegnamento: $\leftarrow$ (usato in queste note) oppure $=$

    - Indicizzazione di un array: $a[i]$ (usata in queste note) oppure $a_i$

    - Indicizzazione di un array bidimensionale: $b[i][j]$ (usata in queste note) oppure $b_{ij}$

    - Commenti: // commento, # commento, oppure (\* commento \*)

    <strong>L'importante è essere coerenti e chiari!</strong>

!!! chiave ""

    <strong>Punti chiave del capitolo.</strong>

    - Le variabili si dichiarano con $:=$ e si modificano con $\leftarrow$.

    - Le istruzioni condizionali e i cicli (<strong>if</strong>, <strong>while</strong>, <strong>for</strong>, con <strong>break</strong> e <strong>continue</strong>) controllano l'ordine di esecuzione.

    - Gli array $a[1..n]$, $b[1..m][1..n]$, … sono indicizzati da $1$ nello pseudocodice; gli insiemi memorizzano elementi distinti senza posizioni.

    - Un algoritmo si scrive come una <strong>funzione</strong> con il suo input (comprese le precondizioni), il suo output e un'istruzione <strong>return</strong>.
