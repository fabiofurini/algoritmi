---
title: "Introduzione a Python"
---

# Introduzione a Python

<div class="info-capitolo" markdown>

**Parte 2 · Linguaggi di programmazione · Capitolo 7** · [:material-file-pdf-box: Dispensa, volume 2 (PDF)](../pdf/dispensa-2-linguaggi-di-programmazione.pdf) · [:material-pencil: Esercizi: Introduzione a Python](../esercizi/es-07-introduzione-python.md)

</div>

## Introduzione

Nel capitolo «Introduzione a <code>C++</code>» abbiamo tradotto lo pseudocodice dei nostri algoritmi in un linguaggio di programmazione compilato. In questo capitolo introduciamo un secondo linguaggio di programmazione, <code>Python</code>, che è interpretato, ha una sintassi più leggera ed è molto diffuso sia nella didattica sia nel calcolo scientifico.

Il capitolo segue lo stesso percorso del capitolo «Introduzione a <code>C++</code>», in modo che i due linguaggi possano essere confrontati sezione per sezione:

- le caratteristiche principali del linguaggio e la struttura di un programma;

- variabili, tipi di dato, ingresso e uscita;

- operatori, istruzioni condizionali e cicli;

- le liste, che svolgono il ruolo degli array di <code>C++</code>;

- le funzioni, i loro parametri e i loro valori di ritorno;

- un algoritmo completo, la ricerca del valore massimo in un array, scritto in pseudocodice e in <code>Python</code>;

- gli operatori bit a bit e una tabella riassuntiva che confronta <code>Python</code> con <code>C++</code>.

Ogni frammento di codice del capitolo è stato eseguito con l'interprete <code>python3</code> (<code>Python 3.14</code>): gli output riportati negli esempi sono quelli stampati dai programmi.

!!! chiave ""

    Nello pseudocodice le componenti di un array $a[1..n]$ sono indicizzate da $1$ a $n$; in <code>Python</code>, come in <code>C++</code>, gli elementi di una lista di dimensione $n$ sono indicizzati da $0$ a $n-1$. La componente $a[i]$ dello pseudocodice corrisponde all'elemento <code>a[i-1]</code> del codice <code>Python</code>.

## 7.1 Caratteristiche principali del linguaggio di programmazione

Le caratteristiche principali di <code>Python</code> sono le seguenti.

- <code>Python</code> è un linguaggio <strong>interpretato</strong>: i programmi sono eseguiti istruzione per istruzione dall'<strong>interprete</strong> <code>Python</code>, senza una fase di compilazione separata. Questo rende lo sviluppo e il debug rapidi e interattivi.

- <code>Python</code> usa la <strong>tipizzazione dinamica</strong>: le variabili non devono essere dichiarate con un tipo di dato. Il tipo di dato è determinato automaticamente, durante l'esecuzione, dal valore assegnato.

- <code>Python</code> supporta le <strong>funzioni</strong>, che permettono un approccio strutturato e modulare alla programmazione. Le funzioni consentono di riutilizzare il codice e di organizzarlo meglio.

- <strong>L'indentazione è obbligatoria</strong> in <code>Python</code>: la struttura a blocchi del codice (cicli, istruzioni condizionali, funzioni) è definita dal livello di indentazione, non dalle parentesi graffe. L'indentazione standard è di $4$ spazi.

- In <code>Python</code>, un commento su una sola riga inizia con il simbolo riservato “<code>#</code>”. Non esiste un simbolo dedicato ai commenti su più righe: un testo racchiuso fra tripli apici <code>"""</code> (oppure <code>”'</code>) è una stringa che il programma non usa, e viene comunemente usato come commento su più righe. La stessa stringa, scritta come prima riga di una funzione, è la sua <strong>stringa di documentazione</strong> (<code>docstring</code>).

<a id="box-1-py-excomments"></a>

!!! esempio "Esempio 7.1: commenti in <code>Python</code>"

    Questo è un esempio di commento su una sola riga:

    ```python
    # Questa è una riga di commento
    ```

    Questo è un esempio di commento su più righe:

    ```python
    """
    Questo è un
    commento su più righe
    """
    ```

### 7.1.1 La struttura di un programma

Un programma <code>Python</code> è un file di testo (con estensione <code>.py</code>) che l'interprete esegue dalla prima riga all'ultima. A differenza di <code>C++</code>, non è richiesta una funzione <code>main</code>: le istruzioni scritte al livello più esterno del file sono eseguite in ordine.

<a id="box-2-py-exskeleton"></a>

!!! esempio "Esempio 7.2: lo scheletro di un programma"

    ```python
    # Qui si scrivono le istruzioni del programma
    print("Ciao, mondo!")
    ```

    Se il codice sorgente è salvato nel file <code>hello.py</code>, lo si esegue con il comando

    ```text
    python3 hello.py
    ```

    e l'output è

    ```text
    Ciao, mondo!
    ```

Negli esempi seguenti, a meno che non contengano un programma completo, i frammenti di codice sono scritti al livello più esterno di un file ed eseguiti in questo modo.

- Un <strong>blocco</strong> di istruzioni (il corpo di un'istruzione condizionale, di un ciclo o di una funzione) è introdotto dal simbolo “<code>:</code>” alla fine della riga precedente, e tutte le sue istruzioni sono indentate dello stesso numero di spazi. Il blocco termina alla prima istruzione indentata di meno.

<a id="box-3-py-exindent"></a>

!!! esempio "Esempio 7.3: blocchi definiti dall'indentazione"

    ```python
    x = 7
    if x > 0:
        print("positivo")           # Dentro il blocco dell'if
        print("ancora dentro")      # Dentro il blocco dell'if
    print("fuori dal blocco")       # Eseguita in ogni caso
    ```

    <strong>Output:</strong>

    ```text
    positivo
    ancora dentro
    fuori dal blocco
    ```

    In <code>C++</code> lo stesso blocco sarebbe racchiuso fra parentesi graffe <code>{}</code>; in <code>Python</code> un'indentazione sbagliata cambia il significato del programma o produce un <code>IndentationError</code>.

!!! chiave ""

    In <code>Python</code> le istruzioni non terminano con “<code>;</code>”, e i blocchi sono delimitati dall'indentazione (4 spazi) invece che dalle parentesi graffe.

## 7.2 Variabili e tipi di dato

Il codice sorgente opera su <strong>variabili</strong>, e ogni valore ha un <strong>tipo di dato</strong>.

- Le informazioni sono classificate in diversi <strong>tipi di dato</strong>. I quattro tipi di dato fondamentali sono:

    1. Il tipo di dato “<code>int</code>” rappresenta un numero intero, cioè un numero scritto senza la virgola decimale. Comprende i numeri interi positivi e negativi, e lo zero. A differenza di <code>C++</code>, gli interi di <code>Python</code> non hanno un valore massimo: possono avere tutte le cifre che servono.

    2. Il tipo di dato “<code>bool</code>” rappresenta un valore booleano: <code>True</code> o <code>False</code> (si noti l'iniziale maiuscola).

    3. Il tipo di dato “<code>float</code>” rappresenta un numero in virgola mobile, che comprende i numeri scritti con la virgola decimale. Un <code>float</code> di <code>Python</code> ha la stessa precisione (doppia) di un <code>double</code> di <code>C++</code>.

    4. Il tipo di dato “<code>str</code>” rappresenta una stringa di caratteri, racchiusa fra apici singoli o doppi (ad esempio <code>'ciao'</code>, <code>"mondo"</code>). Non esiste un tipo di dato separato per un singolo carattere: un carattere è una stringa di lunghezza $1$.

- Una variabile funziona come un contenitore che memorizza un valore. Ogni variabile ha un nome univoco.

- Alle variabili si assegnano valori con l'operatore di assegnamento “<code>=</code>”. Quando si assegna un nuovo valore, il valore precedente viene sovrascritto.

- <strong>Non serve alcuna dichiarazione</strong> prima dell'uso: una variabile viene creata nel momento in cui le si assegna un valore. La funzione <code>type()</code> restituisce il tipo di dato di un valore.

!!! chiave ""

    Le variabili sono create tramite assegnamento; non c'è una fase di dichiarazione separata, e il tipo di dato non è scritto nel codice.

<a id="box-4-py-exvariables"></a>

!!! esempio "Esempio 7.4: assegnamenti di variabili"

    ```python
    age = 25                   # Variabile intera
    is_raining = False         # Variabile booleana
    small_number = 3.14        # Variabile in virgola mobile
    large_number = 123456.789  # Variabile in virgola mobile
    character = 'a'            # Variabile stringa (un solo carattere)
    name = "Alice"             # Variabile stringa

    age = 26  # Il valore precedente 25 viene sovrascritto
    print(age, is_raining, small_number, large_number, character, name)
    print(type(age), type(is_raining), type(small_number), type(name))
    ```

    <strong>Output:</strong>

    ```text
    26 False 3.14 123456.789 a Alice
    <class 'int'> <class 'bool'> <class 'float'> <class 'str'>
    ```

    Si confronti con l'[Esempio 7.6](#box-6-py-exprint) più avanti e con l'esempio corrispondente del capitolo «Introduzione a <code>C++</code>»: il valore booleano è visualizzato come <code>False</code>, e il numero <code>123456.789</code> è visualizzato con tutte le sue cifre.

<a id="box-5-py-exdynamic"></a>

!!! esempio "Esempio 7.5: tipizzazione dinamica e interi grandi"

    ```python
    x = 5
    print(x, type(x))
    x = "cinque"  # Lo stesso nome ora si riferisce a una stringa
    print(x, type(x))

    print(2 ** 100)  # Un intero con 31 cifre
    ```

    <strong>Output:</strong>

    ```text
    5 <class 'int'>
    cinque <class 'str'>
    1267650600228229401496703205376
    ```

    L'operatore <code>\*\*</code> è l'elevamento a potenza (Sezione [7.4.1](#sez-py-secarith)). In <code>C++</code> il valore $2^{100}$ non entra in una variabile di tipo <code>int</code>.

## 7.3 Ingresso e uscita

- La funzione <code>print()</code> visualizza un output sullo schermo. Più valori possono essere stampati in una sola chiamata separandoli con virgole: sono visualizzati separati da uno spazio, e la riga termina con un a capo (lo stesso effetto di <code>endl</code> in <code>C++</code>).

- I parametri opzionali <code>sep</code> e <code>end</code> cambiano il separatore fra i valori e il testo scritto alla fine: <code>print(x, end=" ")</code> scrive uno spazio invece dell'a capo, così la <code>print</code> successiva continua sulla stessa riga.

- Le stringhe e i valori delle variabili possono essere combinati usando le <strong>f-string</strong> (stringhe formattate), precedute dalla lettera <code>f</code>. Dentro le f-string i nomi delle variabili (e, più in generale, le espressioni) si scrivono fra parentesi graffe <code>{}</code>.

- Dentro le parentesi graffe di una f-string, il formato <code>:.kf</code> visualizza un numero in virgola mobile con esattamente $k$ cifre dopo la virgola decimale (lo stesso effetto di <code>fixed</code> e <code>setprecision(k)</code> in <code>C++</code>).

<a id="box-6-py-exprint"></a>

!!! esempio "Esempio 7.6: stampe sullo schermo"

    ```python
    n = 42
    print("Il valore della variabile è", n)
    print(f"Il valore della variabile è {n}")  # Versione con f-string
    print(f"n = {n}, doppio = {n * 2}")        # Espressione dentro {}

    print("a", "b", "c", sep="-")   # Separatore "-" invece dello spazio
    print("Niente a capo", end=" ") # Uno spazio invece dell'a capo
    print("dopo end")
    print(f"{10 / 3:.2f}")          # Due cifre dopo la virgola decimale
    ```

    <strong>Output:</strong>

    ```text
    Il valore della variabile è 42
    Il valore della variabile è 42
    n = 42, doppio = 84
    a-b-c
    Niente a capo dopo end
    3.33
    ```

- La funzione <code>input()</code> visualizza un messaggio, attende che l'utente scriva una riga di testo e la restituisce. Restituisce sempre una <code>str</code>; per ottenere un numero, il risultato deve essere convertito con <code>int()</code> o <code>float()</code>.

<a id="box-7-py-exinput"></a>

!!! esempio "Esempio 7.7: ingresso da tastiera"

    ```python
    name = input("Inserisci il tuo nome: ")             # Legge una stringa
    n = int(input("Inserisci un intero: "))             # Legge e converte in int
    x = float(input("Inserisci un numero reale: "))     # Legge e converte in float
    print(f"Ciao {name}, n = {n}, x = {x}")
    ```

    <strong>Esempio di esecuzione</strong> (l'utente scrive <code>Ada</code>, <code>7</code> e <code>2.5</code>):

    ```text
    Inserisci il tuo nome: Ada
    Inserisci un intero: 7
    Inserisci un numero reale: 2.5
    Ciao Ada, n = 7, x = 2.5
    ```

## 7.4 Operatori

Gli operatori sono simboli che eseguono operazioni su variabili e valori. Come in <code>C++</code>, sono classificati, secondo la loro funzione, in operatori aritmetici, di assegnamento, relazionali e logici; <code>Python</code> non ha operatori di incremento e decremento.

### 7.4.1 Operatori aritmetici { #sez-py-secarith }

!!! chiave ""

    <strong>Operatori aritmetici</strong>, usati per eseguire le operazioni matematiche di base:

    - <code>+</code> (Addizione) $\rightsquigarrow$ Somma due valori.

    - <code>-</code> (Sottrazione) $\rightsquigarrow$ Sottrae un valore da un altro.

    - <code>\*</code> (Moltiplicazione) $\rightsquigarrow$ Moltiplica due valori.

    - <code>/</code> (Divisione) $\rightsquigarrow$ Divide un valore per un altro (restituisce sempre un <code>float</code>).

    - <code>//</code> (Divisione intera) $\rightsquigarrow$ Restituisce il quoziente intero (divisione con arrotondamento per difetto).

    - <code>%</code> (Resto) $\rightsquigarrow$ Restituisce il resto di una divisione.

    - <code>\*\*</code> (Elevamento a potenza) $\rightsquigarrow$ Eleva un valore a una potenza.

<a id="box-8-py-exarith"></a>

!!! esempio "Esempio 7.8: operatori aritmetici"

    ```python
    a = 10
    b = 3

    print("Addizione:", a + b)
    print("Sottrazione:", a - b)
    print("Moltiplicazione:", a * b)
    print("Divisione:", a / b)          # Sempre un float
    print("Divisione intera:", a // b)
    print("Resto:", a % b)
    print("Elevamento a potenza:", a ** b)
    ```

    <strong>Output:</strong>

    ```text
    Addizione: 13
    Sottrazione: 7
    Moltiplicazione: 30
    Divisione: 3.3333333333333335
    Divisione intera: 3
    Resto: 1
    Elevamento a potenza: 1000
    ```

    L'ultima cifra <code>5</code> della divisione non è un errore del programma: $10/3$ ha infinite cifre decimali, e viene visualizzato il <code>float</code> più vicino.

- L'operatore di divisione <code>/</code> restituisce sempre un <code>float</code> in <code>Python 3</code>, anche quando divide due interi. Per ottenere un risultato intero si usa l'operatore di divisione intera <code>//</code>. È la convenzione opposta rispetto a <code>C++</code>, dove <code>10 / 3</code> è la divisione intera.

- L'operatore <code>//</code> calcola $\lfloor a/b \rfloor$, arrotondando per difetto. Per operandi non negativi coincide con la divisione intera di <code>C++</code>; per un quoziente negativo non coincide, perché <code>C++</code> tronca verso lo zero: in <code>Python</code> <code>-7 // 2</code> vale <code>-4</code> e <code>-7 % 2</code> vale <code>1</code>, mentre in <code>C++</code> <code>-7 / 2</code> vale <code>-3</code> e <code>-7 % 2</code> vale <code>-1</code>. In entrambi i linguaggi vale l'identità $a = b \cdot q + r$ fra quoziente $q$ e resto $r$.

- Un valore è convertito in un altro tipo di dato (<strong>conversione di tipo</strong>) con le funzioni <code>int()</code>, <code>float()</code> e <code>str()</code>: <code>int(3.9)</code> vale <code>3</code> (la parte decimale è eliminata), <code>float(7)</code> vale <code>7.0</code>, <code>int("12")</code> è l'intero <code>12</code>.

<a id="box-9-py-exdivision"></a>

!!! esempio "Esempio 7.9: divisione intera e in virgola mobile"

    ```python
    a = 10
    b = 3

    print(a / b)             # Divisione in virgola mobile
    print(a // b)            # Divisione intera
    print(f"{a / b:.2f}")    # Due cifre decimali
    print(-7 // 2, -7 % 2)   # Divisione per difetto con quoziente negativo
    print(int(-7 / 2))       # Troncamento verso zero, come in C++
    print(int(3.9), float(7), int("12") + 1)
    ```

    <strong>Output:</strong>

    ```text
    3.3333333333333335
    3
    3.33
    -4 1
    -3
    3 7.0 13
    ```

### 7.4.2 Operatori di assegnamento

!!! chiave ""

    <strong>Operatori di assegnamento</strong>, usati per assegnare valori alle variabili:

    - <code>=</code>  (Assegnamento) $\rightsquigarrow$ Assegna un valore a una variabile.

    - <code>+=</code> (Assegnamento con addizione) $\rightsquigarrow$ Somma un valore e assegna il risultato.

    - <code>-=</code> (Assegnamento con sottrazione) $\rightsquigarrow$ Sottrae un valore e assegna il risultato.

    - <code>\*=</code> (Assegnamento con moltiplicazione) $\rightsquigarrow$ Moltiplica e assegna il risultato.

    - <code>/=</code> (Assegnamento con divisione) $\rightsquigarrow$ Divide e assegna il risultato (un <code>float</code>).

    - <code>//=</code> (Assegnamento con divisione intera) $\rightsquigarrow$ Divide per difetto e assegna il risultato.

    - <code>%=</code> (Assegnamento con resto) $\rightsquigarrow$ Calcola il resto e assegna il risultato.

    - <code>\*\*=</code> (Assegnamento con elevamento a potenza) $\rightsquigarrow$ Eleva a una potenza e assegna il risultato.

<a id="box-10-py-exassign"></a>

!!! esempio "Esempio 7.10: operatori di assegnamento"

    ```python
    x = 10  # Assegnamento
    print("Valore iniziale:", x)

    x += 5   # Equivalente a: x = x + 5
    print("Dopo += 5:", x)

    x -= 3   # Equivalente a: x = x - 3
    print("Dopo -= 3:", x)

    x *= 2   # Equivalente a: x = x * 2
    print("Dopo *= 2:", x)

    x //= 4  # Equivalente a: x = x // 4
    print("Dopo //= 4:", x)

    x %= 4   # Equivalente a: x = x % 4
    print("Dopo %= 4:", x)

    x **= 3  # Equivalente a: x = x ** 3
    print("Dopo **= 3:", x)

    x /= 4   # Equivalente a: x = x / 4 (il risultato è un float)
    print("Dopo /= 4:", x)
    ```

    <strong>Output:</strong>

    ```text
    Valore iniziale: 10
    Dopo += 5: 15
    Dopo -= 3: 12
    Dopo *= 2: 24
    Dopo //= 4: 6
    Dopo %= 4: 2
    Dopo **= 3: 8
    Dopo /= 4: 2.0
    ```

### 7.4.3 Incremento e decremento

- <code>Python</code> non ha gli operatori <code>++</code> e <code>- -</code>: una variabile si incrementa con <code>x += 1</code> e si decrementa con <code>x -= 1</code>.

- L'istruzione <code>x++</code> è un errore di sintassi. L'espressione <code>++x</code> è accettata, ma non incrementa <code>x</code>: applica due volte il più unario, quindi il suo valore è <code>x</code> stesso.

<a id="box-11-py-exincdec"></a>

!!! esempio "Esempio 7.11: incremento e decremento"

    ```python
    x = 5
    x += 1          # Incremento
    print("Dopo x += 1:", x)
    x -= 1          # Decremento
    print("Dopo x -= 1:", x)
    print("++x vale", ++x, "e x vale ancora", x)  # ++x non è un incremento
    ```

    <strong>Output:</strong>

    ```text
    Dopo x += 1: 6
    Dopo x -= 1: 5
    ++x vale 5 e x vale ancora 5
    ```

### 7.4.4 Operatori relazionali

!!! chiave ""

    <strong>Operatori relazionali</strong>, usati per confrontare valori e restituire un risultato booleano:

    - <code>==</code> (Uguale a) $\rightsquigarrow$ Verifica se due valori sono uguali.

    - <code>!=</code> (Diverso da) $\rightsquigarrow$ Verifica se due valori sono diversi.

    - <code>&lt;</code>  (Minore di) $\rightsquigarrow$ Verifica se un valore è minore di un altro.

    - <code>&gt;</code>  (Maggiore di) $\rightsquigarrow$ Verifica se un valore è maggiore di un altro.

    - <code>&lt;=</code> (Minore o uguale a) $\rightsquigarrow$ Verifica se un valore è minore o uguale a un altro.

    - <code>&gt;=</code> (Maggiore o uguale a) $\rightsquigarrow$ Verifica se un valore è maggiore o uguale a un altro.

- Gli operatori relazionali restituiscono un risultato booleano: <code>True</code> se la condizione è soddisfatta, <code>False</code> altrimenti (visualizzati come <code>True</code> e <code>False</code>, non come <code>1</code> e <code>0</code> come in <code>C++</code>). Questi operatori sono usati comunemente nelle <strong>istruzioni condizionali</strong> e nei <strong>cicli</strong>.

- I confronti possono essere concatenati: <code>0 &lt; x &lt;= 10</code> significa <code>0 &lt; x and x &lt;= 10</code>.

<a id="box-12-py-excompare"></a>

!!! esempio "Esempio 7.12: operatori relazionali"

    ```python
    a = 10
    b = 5

    print("a == b:", a == b)  # Uguale a
    print("a != b:", a != b)  # Diverso da
    print("a < b:", a < b)    # Minore di
    print("a > b:", a > b)    # Maggiore di
    print("a <= b:", a <= b)  # Minore o uguale a
    print("a >= b:", a >= b)  # Maggiore o uguale a
    print("0 < b <= a:", 0 < b <= a)  # Confronto concatenato
    ```

    <strong>Output:</strong>

    ```text
    a == b: False
    a != b: True
    a < b: False
    a > b: True
    a <= b: False
    a >= b: True
    0 < b <= a: True
    ```

### 7.4.5 Operatori logici

!!! chiave ""

    <strong>Operatori logici</strong>, usati per le operazioni logiche, spesso nelle istruzioni condizionali:

    - <code>and</code> (AND logico) $\rightsquigarrow$ Restituisce <code>True</code> se entrambe le condizioni sono <code>True</code>.

    - <code>or</code>  (OR logico)  $\rightsquigarrow$ Restituisce <code>True</code> se almeno una condizione è <code>True</code>.

    - <code>not</code> (NOT logico) $\rightsquigarrow$ Inverte il valore booleano.

- Gli operatori logici di <code>Python</code> sono parole, mentre in <code>C++</code> sono i simboli <code>&amp;&amp;</code>, <code>||</code> e <code>!</code>.

<a id="box-13-py-exlogic"></a>

!!! esempio "Esempio 7.13: operatori logici"

    ```python
    condition1 = True
    condition2 = False

    print("condition1:", condition1)
    print("condition2:", condition2)

    # AND logico: True solo se entrambe le condizioni sono True
    print("condition1 and condition2:", condition1 and condition2)

    # OR logico: True se almeno una condizione è True
    print("condition1 or condition2:", condition1 or condition2)

    # NOT logico: inverte il valore booleano
    print("not condition1:", not condition1)
    print("not condition2:", not condition2)
    ```

    <strong>Output:</strong>

    ```text
    condition1: True
    condition2: False
    condition1 and condition2: False
    condition1 or condition2: True
    not condition1: False
    not condition2: True
    ```

## 7.5 Istruzioni condizionali

Gli operatori relazionali e logici producono le condizioni che decidono quali istruzioni vengono eseguite.

- Le istruzioni condizionali permettono di eseguire blocchi di codice diversi in base a condizioni specifiche.

- L'istruzione <code>if</code> valuta una condizione. Se la condizione è <code>True</code>, il blocco indentato viene eseguito.

- La clausola opzionale <code>elif</code> (else if) verifica una condizione aggiuntiva quando le precedenti sono <code>False</code>.

- La clausola opzionale <code>else</code> viene eseguita quando tutte le condizioni precedenti sono <code>False</code>.

- <strong>Non servono parentesi</strong> attorno alla condizione, e <strong>non si usano parentesi graffe</strong>: la riga della condizione termina con “<code>:</code>” e il blocco è delimitato dall'indentazione.

<a id="box-14-py-exif"></a>

!!! esempio "Esempio 7.14: istruzione condizionale"

    ```python
    number = 10

    # Verifica se il numero è positivo
    if number > 0:
        print("Il numero è positivo.")
    else:
        print("Il numero non è positivo.")
    ```

    <strong>Output:</strong>

    ```text
    Il numero è positivo.
    ```

<a id="box-15-py-exelif"></a>

!!! esempio "Esempio 7.15: <code>if</code> / <code>elif</code> / <code>else</code>"

    ```python
    score = 85

    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"

    print(f"Punteggio: {score}, Voto: {grade}")
    ```

    <strong>Output:</strong>

    ```text
    Punteggio: 85, Voto: B
    ```

    Le condizioni sono valutate dall'alto verso il basso, e viene eseguito solo il blocco della prima condizione vera: <code>score &gt;= 90</code> è falsa e <code>score &gt;= 80</code> è vera, quindi il voto è <code>"B"</code>. Il risultato è lo stesso degli operatori ternari annidati del capitolo «Introduzione a <code>C++</code>».

### 7.5.1 Espressione condizionale

- L'<strong>espressione condizionale</strong> è la versione <code>Python</code> dell'operatore ternario <code>?:</code> di <code>C++</code>: offre un modo compatto per scrivere semplici istruzioni <code>if-else</code>.

- Sintassi: <code>valore\_se\_vero if condizione else valore\_se\_falso</code>

- Se la condizione è <code>True</code>, l'espressione vale <code>valore\_se\_vero</code>; altrimenti vale <code>valore\_se\_falso</code>.

<a id="box-16-py-externary"></a>

!!! esempio "Esempio 7.16: espressione condizionale"

    ```python
    number = 10

    # Espressione condizionale compatta
    result = "positivo" if number > 0 else "non positivo"
    print(f"Il numero è {result}")

    # Ricerca del massimo fra due numeri
    a, b = 15, 20  # Assegnamento multiplo: a = 15 e b = 20
    maximum = a if a > b else b
    print(f"Massimo: {maximum}")

    # Verifica se pari o dispari
    n = 7
    parity = "pari" if n % 2 == 0 else "dispari"
    print(f"{n} è {parity}")

    # Valore assoluto
    x = -5
    abs_value = x if x >= 0 else -x
    print(f"Il valore assoluto di {x} è {abs_value}")
    ```

    <strong>Output:</strong>

    ```text
    Il numero è positivo
    Massimo: 20
    7 è dispari
    Il valore assoluto di -5 è 5
    ```

    La libreria di <code>Python</code> fornisce anche le funzioni <code>max(a, b)</code> e <code>abs(x)</code>, che restituiscono gli stessi valori.

## 7.6 Cicli

Le istruzioni condizionali scelgono <em>se</em> un blocco di codice viene eseguito; i cicli decidono <em>quante volte</em> viene eseguito.

- I cicli servono a eseguire ripetutamente un blocco di codice. In <code>Python</code> i due costrutti di ciclo sono il ciclo <code>while</code> e il ciclo <code>for</code>.

### 7.6.1 Il ciclo <code>while</code>

- Il ciclo <code>while</code> esegue un blocco di codice finché la condizione vale <code>True</code>. Se la condizione è <code>False</code> fin dall'inizio, il blocco non viene mai eseguito.

<a id="box-17-py-exwhile"></a>

!!! esempio "Esempio 7.17: ciclo <code>while</code>"

    ```python
    i = 1              # Inizializzazione

    while i <= 5:      # Condizione
        print(f"Numero: {i}")
        i += 1         # Incremento (in Python non esiste l'operatore ++)
    ```

    <strong>Output:</strong>

    ```text
    Numero: 1
    Numero: 2
    Numero: 3
    Numero: 4
    Numero: 5
    ```

    Come in <code>C++</code>, la condizione <code>i &lt;= 5</code> è valutata sei volte: cinque volte è vera, e la sesta volta (<code>i</code> uguale a <code>6</code>) è falsa e il ciclo termina.

### 7.6.2 Il ciclo <code>for</code>

- Il ciclo <code>for</code> di <code>Python</code> scorre gli elementi di un <strong>iterabile</strong>, come una lista, una stringa o un intervallo di interi: a ogni iterazione la variabile del ciclo assume l'elemento successivo.

- La funzione <code>range(start, stop, step)</code> genera la sequenza di interi da <code>start</code> (incluso) a <code>stop</code> (escluso), con incremento <code>step</code>. Se è dato un solo argomento, la sequenza parte da $0$; se <code>step</code> è omesso, vale $1$; con un <code>step</code> negativo la sequenza decresce.

- Il ciclo dello pseudocodice “<strong>for</strong> $i := 1$ <strong>to</strong> $n$” corrisponde a <code>for i in range(1, n + 1)</code>, e il ciclo sugli indici di una lista di dimensione $n$ è <code>for i in range(n)</code>, con $i = 0, 1, \dots, n-1$.

<a id="box-18-py-exfor"></a>

!!! esempio "Esempio 7.18: ciclo <code>for</code> con <code>range</code>"

    ```python
    for i in range(1, 6):   # i assume i valori 1, 2, 3, 4, 5
        print(f"Numero: {i}")
    ```

    L'output è lo stesso del ciclo <code>while</code> dell'[Esempio 7.17](#box-17-py-exwhile). La funzione <code>list()</code> mostra gli interi generati da un <code>range</code>:

    ```python
    print(list(range(5)))
    print(list(range(1, 6)))
    print(list(range(0, 10, 3)))
    print(list(range(5, 0, -1)))
    ```

    <strong>Output:</strong>

    ```text
    [0, 1, 2, 3, 4]
    [1, 2, 3, 4, 5]
    [0, 3, 6, 9]
    [5, 4, 3, 2, 1]
    ```

<a id="box-19-py-exforlist"></a>

!!! esempio "Esempio 7.19: ciclo <code>for</code> su una lista"

    ```python
    a = [3, 7, 2, 9, 5]

    for element in a:
        print(element)
    ```

    <strong>Output:</strong>

    ```text
    3
    7
    2
    9
    5
    ```

    Il ciclo visita direttamente gli elementi, senza usare i loro indici.

### 7.6.3 Le istruzioni <code>break</code> e <code>continue</code>

- L'istruzione <code>break</code> termina immediatamente il ciclo.

- L'istruzione <code>continue</code> salta il resto dell'iterazione corrente e passa alla successiva.

<a id="box-20-py-exbreak"></a>

!!! esempio "Esempio 7.20: <code>break</code> e <code>continue</code>"

    ```python
    for i in range(1, 11):
        if i % 2 == 0:
            continue  # Salta i numeri pari
        if i > 7:
            break     # Interrompe il ciclo al primo dispari maggiore di 7
        print(i, end=" ")
    print()
    ```

    <strong>Output:</strong>

    ```text
    1 3 5 7
    ```

    Come nella versione <code>C++</code>, i valori pari di <code>i</code> sono saltati da <code>continue</code>; quando <code>i</code> è uguale a <code>9</code> l'istruzione <code>break</code> termina il ciclo, e il valore <code>10</code> non viene mai raggiunto. L'ultima <code>print()</code> scrive solo l'a capo.

## 7.7 Liste

I cicli diventano davvero utili quando visitano collezioni di valori. In <code>Python</code> una collezione di valori è memorizzata in una <strong>lista</strong>.

- Una <strong>lista</strong> è una collezione ordinata e modificabile di elementi, che può contenere valori di qualunque tipo. Le liste sono la principale struttura dati sequenziale di <code>Python</code> e svolgono il ruolo degli array di <code>C++</code>.

- Le liste sono racchiuse fra parentesi quadre <code>[]</code> e gli elementi sono separati da virgole. Gli elementi si raggiungono tramite il loro <strong>indice</strong>, a partire da <code>0</code>: gli elementi di una lista <code>a</code> di dimensione $n$ sono <code>a[0]</code>, <code>a[1]</code>, …, <code>a[n-1]</code>. La funzione <code>len(a)</code> restituisce la dimensione della lista, e l'indice negativo <code>a[-1]</code> indica l'ultimo elemento.

- A differenza degli array di <code>C++</code>, le liste sono <strong>dinamiche</strong>: possono crescere o ridursi durante l'esecuzione senza gestire manualmente la memoria. L'istruzione <code>a.append(x)</code> aggiunge l'elemento <code>x</code> in fondo alla lista.

- L'espressione <code>[0] \* n</code> crea una lista di $n$ zeri. Più in generale, una <strong>list comprehension</strong> <code>[espressione for i in range(n)]</code> crea la lista degli $n$ valori dell'espressione per $i = 0, 1, \dots, n-1$; quando la variabile del ciclo non è usata, per convenzione si chiama <code>\_</code>.

!!! chiave ""

    Le liste si creano con <code>[]</code> e si indicizzano a partire da <code>0</code>. Non servono né l'allocazione né la deallocazione della memoria.

<a id="box-21-py-exlist"></a>

!!! esempio "Esempio 7.21: creazione e accesso a una lista"

    ```python
    n = 5

    # Crea una lista di n zeri
    a = [0] * n

    # Assegna i valori
    for i in range(n):
        a[i] = i * 2

    print(a)       # L'intera lista
    print(a[0])    # Primo elemento
    print(a[4])    # Ultimo elemento, indice n-1
    print(len(a))  # Numero di elementi
    ```

    <strong>Output:</strong>

    ```text
    [0, 2, 4, 6, 8]
    0
    8
    5
    ```

<a id="box-22-py-exlistlit"></a>

!!! esempio "Esempio 7.22: lista scritta per esteso, modifica e crescita"

    ```python
    b = [9, 12, 3, 16]   # Lista di 4 interi

    b[2] = 5             # Assegna un nuovo valore al terzo elemento
    b.append(20)         # La lista cresce: ora ha 5 elementi
    print(b, len(b))
    print(b[-1])         # L'ultimo elemento

    squares = [i * i for i in range(6)]  # List comprehension
    print(squares)
    ```

    <strong>Output:</strong>

    ```text
    [9, 12, 5, 16, 20] 5
    20
    [0, 1, 4, 9, 16, 25]
    ```

    Accedere a un indice che non esiste, per esempio <code>b[5]</code>, ferma il programma con l'errore <code>IndexError: list index out of range</code> (in <code>C++</code> lo stesso accesso non è controllato).

<a id="box-23-py-exlistiter"></a>

!!! esempio "Esempio 7.23: lista scritta per esteso e iterazione sugli indici"

    ```python
    a = [9, 12, 3, 16, 19, 11, 12]
    n = len(a)

    for i in range(n):
        print(f"a[{i}] = {a[i]}")
    ```

    <strong>Output:</strong>

    ```text
    a[0] = 9
    a[1] = 12
    a[2] = 3
    a[3] = 16
    a[4] = 19
    a[5] = 11
    a[6] = 12
    ```

### 7.7.1 Liste bidimensionali

- I dati bidimensionali possono essere rappresentati con una <strong>lista di liste</strong>. Ogni riga è a sua volta una lista, e gli elementi si raggiungono con due indici <code>matrix[i][j]</code>, entrambi a partire da $0$: per esempio, se <code>c = [[3, 1, 4], [1, 5, 9]]</code>, allora <code>c[1][2]</code> è l'elemento nella seconda riga e terza colonna, uguale a $9$.

- Una matrice di $m$ righe e $n$ colonne riempita di zeri si crea con la list comprehension <code>[[0] \* n for \_ in range(m)]</code>, che costruisce $m$ righe distinte.

<a id="box-24-py-exmatrix"></a>

!!! esempio "Esempio 7.24: lista bidimensionale (matrice)"

    ```python
    m = 3   # Numero di righe
    n = 2   # Numero di colonne

    # Crea una matrice di zeri
    matrix = [[0] * n for _ in range(m)]

    # Assegna i valori
    for i in range(m):
        for j in range(n):
            matrix[i][j] = i * j

    # Stampa la matrice
    for i in range(m):
        for j in range(n):
            print(f"matrix[{i}][{j}] = {matrix[i][j]}")
    print(matrix)
    ```

    <strong>Output:</strong>

    ```text
    matrix[0][0] = 0
    matrix[0][1] = 0
    matrix[1][0] = 0
    matrix[1][1] = 1
    matrix[2][0] = 0
    matrix[2][1] = 2
    [[0, 0], [0, 1], [0, 2]]
    ```

- L'espressione più breve <code>[[0] \* n] \* m</code> è sbagliata: ripete $m$ volte la <em>stessa</em> riga, quindi una modifica a una riga compare in tutte le righe.

<a id="box-25-py-exalias"></a>

!!! esempio "Esempio 7.25: un errore frequente con le liste bidimensionali"

    ```python
    wrong = [[0] * 2] * 3                  # Tre riferimenti alla stessa riga
    wrong[0][0] = 1
    print(wrong)

    right = [[0] * 2 for _ in range(3)]    # Tre righe distinte
    right[0][0] = 1
    print(right)
    ```

    <strong>Output:</strong>

    ```text
    [[1, 0], [1, 0], [1, 0]]
    [[1, 0], [0, 0], [0, 0]]
    ```

## 7.8 Funzioni

Come nello pseudocodice, un algoritmo è scritto come una funzione che riceve l'input e restituisce l'output.

- Le funzioni permettono di scrivere codice modulare e riutilizzabile, raggruppando le istruzioni in una sola unità. Una funzione si definisce con la parola chiave <code>def</code>, seguita dal nome della funzione e dall'elenco dei parametri fra parentesi, e termina con il simbolo “<code>:</code>”.

- Una funzione in <code>Python</code> è composta da:

    1. la parola chiave <code>def</code> seguita dal <strong>nome della funzione</strong>;

    2. un <strong>elenco di parametri</strong> (opzionale): specifica i valori in ingresso, senza i loro tipi di dato;

    3. un <strong>corpo</strong> indentato: il blocco di codice eseguito quando la funzione viene chiamata;

    4. un'istruzione <code>return</code> (opzionale): restituisce un valore a chi chiama la funzione. Una funzione senza <code>return</code> restituisce il valore speciale <code>None</code>.

- Una funzione deve essere definita prima che venga eseguita l'istruzione che la chiama: per questo motivo le funzioni sono scritte all'inizio del file.

- Le istruzioni principali di un programma <code>Python</code> sono tipicamente poste al livello più esterno del file, oppure dentro un blocco protetto da <code>if \_\_name\_\_ == "\_\_main\_\_":</code>, che garantisce che il codice venga eseguito solo quando il file è eseguito direttamente (e non quando è importato come modulo da un altro file). Questo blocco svolge il ruolo della funzione <code>main</code> di <code>C++</code>.

- Il codice sorgente <code>Python</code> può anche essere eseguito online, per esempio al seguente indirizzo:<br> [www.mycompiler.io/online-python-compiler](https://www.mycompiler.io/online-python-compiler)

<a id="box-26-py-exfunctions"></a>

!!! esempio "Esempio 7.26: funzioni"

    ```python
    # Definizione di funzione
    def addition(a, b):
        return a + b  # Restituisce la somma

    # Definizione di funzione
    def multiplication(a, b):
        return a * b  # Restituisce il prodotto

    if __name__ == "__main__":
        total = addition(5, 10)          # Chiamata di funzione
        print(f"Somma: {total}")

        product = multiplication(5, 10)  # Chiamata di funzione
        print(f"Prodotto: {product}")
    ```

    <strong>Output:</strong>

    ```text
    Somma: 15
    Prodotto: 50
    ```

<a id="box-27-py-exsummatrix"></a>

!!! esempio "Esempio 7.27: funzione che opera su una lista bidimensionale"

    ```python
    def sum_matrix(matrix, rows, columns):
        """Restituisce la somma di tutti gli elementi di una lista 2D."""
        total = 0
        for i in range(rows):
            for j in range(columns):
                total += matrix[i][j]
        return total

    if __name__ == "__main__":
        m, n = 3, 2

        # Costruisce la matrice con una list comprehension annidata
        matrix = [[i * j for j in range(n)] for i in range(m)]

        result = sum_matrix(matrix, m, n)
        print(f"Somma degli elementi della matrice: {result}")
    ```

    <strong>Output:</strong>

    ```text
    Somma degli elementi della matrice: 3
    ```

    La matrice è <code>[[0, 0], [0, 1], [0, 2]]</code>, come nell'[Esempio 7.24](#box-24-py-exmatrix), e la somma dei suoi elementi è $0+0+0+1+0+2 = 3$.

### 7.8.1 Parametri e valori di ritorno

In <code>C++</code> i parametri sono passati per valore o per riferimento. In <code>Python</code> ogni parametro riceve lo <em>stesso</em> oggetto che è l'argomento di chi chiama, e l'effetto di una funzione su chi la chiama dipende da ciò che la funzione fa con esso.

- Se la funzione <strong>assegna un nuovo valore</strong> a un parametro (per esempio <code>x = x + 1</code>), cambia solo il nome locale: la variabile di chi chiama non è toccata. Per i numeri, il comportamento è lo stesso dei parametri passati per valore in <code>C++</code>.

- Se la funzione <strong>modifica gli elementi</strong> di una lista ricevuta come parametro (per esempio <code>a[i] = 0</code>), la modifica è visibile a chi chiama, come per gli array passati a una funzione in <code>C++</code>.

- Una funzione può restituire <strong>più valori</strong> contemporaneamente, separati da virgole: sono restituiti come una <strong>tupla</strong>, e chi chiama li assegna a più variabili con un assegnamento multiplo. In <code>C++</code> lo stesso risultato richiede parametri passati per riferimento.

<a id="box-28-py-exparams"></a>

!!! esempio "Esempio 7.28: parametri e valori di ritorno multipli"

    ```python
    def increment(x):
        x = x + 1           # Cambia solo il nome locale x

    def fill_with_zeros(a):
        for i in range(len(a)):
            a[i] = 0        # Modifica la lista di chi chiama

    def divide(n, m):
        return n // m, n % m  # Restituisce due valori (una tupla)

    if __name__ == "__main__":
        k = 5
        increment(k)
        print("Dopo increment:", k)

        b = [4, 7, 1]
        fill_with_zeros(b)
        print("Lista:", b)

        q, r = divide(17, 5)
        print("Quoziente e resto:", q, r)
        print("Tupla:", divide(17, 5))
    ```

    <strong>Output:</strong>

    ```text
    Dopo increment: 5
    Lista: [0, 0, 0]
    Quoziente e resto: 3 2
    Tupla: (3, 2)
    ```

## 7.9 Un algoritmo completo: il valore massimo in un array

Mettiamo ora insieme tutti i pezzi: una funzione, un ciclo, un'istruzione condizionale e una lista.

!!! chiave ""

    Consideriamo il problema di trovare il valore massimo in un array $a$ di $n \ge 1$ numeri interi.

- Questo è lo pseudocodice dell'algoritmo <code>FindMaximum</code> del capitolo «Pseudocodice»: le componenti sono indicizzate da $1$ a $n$.

!!! algoritmo "Algoritmo: FindMaximum"

    <div class="pseudocodice" markdown="0">
    <div class="pc-io"><span class="pc-kw">Input:</span> <span>An array <span class="arithmatex">&#92;(a&#91;1..n&#93;&#92;)</span> of <span class="arithmatex">&#92;(n &#92;ge 1&#92;)</span> integer numbers</span></div>
    <div class="pc-io"><span class="pc-kw">Output:</span> <span>The maximum value in the array <span class="arithmatex">&#92;(a&#92;)</span></span></div>
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

- Questa è l'implementazione in <code>Python</code>. Gli elementi sono indicizzati da $0$ a $n-1$, quindi l'inizializzazione usa <code>a[0]</code> e il ciclo <code>for i in range(1, len(a))</code> visita gli indici $1, \dots, n-1$. La dimensione $n$ non è passata come parametro, perché la funzione la ottiene con <code>len(a)</code>. La variabile si chiama <code>max\_val</code> e non <code>max</code>, per non nascondere la funzione predefinita <code>max()</code>. La funzione suppone $n \ge 1$, come lo pseudocodice: per una lista vuota l'accesso ad <code>a[0]</code> ferma il programma con un <code>IndexError</code>.

    ```python
    def array_max_value(a):
        """Restituisce il valore massimo della lista a (len(a) >= 1)."""
        max_val = a[0]  # Inizializza con il primo elemento

        for i in range(1, len(a)):
            if a[i] > max_val:
                max_val = a[i]  # Aggiorna il massimo

        return max_val

    if __name__ == "__main__":
        a = [9, 12, 3, 16, 19, 11, 12]

        max_val = array_max_value(a)
        print(f"Valore massimo: {max_val}")
    ```

    <strong>Output:</strong>

    ```text
    Valore massimo: 19
    ```

- L'istanza di prova può anche essere generata a caso con il modulo <code>random</code> della libreria di <code>Python</code>: <code>random.randint(1, 100)</code> restituisce un intero casuale fra $1$ e $100$ (entrambi inclusi). L'istruzione <code>random.seed(2026)</code> fissa il punto di partenza del generatore casuale, in modo che ogni esecuzione produca la stessa lista; senza di essa, ogni esecuzione produce una lista diversa.

<a id="box-29-py-exrandom"></a>

!!! esempio "Esempio 7.29: un'istanza casuale"

    ```python
    import random

    def array_max_value(a):
        max_val = a[0]
        for i in range(1, len(a)):
            if a[i] > max_val:
                max_val = a[i]
        return max_val

    if __name__ == "__main__":
        random.seed(2026)  # Stessa lista casuale a ogni esecuzione
        n = 10             # Dimensione della lista
        a = [random.randint(1, 100) for _ in range(n)]

        print(a)
        print(f"Valore massimo: {array_max_value(a)}")
    ```

    <strong>Output:</strong>

    ```text
    [16, 41, 65, 66, 83, 14, 29, 77, 80, 72]
    Valore massimo: 83
    ```

<a id="box-30-py-extrace"></a>

!!! esempio "Esempio 7.30: esecuzione passo per passo"

    In ogni tabella, la colonna $i$ è l'indice del ciclo <code>Python</code> e la colonna $i+1$ è l'indice corrispondente dello pseudocodice. La prima riga è l'inizializzazione <code>max\_val = a[0]</code>.

    <strong>Istanza 1:</strong> $a = [9, 12, 3, 16, 19, 11, 12]$, $n=7$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span> (<code>Python</code>)</th>
    <th><span class="arithmatex">&#92;(i+1&#92;)</span> (pseudocodice)</th>
    <th><code>a[i]</code></th>
    <th><code>a[i] &gt; max\_val</code>?</th>
    <th><code>max\_val</code></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(16&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(16&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(11&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(6&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td><span class="arithmatex">&#92;(12&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(19&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> <code>max\_val</code> $= 19$

    <strong>Istanza 2:</strong> $a = [3, 7, 2, 9, 1]$, $n=5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span> (<code>Python</code>)</th>
    <th><span class="arithmatex">&#92;(i+1&#92;)</span> (pseudocodice)</th>
    <th><code>a[i]</code></th>
    <th><code>a[i] &gt; max\_val</code>?</th>
    <th><code>max\_val</code></th>
    </tr>
    <tr>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td>–</td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(2&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(7&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(3&#92;)</span></td>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    <td>Sì</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    <tr>
    <td><span class="arithmatex">&#92;(4&#92;)</span></td>
    <td><span class="arithmatex">&#92;(5&#92;)</span></td>
    <td><span class="arithmatex">&#92;(1&#92;)</span></td>
    <td>No</td>
    <td><span class="arithmatex">&#92;(9&#92;)</span></td>
    </tr>
    </table></div>

    <strong>Restituisce:</strong> <code>max\_val</code> $= 9$

## 7.10 Operatori bit a bit

Gli operatori bit a bit del capitolo «Introduzione a <code>C++</code>» esistono in <code>Python</code> con gli stessi simboli e lo stesso significato: <code>&amp;</code> (AND), <code>|</code> (OR), <code></code> (XOR), <code>~</code> (NOT), <code>&lt; &lt;</code> (scorrimento a sinistra) e <code>&gt; &gt;</code> (scorrimento a destra). La funzione <code>bin()</code> restituisce la rappresentazione binaria di un intero, preceduta dal prefisso <code>0b</code>.

- Poiché gli interi di <code>Python</code> non hanno un numero fisso di bit, il NOT bit a bit non dipende da un tipo di dato: <code>~x</code> è sempre uguale a $-x-1$. Per ottenere il risultato a $8$ bit di <code>C++</code>, il risultato è combinato con la maschera <code>0xFF</code> (il numero $255$, la cui rappresentazione binaria è $11111111$).

<a id="box-31-py-exbitwise"></a>

!!! esempio "Esempio 7.31: operatori bit a bit"

    ```python
    a = 12  # Binario: 1100
    b = 10  # Binario: 1010

    print(a & b, a | b, a ^ b)          # AND, OR, XOR
    print(bin(a), bin(b), bin(a & b))   # Rappresentazioni binarie
    print(5 << 2, 20 >> 2, 20 >> 3)     # Scorrimenti
    print(~a, ~a & 0xFF)                # NOT, e la sua versione a 8 bit

    n = 15
    print("dispari" if n & 1 else "pari")   # Bit meno significativo
    ```

    <strong>Output:</strong>

    ```text
    8 14 6
    0b1100 0b1010 0b1000
    20 5 2
    -13 243
    dispari
    ```

    Tutti i valori coincidono con quelli degli esempi corrispondenti del capitolo «Introduzione a <code>C++</code>».

## 7.11 <code>Python</code> e <code>C++</code> a confronto

La tabella seguente riassume le principali differenze fra i due linguaggi incontrate in questo capitolo.

<div class="tabella" markdown="0"><table>
<tr>
<th></th>
<th><code>C++</code></th>
<th><code>Python</code></th>
</tr>
<tr>
<td>Esecuzione</td>
<td>compilato (<code>g++</code>), poi eseguito</td>
<td>interpretato (<code>python3</code>)</td>
</tr>
<tr>
<td>Tipi di dato</td>
<td>dichiarati: <code>int x = 5;</code></td>
<td>non dichiarati: <code>x = 5</code></td>
</tr>
<tr>
<td>Fine dell'istruzione</td>
<td><code>;</code></td>
<td>fine della riga</td>
</tr>
<tr>
<td>Blocchi</td>
<td>parentesi graffe <code>{}</code></td>
<td><code>:</code> e indentazione</td>
</tr>
<tr>
<td>Commenti</td>
<td><code>//</code> e <code>/\* \*/</code></td>
<td><code>#</code> (e <code>""" """</code>)</td>
</tr>
<tr>
<td>Valori booleani</td>
<td><code>true</code>, <code>false</code> (stampati <code>1</code>, <code>0</code>)</td>
<td><code>True</code>, <code>False</code></td>
</tr>
<tr>
<td><code>10 / 3</code></td>
<td><code>3</code> (divisione intera)</td>
<td><code>3.3333333333333335</code></td>
</tr>
<tr>
<td>Divisione intera</td>
<td><code>/</code> fra due <code>int</code></td>
<td><code>//</code></td>
</tr>
<tr>
<td>Potenza</td>
<td>funzione <code>pow</code></td>
<td>operatore <code>\*\*</code></td>
</tr>
<tr>
<td>Incremento</td>
<td><code>x++</code>, <code>++x</code></td>
<td><code>x += 1</code></td>
</tr>
<tr>
<td>Operatori logici</td>
<td><code>&amp;&amp;</code>, <code>||</code>, <code>!</code></td>
<td><code>and</code>, <code>or</code>, <code>not</code></td>
</tr>
<tr>
<td>Operatore ternario</td>
<td><code>c ? x : y</code></td>
<td><code>x if c else y</code></td>
</tr>
<tr>
<td>Ciclo <code>for</code></td>
<td><code>for (int i = 0; i &lt; n; i++)</code></td>
<td><code>for i in range(n):</code></td>
</tr>
<tr>
<td>Collezioni</td>
<td>array, di dimensione fissa o dinamica</td>
<td>liste, dinamiche</td>
</tr>
<tr>
<td>Dimensione di una collezione</td>
<td>memorizzata in una variabile separata</td>
<td><code>len(a)</code></td>
</tr>
<tr>
<td>Più risultati</td>
<td>parametri per riferimento</td>
<td>restituzione di una tupla</td>
</tr>
<tr>
<td>Punto di ingresso</td>
<td>funzione <code>main</code></td>
<td>livello più esterno del file</td>
</tr>
</table></div>

!!! chiave ""

    <strong>Punti chiave del capitolo</strong>

    - Un programma <code>Python</code> è eseguito dall'interprete (<code>python3</code>) dalla prima riga all'ultima; le istruzioni non terminano con “<code>;</code>” e i blocchi sono delimitati da “<code>:</code>” e dall'indentazione.

    - Le variabili sono create tramite assegnamento, senza dichiarare il loro tipo di dato; gli interi non hanno un valore massimo.

    - L'operatore <code>/</code> dà sempre un <code>float</code>; la divisione intera è <code>//</code> e arrotonda per difetto, anche per i numeri negativi.

    - Le istruzioni condizionali (<code>if</code>, <code>elif</code>, <code>else</code>, e l'espressione condizionale) scelgono quali istruzioni vengono eseguite; i cicli (<code>while</code>, e <code>for</code> su un <code>range</code> o su una lista) le ripetono.

    - Le liste di <code>Python</code> sono indicizzate da $0$ a $n-1$, con $n$ = <code>len(a)</code>, mentre gli array dello pseudocodice sono indicizzati da $1$ a $n$; le liste crescono con <code>append</code> e non richiedono gestione della memoria.

    - Una funzione modifica la lista di chi chiama quando ne cambia gli elementi, ma non un numero che riceve; più risultati sono restituiti insieme come una tupla.

---

**Esercizi su questo capitolo:** [:material-pencil: Introduzione a Python](../esercizi/es-07-introduzione-python.md)
