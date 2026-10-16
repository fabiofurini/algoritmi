---
title: "Introduzione a Java"
---

# Introduzione a Java

<div class="info-capitolo" markdown>

**Parte 2 · Linguaggi di programmazione · Capitolo 8** · [:material-file-pdf-box: Dispensa, volume 2 (PDF)](../pdf/dispensa-2-linguaggi-di-programmazione.pdf) · [:material-presentation: Slide](../pdf/slide-08-introduzione-java.pdf) · [:material-pencil: Esercizi: Introduzione a Java](../esercizi/es-08-introduzione-java.md)

</div>

## Introduzione

Nei capitoli «Introduzione a <code>C++</code>» e «Introduzione a <code>Python</code>» abbiamo tradotto lo pseudocodice dei nostri algoritmi in un linguaggio di programmazione compilato e in uno interpretato. In questo capitolo introduciamo un terzo linguaggio di programmazione, <code>Java</code>, che sta a metà strada: i suoi programmi sono compilati in un codice intermedio, che viene poi eseguito da una macchina virtuale. La sua sintassi è molto vicina a quella di <code>C++</code>, ma ogni programma è organizzato in <strong>classi</strong>.

Il capitolo segue lo stesso percorso dei due capitoli precedenti, in modo che i tre linguaggi possano essere confrontati sezione per sezione:

- le caratteristiche principali del linguaggio e la struttura di un programma;

- variabili, tipi di dato, ingresso e uscita;

- operatori, istruzioni condizionali e cicli;

- gli array, e le liste dinamiche della classe <code>ArrayList</code>;

- i metodi (il nome che <code>Java</code> dà alle funzioni), i loro parametri e i loro valori di ritorno;

- un algoritmo completo, la ricerca del valore massimo in un array, scritto in pseudocodice e in <code>Java</code>;

- gli operatori bit a bit e una tabella riassuntiva che confronta <code>Java</code> con <code>C++</code> e <code>Python</code>.

Ogni frammento di codice del capitolo è stato compilato con il compilatore <code>javac</code> ed eseguito con la macchina virtuale <code>java</code> (<code>OpenJDK 25</code>): gli output riportati negli esempi sono quelli stampati dai programmi.

!!! chiave ""

    Nello pseudocodice le componenti di un array $a[1..n]$ sono indicizzate da $1$ a $n$; in <code>Java</code>, come in <code>C++</code> e in <code>Python</code>, gli elementi di un array di dimensione $n$ sono indicizzati da $0$ a $n-1$. La componente $a[i]$ dello pseudocodice corrisponde all'elemento <code>a[i-1]</code> del codice <code>Java</code>.

## 8.1 Caratteristiche principali del linguaggio di programmazione

Le caratteristiche principali di <code>Java</code> sono le seguenti.

- <code>Java</code> è un linguaggio <strong>compilato e interpretato</strong>: il codice sorgente (file <code>.java</code>) viene prima compilato in <strong>bytecode</strong> (file <code>.class</code>) dal compilatore <code>Java</code> <code>javac</code>, e poi il bytecode viene eseguito dalla <strong>Java Virtual Machine</strong> (JVM). Questo rende i programmi <code>Java</code> <strong>indipendenti dalla piattaforma</strong>: lo stesso bytecode funziona su qualunque macchina su cui sia installata una JVM («scrivi una volta, esegui ovunque»).

- <code>Java</code> è un linguaggio <strong>fortemente e staticamente tipizzato</strong>: ogni variabile deve essere dichiarata con il suo tipo di dato prima dell'uso, e il suo tipo di dato non può cambiare durante l'esecuzione.

- <code>Java</code> è <strong>orientato agli oggetti</strong>: ogni programma è organizzato in <strong>classi</strong>. Il punto di ingresso di ogni programma <code>Java</code> è il metodo <code>main</code> di una classe.

- <code>Java</code> supporta i <strong>metodi</strong> (il termine <code>Java</code> per le funzioni), che permettono un approccio modulare e riutilizzabile alla programmazione.

- Come in <code>C++</code>, la struttura a blocchi del codice è definita dalle <strong>parentesi graffe</strong> <code>{}</code>, e ogni istruzione deve terminare con il simbolo riservato “<code>;</code>”.

- Come in <code>C++</code>, un commento su una sola riga inizia con il simbolo riservato “<code>//</code>”, e i commenti su più righe sono racchiusi fra i simboli riservati “<code>/\*</code>” e “<code>\*/</code>”.

<a id="box-1-java-excomments"></a>

!!! esempio "Esempio 8.1: commenti in <code>Java</code>"

    Questo è un esempio di commento su una sola riga:

    ```java
    // Questa è una riga di commento
    ```

    Questo è un esempio di commento su più righe:

    ```java
    /* Questo è un
       commento su più righe */
    ```

### 8.1.1 La struttura di un programma

Prima di descrivere le singole istruzioni, osserviamo lo scheletro che ogni programma ha in comune. Un programma <code>Java</code> è costituito da una o più classi; l'esecuzione parte dal metodo <code>public static void main(String[] args)</code> della classe che viene lanciata.

<a id="box-2-java-exskeleton"></a>

!!! esempio "Esempio 8.2: lo scheletro di un programma"

    ```java
    public class HelloWorld {

        public static void main(String[] args) {
            // Qui si scrivono le istruzioni del programma
            System.out.println("Ciao, mondo!");
        }
    }
    ```

    Una classe dichiarata <code>public</code> deve essere salvata in un file con lo stesso nome della classe: qui <code>HelloWorld.java</code>. Il programma si compila e si esegue con i comandi

    ```text
    javac HelloWorld.java
    java HelloWorld
    ```

    Il primo comando produce il file di bytecode <code>HelloWorld.class</code>; il secondo lo esegue (si noti che l'estensione non si scrive). L'output è

    ```text
    Ciao, mondo!
    ```

Negli esempi seguenti scriviamo solo le istruzioni che contano: a meno che non contengano un programma completo, i frammenti di codice vanno inseriti fra le parentesi graffe di <code>main</code>.

!!! chiave ""

    Ogni istruzione <code>Java</code> appartiene a un metodo, e ogni metodo appartiene a una classe. Ogni istruzione termina con “<code>;</code>”.

## 8.2 Variabili e tipi di dato

Il codice sorgente opera su <strong>variabili</strong>, e ogni variabile ha un <strong>tipo di dato</strong>.

- I quattro tipi di dato fondamentali di <code>Java</code> sono:

    1. Il tipo di dato “<code>int</code>” rappresenta un intero memorizzato con $32$ bit: un numero intero da $-2^{31} = -2147483648$ a $2^{31}-1 = 2147483647$. Per interi più grandi si usa il tipo di dato <code>long</code> ($64$ bit).

    2. Il tipo di dato “<code>boolean</code>” rappresenta un valore booleano: <code>true</code> o <code>false</code> (minuscolo).

    3. Il tipo di dato “<code>double</code>” rappresenta un numero in virgola mobile a precisione doppia ($64$ bit), come in <code>C++</code>. Il tipo di dato <code>float</code> ha precisione singola, e i suoi valori si scrivono con il suffisso <code>f</code> (ad esempio <code>3.14f</code>).

    4. Il tipo di dato “<code>char</code>” rappresenta un singolo carattere, racchiuso fra apici singoli (ad esempio <code>'A'</code>, <code>'7'</code>).

- Il tipo di dato “<code>String</code>” (con la <code>S</code> maiuscola) rappresenta una sequenza di caratteri racchiusa fra virgolette doppie, ed è il modo standard di trattare il testo in <code>Java</code>.

- Una variabile funziona come un contenitore che memorizza un valore di un tipo di dato specifico per un uso successivo.

- Alle variabili si assegnano valori con l'operatore di assegnamento “<code>=</code>”. Quando si assegna un nuovo valore, il valore precedente viene sovrascritto.

- Il compilatore controlla i tipi di dato: assegnare un valore di tipo sbagliato (per esempio la stringa <code>"cinque"</code> a una variabile di tipo <code>int</code>) o usare una variabile che non ha ricevuto un valore è un <strong>errore di compilazione</strong>, e il programma non viene prodotto.

!!! chiave ""

    Le variabili devono essere dichiarate con il loro tipo di dato prima dell'uso, come in <code>C++</code>.

<a id="box-3-java-exvariables"></a>

!!! esempio "Esempio 8.3: dichiarazioni e assegnamenti di variabili"

    ```java
    int age = 25;              // Variabile intera
    boolean isRaining = false; // Variabile booleana
    double pi = 3.14159;       // Virgola mobile a precisione doppia
    float small = 3.14f;       // Virgola mobile a precisione singola
    double large = 123456.789; // Virgola mobile a precisione doppia
    char letter = 'A';         // Variabile carattere
    String name = "Alice";     // Variabile stringa

    age = 26; // Il valore precedente 25 viene sovrascritto
    System.out.println(age + " " + isRaining + " " + pi + " " + small);
    System.out.println(large + " " + letter + " " + name);
    ```

    <strong>Output:</strong>

    ```text
    26 false 3.14159 3.14
    123456.789 A Alice
    ```

    A differenza di <code>C++</code>, il valore booleano è visualizzato come <code>false</code> e il numero <code>123456.789</code> è visualizzato con tutte le sue cifre.

<a id="box-4-java-exoverflow"></a>

!!! esempio "Esempio 8.4: i limiti del tipo di dato <code>int</code>"

    ```java
    int big = Integer.MAX_VALUE;  // Il più grande int
    System.out.println(big);
    System.out.println(big + 1);  // Overflow: il risultato non entra in 32 bit

    long bigger = (long) big + 1; // Calcolato con 64 bit
    System.out.println(bigger);
    ```

    <strong>Output:</strong>

    ```text
    2147483647
    -2147483648
    2147483648
    ```

    Quando il risultato di un'operazione fra valori <code>int</code> non entra in $32$ bit, «riparte» dall'altro estremo dell'intervallo, senza alcun messaggio di errore. Gli interi di <code>Python</code> non vanno mai in overflow.

## 8.3 Ingresso e uscita

- L'oggetto <code>System.out</code> (l'uscita standard, fornita dalla classe <code>System</code>) ha i metodi che visualizzano valori sullo schermo. I più comuni sono:

    - <code>System.out.println()</code>: stampa un valore seguito da un a capo;

    - <code>System.out.print()</code>: stampa un valore senza l'a capo.

- Valori e stringhe sono <strong>concatenati</strong> con l'operatore <code>+</code> dentro un'istruzione di stampa: quando uno dei due operandi di <code>+</code> è una <code>String</code>, l'altro viene convertito in testo. L'espressione è valutata da sinistra a destra, quindi un'operazione aritmetica dentro una concatenazione deve essere racchiusa fra parentesi.

- Il metodo <code>System.out.printf()</code> stampa un testo formattato: nella prima stringa, <code>%d</code> è sostituito da un intero, <code>%s</code> da una stringa, <code>%.kf</code> da un numero in virgola mobile con esattamente $k$ cifre dopo la virgola decimale, e <code>%n</code> da un a capo.

<a id="box-5-java-exprint"></a>

!!! esempio "Esempio 8.5: stampe sullo schermo"

    ```java
    int n = 42;
    System.out.println("Il valore della variabile è " + n);
    System.out.println("n = " + n + ", doppio = " + (n * 2));

    System.out.println("n + 1 = " + n + 1);   // Concatenazione: "42" poi "1"
    System.out.println("n + 1 = " + (n + 1)); // Addizione, poi concatenazione

    System.out.print("Niente a capo ");
    System.out.println("dopo print");
    System.out.printf("%d diviso %d è %.2f%n", 10, 3, 10.0 / 3);
    ```

    <strong>Output:</strong>

    ```text
    Il valore della variabile è 42
    n = 42, doppio = 84
    n + 1 = 421
    n + 1 = 43
    Niente a capo dopo print
    10 diviso 3 è 3.33
    ```

- Il separatore decimale stampato da <code>printf</code> dipende dalle impostazioni della lingua del calcolatore: su un calcolatore impostato in italiano l'ultima riga è <code>10 diviso 3 è 3,33</code>, con la virgola. Il metodo <code>println</code> usa sempre il punto.

- Per leggere l'ingresso da tastiera si usa la classe <code>Scanner</code> del pacchetto <code>java.util</code>. Va importata con l'istruzione <code>import java.util.Scanner;</code>, scritta all'inizio del file, prima della classe. I metodi <code>nextLine()</code>, <code>nextInt()</code> e <code>nextDouble()</code> leggono una riga di testo, un intero e un numero in virgola mobile.

<a id="box-6-java-exinput"></a>

!!! esempio "Esempio 8.6: ingresso da tastiera con <code>Scanner</code>"

    ```java
    import java.util.Scanner;

    public class InputExample {

        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);

            System.out.print("Inserisci il tuo nome: ");
            String name = sc.nextLine();     // Legge una String

            System.out.print("Inserisci un intero: ");
            int n = sc.nextInt();            // Legge un int

            System.out.print("Inserisci un numero reale: ");
            double x = sc.nextDouble();      // Legge un double

            System.out.println("Ciao " + name + ", n = " + n + ", x = " + x);
            sc.close();
        }
    }
    ```

    <strong>Esempio di esecuzione</strong> (l'utente scrive <code>Ada</code>, <code>7</code> e <code>2.5</code>):

    ```text
    Inserisci il tuo nome: Ada
    Inserisci un intero: 7
    Inserisci un numero reale: 2.5
    Ciao Ada, n = 7, x = 2.5
    ```

    Come <code>printf</code>, il metodo <code>nextDouble()</code> segue le impostazioni della lingua: su un calcolatore impostato in italiano il numero reale va scritto come <code>2,5</code>.

## 8.4 Operatori

Gli operatori sono simboli che eseguono operazioni su variabili e valori. Gli operatori di <code>Java</code> sono gli stessi di <code>C++</code>: operatori aritmetici, di assegnamento, di incremento e decremento, relazionali e logici.

### 8.4.1 Operatori aritmetici

!!! chiave ""

    <strong>Operatori aritmetici</strong>, usati per eseguire le operazioni matematiche di base:

    - <code>+</code> (Addizione) $\rightsquigarrow$ Somma due valori.

    - <code>-</code> (Sottrazione) $\rightsquigarrow$ Sottrae un valore da un altro.

    - <code>\*</code> (Moltiplicazione) $\rightsquigarrow$ Moltiplica due valori.

    - <code>/</code> (Divisione) $\rightsquigarrow$ Divide un valore per un altro. Divisione intera quando entrambi gli operandi sono interi.

    - <code>%</code> (Resto) $\rightsquigarrow$ Restituisce il resto di una divisione.

<a id="box-7-java-exarith"></a>

!!! esempio "Esempio 8.7: operatori aritmetici"

    ```java
    int a = 10, b = 3;

    System.out.println("Addizione:       " + (a + b));
    System.out.println("Sottrazione:     " + (a - b));
    System.out.println("Moltiplicazione: " + (a * b));
    System.out.println("Divisione:       " + (a / b));  // Divisione intera
    System.out.println("Resto:           " + (a % b));  // Resto della divisione
    System.out.println("Divisione reale: " + ((double) a / b));
    ```

    <strong>Output:</strong>

    ```text
    Addizione:       13
    Sottrazione:     7
    Moltiplicazione: 30
    Divisione:       3
    Resto:           1
    Divisione reale: 3.3333333333333335
    ```

- Come in <code>C++</code>, l'operatore di divisione <code>/</code> esegue la <strong>divisione intera</strong> quando entrambi gli operandi sono interi, e il quoziente è troncato verso lo zero: <code>10 / 3</code> vale <code>3</code> e <code>-7 / 2</code> vale <code>-3</code> (con resto <code>-7 % 2</code> uguale a <code>-1</code>). Per ottenere un risultato in virgola mobile almeno un operando deve essere di tipo <code>double</code>, per esempio con la <strong>conversione di tipo</strong> (<strong>cast</strong>) <code>(double) a / b</code>.

- La conversione <code>(int)</code> elimina la parte decimale di un <code>double</code>: <code>(int) 3.9</code> vale <code>3</code>. Non esiste un operatore per la potenza: il metodo <code>Math.pow(x, y)</code> restituisce $x^y$ come <code>double</code>.

<a id="box-8-java-exdivision"></a>

!!! esempio "Esempio 8.8: divisione intera e in virgola mobile"

    ```java
    int a = 10, b = 3;

    System.out.println(a / b);             // Divisione intera
    System.out.println(10.0 / 3);          // Divisione in virgola mobile
    System.out.println((double) a / b);    // Conversione di a in double
    System.out.printf("%.2f%n", (double) a / b); // Due cifre decimali
    System.out.println(-7 / 2 + " " + -7 % 2);   // Troncamento verso zero
    System.out.println((int) 3.9 + " " + Math.pow(2, 10));
    ```

    <strong>Output:</strong>

    ```text
    3
    3.3333333333333335
    3.3333333333333335
    3.33
    -3 -1
    3 1024.0
    ```

### 8.4.2 Operatori di assegnamento

!!! chiave ""

    <strong>Operatori di assegnamento</strong>, usati per assegnare valori alle variabili:

    - <code>=</code>  (Assegnamento) $\rightsquigarrow$ Assegna un valore a una variabile.

    - <code>+=</code> (Assegnamento con addizione) $\rightsquigarrow$ Somma un valore e assegna il risultato.

    - <code>-=</code> (Assegnamento con sottrazione) $\rightsquigarrow$ Sottrae un valore e assegna il risultato.

    - <code>\*=</code> (Assegnamento con moltiplicazione) $\rightsquigarrow$ Moltiplica e assegna il risultato.

    - <code>/=</code> (Assegnamento con divisione) $\rightsquigarrow$ Divide e assegna il risultato.

    - <code>%=</code> (Assegnamento con resto) $\rightsquigarrow$ Calcola il resto e assegna il risultato.

<a id="box-9-java-exassign"></a>

!!! esempio "Esempio 8.9: operatori di assegnamento"

    ```java
    int x = 10;  // Assegnamento
    System.out.println("Valore iniziale: " + x);

    x += 5;  System.out.println("Dopo += 5: " + x); // x = x + 5
    x -= 3;  System.out.println("Dopo -= 3: " + x); // x = x - 3
    x *= 2;  System.out.println("Dopo *= 2: " + x); // x = x * 2
    x /= 4;  System.out.println("Dopo /= 4: " + x); // x = x / 4
    x %= 4;  System.out.println("Dopo %= 4: " + x); // x = x % 4
    ```

    <strong>Output:</strong>

    ```text
    Valore iniziale: 10
    Dopo += 5: 15
    Dopo -= 3: 12
    Dopo *= 2: 24
    Dopo /= 4: 6
    Dopo %= 4: 2
    ```

    Due istruzioni possono essere scritte sulla stessa riga, perché ciascuna termina con “<code>;</code>”.

### 8.4.3 Operatori di incremento e decremento

!!! chiave ""

    <strong>Operatori di incremento e decremento</strong>:

    - <code>++</code> (Incremento) $\rightsquigarrow$ Aumenta di 1 il valore di una variabile.

    - <code>- -</code> (Decremento) $\rightsquigarrow$ Diminuisce di 1 il valore di una variabile.

- Come in <code>C++</code>, il pre-incremento (<code>++x</code>) incrementa il valore prima di restituirlo, e il post-incremento (<code>x++</code>) restituisce prima il valore, poi lo incrementa. La stessa logica vale per l'operatore di decremento (<code>- -x</code> e <code>x- -</code>).

<a id="box-10-java-exincdec"></a>

!!! esempio "Esempio 8.10: operatori di incremento e decremento"

    ```java
    int x = 5;
    System.out.println("Valore iniziale: " + x);
    System.out.println("Pre-incremento (++x): " + ++x);
    System.out.println("Post-incremento (x++): " + x++);
    System.out.println("Valore dopo il post-incremento: " + x);
    System.out.println("Pre-decremento (--x): " + --x);
    System.out.println("Post-decremento (x--): " + x--);
    System.out.println("Valore dopo il post-decremento: " + x);
    ```

    <strong>Output:</strong>

    ```text
    Valore iniziale: 5
    Pre-incremento (++x): 6
    Post-incremento (x++): 6
    Valore dopo il post-incremento: 7
    Pre-decremento (--x): 6
    Post-decremento (x--): 6
    Valore dopo il post-decremento: 5
    ```

### 8.4.4 Operatori relazionali

!!! chiave ""

    <strong>Operatori relazionali</strong>, usati per confrontare valori e restituire un risultato <code>boolean</code>:

    - <code>==</code> (Uguale a) $\rightsquigarrow$ Verifica se due valori sono uguali.

    - <code>!=</code> (Diverso da) $\rightsquigarrow$ Verifica se due valori sono diversi.

    - <code>&lt;</code>  (Minore di) $\rightsquigarrow$ Verifica se un valore è minore di un altro.

    - <code>&gt;</code>  (Maggiore di) $\rightsquigarrow$ Verifica se un valore è maggiore di un altro.

    - <code>&lt;=</code> (Minore o uguale a) $\rightsquigarrow$ Verifica se un valore è minore o uguale a un altro.

    - <code>&gt;=</code> (Maggiore o uguale a) $\rightsquigarrow$ Verifica se un valore è maggiore o uguale a un altro.

- Gli operatori relazionali restituiscono un valore di tipo <code>boolean</code>, visualizzato come <code>true</code> o <code>false</code> (non come <code>1</code> e <code>0</code> come in <code>C++</code>). Questi operatori sono usati comunemente nelle <strong>istruzioni condizionali</strong> e nei <strong>cicli</strong>.

- L'operatore <code>==</code> confronta i valori dei tipi di dato primitivi (<code>int</code>, <code>double</code>, <code>char</code>, <code>boolean</code>); due valori <code>String</code> si confrontano con il metodo <code>equals</code>, per esempio <code>name.equals("Alice")</code>.

<a id="box-11-java-exrel"></a>

!!! esempio "Esempio 8.11: operatori relazionali"

    ```java
    int a = 10, b = 5;

    System.out.println("a == b: " + (a == b)); // Uguale a
    System.out.println("a != b: " + (a != b)); // Diverso da
    System.out.println("a < b: " + (a < b));   // Minore di
    System.out.println("a > b: " + (a > b));   // Maggiore di
    System.out.println("a <= b: " + (a <= b)); // Minore o uguale a
    System.out.println("a >= b: " + (a >= b)); // Maggiore o uguale a
    ```

    <strong>Output:</strong>

    ```text
    a == b: false
    a != b: true
    a < b: false
    a > b: true
    a <= b: false
    a >= b: true
    ```

### 8.4.5 Operatori logici

!!! chiave ""

    <strong>Operatori logici</strong>, usati per le operazioni logiche, spesso nelle istruzioni condizionali:

    - <code>&amp;&amp;</code> (AND logico) $\rightsquigarrow$ Restituisce <code>true</code> se entrambe le condizioni sono <code>true</code>.

    - <code>||</code> (OR logico) $\rightsquigarrow$ Restituisce <code>true</code> se almeno una condizione è <code>true</code>.

    - <code>!</code> (NOT logico) $\rightsquigarrow$ Inverte il valore booleano.

<a id="box-12-java-exlogic"></a>

!!! esempio "Esempio 8.12: operatori logici"

    ```java
    boolean c1 = true, c2 = false;

    System.out.println("c1: " + c1);
    System.out.println("c2: " + c2);
    System.out.println("c1 && c2: " + (c1 && c2)); // true solo se entrambe sono true
    System.out.println("c1 || c2: " + (c1 || c2)); // true se almeno una è true
    System.out.println("!c1: " + (!c1));           // Inverte il valore
    System.out.println("!c2: " + (!c2));
    ```

    <strong>Output:</strong>

    ```text
    c1: true
    c2: false
    c1 && c2: false
    c1 || c2: true
    !c1: false
    !c2: true
    ```

## 8.5 Istruzioni condizionali

Gli operatori relazionali e logici producono le condizioni che decidono quali istruzioni vengono eseguite.

- L'istruzione <code>if</code> valuta una condizione racchiusa fra parentesi <code>()</code>. Se la condizione è <code>true</code>, viene eseguito il blocco racchiuso fra parentesi graffe <code>{}</code>. La clausola opzionale <code>else if</code> verifica condizioni aggiuntive, e la clausola opzionale <code>else</code> tratta tutti i casi rimanenti.

- A differenza di <code>C++</code>, la condizione deve essere di tipo <code>boolean</code>: un intero non è accettato come condizione, quindi <code>if (n % 2)</code> è un errore di compilazione e il test va scritto <code>if (n % 2 != 0)</code>.

<a id="box-13-java-exif"></a>

!!! esempio "Esempio 8.13: istruzione condizionale"

    ```java
    int number = 10;

    // Verifica se il numero è positivo
    if (number > 0) {
        System.out.println("Il numero è positivo.");
    } else {
        System.out.println("Il numero non è positivo.");
    }
    ```

    <strong>Output:</strong>

    ```text
    Il numero è positivo.
    ```

<a id="box-14-java-exelseif"></a>

!!! esempio "Esempio 8.14: <code>if</code> / <code>else if</code> / <code>else</code>"

    ```java
    int score = 85;
    String grade;

    if      (score >= 90) { grade = "A"; }
    else if (score >= 80) { grade = "B"; }
    else if (score >= 70) { grade = "C"; }
    else if (score >= 60) { grade = "D"; }
    else                  { grade = "F"; }

    System.out.println("Punteggio: " + score + ", Voto: " + grade);
    ```

    <strong>Output:</strong>

    ```text
    Punteggio: 85, Voto: B
    ```

    Le condizioni sono valutate dall'alto verso il basso, e viene eseguito solo il blocco della prima condizione vera. La variabile <code>grade</code> è dichiarata senza un valore: il compilatore la accetta perché ogni ramo le assegna un valore prima che venga stampata.

### 8.5.1 Operatore ternario (operatore condizionale)

- L'<strong>operatore ternario</strong> <code>?:</code> è lo stesso di <code>C++</code>. Sintassi: <code>condizione ? valore\_se\_vero : valore\_se\_falso</code>.

<a id="box-15-java-extern"></a>

!!! esempio "Esempio 8.15: operatore ternario"

    ```java
    int number = 10;

    // condizione ? valore_se_vero : valore_se_falso
    String result = (number > 0) ? "positivo" : "non positivo";
    System.out.println("Il numero è " + result);

    // Ricerca del massimo fra due numeri
    int a = 15, b = 20;
    int maximum = (a > b) ? a : b;
    System.out.println("Massimo: " + maximum);

    // Verifica se pari o dispari
    int n = 7;
    String parity = (n % 2 == 0) ? "pari" : "dispari";
    System.out.println(n + " è " + parity);

    // Valore assoluto
    int x = -5;
    int absValue = (x >= 0) ? x : -x;
    System.out.println("Il valore assoluto di " + x + " è " + absValue);
    ```

    <strong>Output:</strong>

    ```text
    Il numero è positivo
    Massimo: 20
    7 è dispari
    Il valore assoluto di -5 è 5
    ```

    La classe <code>Math</code> fornisce anche i metodi <code>Math.max(a, b)</code> e <code>Math.abs(x)</code>, che restituiscono gli stessi valori.

## 8.6 Cicli

Le istruzioni condizionali scelgono <em>se</em> un blocco di codice viene eseguito; i cicli decidono <em>quante volte</em> viene eseguito.

- I cicli servono a eseguire ripetutamente un blocco di codice finché una condizione è soddisfatta. Come in <code>C++</code>, i cicli più usati di <code>Java</code> sono il ciclo <code>while</code> e il ciclo <code>for</code>.

### 8.6.1 Il ciclo <code>while</code>

- Il ciclo <code>while</code> esegue un blocco di codice finché la condizione racchiusa fra parentesi <code>()</code> vale <code>true</code>. Quando la condizione è <code>false</code>, il ciclo termina.

<a id="box-16-java-exwhile"></a>

!!! esempio "Esempio 8.16: ciclo <code>while</code>"

    ```java
    int i = 1; // Inizializzazione

    while (i <= 5) { // Condizione
        System.out.println("Numero: " + i);
        i++; // Incremento
    }
    ```

    <strong>Output:</strong>

    ```text
    Numero: 1
    Numero: 2
    Numero: 3
    Numero: 4
    Numero: 5
    ```

### 8.6.2 Il ciclo <code>for</code>

- Il ciclo <code>for</code> combina inizializzazione, condizione e incremento (o decremento) in una sola istruzione, esattamente come in <code>C++</code>.

<a id="box-17-java-exfor"></a>

!!! esempio "Esempio 8.17: ciclo <code>for</code>"

    ```java
    // Inizializzazione; Condizione; Incremento
    for (int i = 1; i <= 5; i++) {
        System.out.println("Numero: " + i);
    }
    ```

    L'output è lo stesso del ciclo <code>while</code> dell'[Esempio 8.16](#box-16-java-exwhile).

### 8.6.3 Le istruzioni <code>break</code> e <code>continue</code>

- L'istruzione <code>break</code> termina immediatamente il ciclo.

- L'istruzione <code>continue</code> salta il resto dell'iterazione corrente e passa alla successiva.

<a id="box-18-java-exbreak"></a>

!!! esempio "Esempio 8.18: <code>break</code> e <code>continue</code>"

    ```java
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue; // Salta i numeri pari
        }
        if (i > 7) {
            break; // Interrompe il ciclo al primo dispari maggiore di 7
        }
        System.out.print(i + " ");
    }
    System.out.println();
    ```

    <strong>Output:</strong>

    ```text
    1 3 5 7
    ```

    L'output è lo stesso delle versioni <code>C++</code> e <code>Python</code>: il valore <code>9</code> fa scattare il <code>break</code>.

## 8.7 Array

I cicli diventano davvero utili quando visitano collezioni di valori. Una collezione di variabili dello stesso tipo di dato è memorizzata in un <strong>array</strong>.

- Un <strong>array</strong> in <code>Java</code> è una collezione ordinata di elementi dello stesso tipo di dato, con una dimensione fissata al momento della creazione: la dimensione non può cambiare in seguito.

- Il tipo di dato di un array di interi si scrive <code>int[]</code>. Un array si alloca con l'operatore <code>new</code>, per esempio <code>new int[n]</code>, dove la dimensione <code>n</code> può essere decisa durante l'esecuzione, come per gli array di dimensione dinamica di <code>C++</code>. Gli elementi di un nuovo array sono inizializzati a <code>0</code> (a <code>false</code> per <code>boolean</code>).

- Gli elementi si raggiungono tramite il loro <strong>indice</strong> fra parentesi quadre <code>[]</code>, a partire da <code>0</code>: gli elementi di un array di dimensione $n$ sono <code>a[0]</code>, <code>a[1]</code>, …, <code>a[n-1]</code>. Ogni array conosce la propria dimensione: la lunghezza di un array <code>a</code> è <code>a.length</code>.

- A differenza di <code>C++</code>, la memoria di un array non deve essere liberata con <code>delete[]</code>: viene rilasciata automaticamente dal <strong>garbage collector</strong> della JVM quando l'array non è più usato.

!!! chiave ""

    Gli array si allocano con <code>new</code> prima dell'uso (oppure si creano con un elenco di valori fra parentesi graffe). Gli indici partono da <code>0</code>, la dimensione è fissa ed è data da <code>a.length</code>.

<a id="box-19-java-exarray"></a>

!!! esempio "Esempio 8.19: creazione e accesso a un array"

    ```java
    int n = 5;

    int[] a = new int[n]; // Allocazione di un array di n interi

    for (int i = 0; i < n; i++) {
        a[i] = i * 2; // Esempio di assegnamento di valori
    }

    System.out.println("Lunghezza: " + a.length);
    System.out.println("a[0] = " + a[0]); // Primo elemento
    System.out.println("a[4] = " + a[4]); // Ultimo elemento, indice n-1
    ```

    <strong>Output:</strong>

    ```text
    Lunghezza: 5
    a[0] = 0
    a[4] = 8
    ```

    Accedere a un indice che non esiste, per esempio <code>a[5]</code>, ferma il programma con l'errore <code>ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5</code> (in <code>C++</code> lo stesso accesso non è controllato).

- Un array i cui valori sono noti quando si scrive il programma può essere creato elencando i suoi valori fra parentesi graffe, come in <code>C++</code>.

- Il <strong>ciclo <code>for</code> esteso</strong> <code>for (int x : a)</code> visita direttamente gli elementi dell'array <code>a</code>, senza usare i loro indici, come il ciclo <code>for</code> su una lista di <code>Python</code>.

- Il metodo <code>Arrays.toString(a)</code>, della classe <code>Arrays</code> del pacchetto <code>java.util</code>, restituisce gli elementi di un array come un testo fra parentesi quadre.

<a id="box-20-java-exarraylit"></a>

!!! esempio "Esempio 8.20: array scritto per esteso e iterazione"

    ```java
    import java.util.Arrays;

    int[] a = {9, 12, 3, 16, 19, 11, 12};
    int n = a.length;

    for (int i = 0; i < n; i++) {      // Ciclo sugli indici
        System.out.println("a[" + i + "] = " + a[i]);
    }

    for (int x : a) {                  // Ciclo sugli elementi
        System.out.print(x + " ");
    }
    System.out.println();

    System.out.println(Arrays.toString(a));
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
    9 12 3 16 19 11 12
    [9, 12, 3, 16, 19, 11, 12]
    ```

    L'istruzione <code>import</code> si scrive all'inizio del file, prima della classe.

### 8.7.1 Array bidimensionali

- Gli array bidimensionali (matrici) si dichiarano con due coppie di parentesi quadre <code>[][]</code>, e si allocano con <code>new int[m][n]</code> ($m$ righe e $n$ colonne) in una sola istruzione. L'elemento nella riga $i$ e colonna $j$ si raggiunge come <code>matrix[i][j]</code>, con entrambi gli indici a partire da $0$; <code>matrix.length</code> è il numero di righe e <code>matrix[i].length</code> è il numero di colonne della riga $i$.

- Un array bidimensionale può anche essere creato elencando i suoi valori riga per riga: <code>int[][] c = {{3, 1, 4}, {1, 5, 9}};</code> crea un array con $2$ righe e $3$ colonne, e <code>c[1][2]</code> è l'elemento nella seconda riga e terza colonna, uguale a $9$.

<a id="box-21-java-exmatrix"></a>

!!! esempio "Esempio 8.21: array bidimensionale (matrice)"

    ```java
    int m = 3; // Numero di righe
    int n = 2; // Numero di colonne

    int[][] matrix = new int[m][n]; // Allocazione di una matrice m x n

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            matrix[i][j] = i * j; // Esempio di assegnamento di valori
        }
    }

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            System.out.println("matrix[" + i + "][" + j + "] = " + matrix[i][j]);
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    matrix[0][0] = 0
    matrix[0][1] = 0
    matrix[1][0] = 0
    matrix[1][1] = 1
    matrix[2][0] = 0
    matrix[2][1] = 2
    ```

### 8.7.2 Liste di dimensione variabile: <code>ArrayList</code>

- Quando il numero di elementi non è noto in anticipo, la classe <code>ArrayList</code> del pacchetto <code>java.util</code> fornisce una lista che cresce durante l'esecuzione, come le liste di <code>Python</code>. Il tipo di dato di una lista di interi è <code>ArrayList&lt;Integer&gt;</code>: gli elementi di una <code>ArrayList</code> sono oggetti, e <code>Integer</code> è la classe che corrisponde a <code>int</code>.

- Il metodo <code>add(x)</code> aggiunge l'elemento <code>x</code> in fondo alla lista, <code>get(i)</code> restituisce l'elemento di indice $i$, <code>set(i, x)</code> lo sostituisce, e <code>size()</code> restituisce il numero di elementi.

<a id="box-22-java-exarraylist"></a>

!!! esempio "Esempio 8.22: una lista di dimensione variabile"

    ```java
    import java.util.ArrayList;

    ArrayList<Integer> list = new ArrayList<>(); // Lista vuota

    for (int i = 1; i <= 4; i++) {
        list.add(i * i);  // La lista cresce
    }
    list.set(0, 100);     // Sostituisce l'elemento di indice 0

    System.out.println(list + " ha " + list.size() + " elementi");
    System.out.println("list.get(2) = " + list.get(2));
    ```

    <strong>Output:</strong>

    ```text
    [100, 4, 9, 16] ha 4 elementi
    list.get(2) = 9
    ```

## 8.8 Metodi (funzioni)

Come nello pseudocodice, un algoritmo è scritto come una funzione che riceve l'input e restituisce l'output. In <code>Java</code> le funzioni si chiamano <strong>metodi</strong> e devono sempre essere definite dentro una <strong>classe</strong>.

- Un metodo in <code>Java</code> è composto da:

    1. un <strong>modificatore di accesso</strong> opzionale (ad esempio <code>public</code>, <code>private</code>) e la parola chiave <code>static</code> quando il metodo appartiene alla classe invece che a un oggetto della classe (tutti i metodi di questo capitolo sono <code>static</code>);

    2. un <strong>tipo di ritorno</strong>: specifica il tipo del valore restituito (<code>void</code> se non viene restituito nulla);

    3. un <strong>nome del metodo</strong>: l'identificatore univoco del metodo;

    4. un <strong>elenco di parametri</strong> (opzionale): specifica i valori in ingresso, ciascuno con il suo tipo di dato;

    5. un <strong>corpo</strong>: il blocco di codice eseguito quando il metodo viene chiamato;

    6. un'istruzione <code>return</code>, obbligatoria se il tipo di ritorno non è <code>void</code>.

- Il <strong>punto di ingresso</strong> di ogni programma <code>Java</code> è il metodo <code>public static void main(String[] args)</code>, che svolge il ruolo della funzione <code>main</code> di <code>C++</code>. Il parametro <code>args</code> contiene le parole scritte dopo il nome della classe nel comando <code>java</code>.

- A differenza di <code>C++</code>, un metodo può essere chiamato prima del punto in cui è definito nella classe: l'ordine dei metodi dentro una classe non conta.

- Il codice sorgente <code>Java</code> può anche essere compilato ed eseguito online, per esempio al seguente indirizzo:<br> [www.mycompiler.io/online-java-compiler](https://www.mycompiler.io/online-java-compiler)

<a id="box-23-java-exmethods"></a>

!!! esempio "Esempio 8.23: metodi"

    ```java
    public class Main {

        // Definizione di metodo
        static int addition(int a, int b) {
            return a + b; // Restituisce la somma
        }

        // Definizione di metodo
        static int multiplication(int a, int b) {
            return a * b; // Restituisce il prodotto
        }

        public static void main(String[] args) {
            int sum = addition(5, 10);         // Chiamata di metodo
            System.out.println("Somma: " + sum);

            int prod = multiplication(5, 10);  // Chiamata di metodo
            System.out.println("Prodotto: " + prod);
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    Somma: 15
    Prodotto: 50
    ```

<a id="box-24-java-exsummatrix"></a>

!!! esempio "Esempio 8.24: metodo che opera su un array bidimensionale"

    ```java
    public class Main {

        static int sumMatrix(int[][] matrix, int rows, int cols) {
            int sum = 0;
            for (int i = 0; i < rows; i++) {
                for (int j = 0; j < cols; j++) {
                    sum += matrix[i][j];
                }
            }
            return sum;
        }

        public static void main(String[] args) {
            int m = 3, n = 2;
            int[][] matrix = new int[m][n];

            for (int i = 0; i < m; i++)
                for (int j = 0; j < n; j++)
                    matrix[i][j] = i * j;

            int total = sumMatrix(matrix, m, n);
            System.out.println("Somma degli elementi della matrice: " + total);
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    Somma degli elementi della matrice: 3
    ```

    Il corpo di un ciclo <code>for</code> fatto di una sola istruzione può essere scritto senza parentesi graffe, come in <code>C++</code>.

### 8.8.1 Parametri e valori di ritorno

- In <code>Java</code> ogni parametro è passato <strong>per valore</strong>: il metodo riceve una copia dell'argomento. Per i tipi di dato primitivi (<code>int</code>, <code>double</code>, <code>boolean</code>, <code>char</code>) le modifiche fatte alla copia non influiscono sulla variabile di chi chiama; non esiste il passaggio per riferimento con il simbolo <code>&amp;</code> di <code>C++</code>.

- Una variabile di tipo <code>int[]</code> non contiene gli elementi, ma un <strong>riferimento</strong> all'array (simile al puntatore di <code>C++</code>). Il metodo riceve una copia del riferimento, che punta allo stesso array: le modifiche fatte agli <em>elementi</em> dell'array sono visibili a chi chiama.

- Un metodo restituisce al più un valore. Quando un metodo deve restituire più risultati, può restituirli in un array, per esempio <code>new int[]{q, r}</code>.

<a id="box-25-java-exparams"></a>

!!! esempio "Esempio 8.25: parametri e risultati multipli"

    ```java
    public class Main {

        static void increment(int x) {
            x = x + 1; // Modifica solo la copia locale
        }

        static void fillWithZeros(int[] a) {
            for (int i = 0; i < a.length; i++) {
                a[i] = 0; // Modifica l'array di chi chiama
            }
        }

        static int[] divide(int n, int m) {
            return new int[]{n / m, n % m}; // Due risultati in un array
        }

        public static void main(String[] args) {
            int k = 5;
            increment(k);
            System.out.println("Dopo increment: " + k);

            int[] b = {4, 7, 1};
            fillWithZeros(b);
            System.out.println("Array: " + b[0] + " " + b[1] + " " + b[2]);

            int[] qr = divide(17, 5);
            System.out.println("Quoziente e resto: " + qr[0] + " " + qr[1]);
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    Dopo increment: 5
    Array: 0 0 0
    Quoziente e resto: 3 2
    ```

## 8.9 Un algoritmo completo: il valore massimo in un array

Mettiamo ora insieme tutti i pezzi: un metodo, un ciclo, un'istruzione condizionale e un array.

!!! chiave ""

    Consideriamo il problema di trovare il valore massimo in un array $a$ di $n \ge 1$ numeri interi.

- Questo è lo pseudocodice dell'algoritmo <code>FindMaximum</code> del capitolo «Pseudocodice»: le componenti sono indicizzate da $1$ a $n$.

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

- Questa è l'implementazione in <code>Java</code>. Gli elementi sono indicizzati da $0$ a $n-1$, quindi l'inizializzazione usa <code>a[0]</code> e il ciclo parte da <code>i = 1</code>. La dimensione $n$ non è passata come parametro, perché il metodo la ottiene con <code>a.length</code>. Il metodo suppone $n \ge 1$, come lo pseudocodice: per un array vuoto l'accesso ad <code>a[0]</code> ferma il programma con una <code>ArrayIndexOutOfBoundsException</code>.

    ```java
    public class Main {

        // Metodo che trova il valore massimo in un array
        static int arrayMaxValue(int[] a) {
            int max = a[0]; // Inizializza con il primo elemento

            for (int i = 1; i < a.length; i++) {
                if (a[i] > max) {
                    max = a[i]; // Aggiorna il massimo
                }
            }

            return max;
        }

        public static void main(String[] args) {
            int[] a = {9, 12, 3, 16, 19, 11, 12};

            int max = arrayMaxValue(a);
            System.out.println("Valore massimo: " + max);
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    Valore massimo: 19
    ```

- L'istanza di prova può anche essere generata a caso con la classe <code>Random</code> del pacchetto <code>java.util</code>: se <code>rand</code> è un oggetto di questa classe, <code>rand.nextInt(100)</code> restituisce un intero casuale fra $0$ e $99$, quindi <code>rand.nextInt(100) + 1</code> è fra $1$ e $100$. L'oggetto creato con <code>new Random(2026)</code> parte dal valore fisso $2026$ (il <strong>seme</strong>), in modo che ogni esecuzione produca lo stesso array; l'oggetto creato con <code>new Random()</code> produce un array diverso a ogni esecuzione.

<a id="box-26-java-exrandom"></a>

!!! esempio "Esempio 8.26: un'istanza casuale"

    ```java
    import java.util.Arrays;
    import java.util.Random;

    public class Main {

        static int arrayMaxValue(int[] a) {
            int max = a[0];
            for (int i = 1; i < a.length; i++) {
                if (a[i] > max) {
                    max = a[i];
                }
            }
            return max;
        }

        public static void main(String[] args) {
            int n = 10;  // Dimensione dell'array
            int[] a = new int[n];
            Random rand = new Random(2026); // Stesso array casuale a ogni esecuzione
            for (int i = 0; i < n; i++) {
                a[i] = rand.nextInt(100) + 1; // Intero casuale fra 1 e 100
            }

            System.out.println(Arrays.toString(a));
            System.out.println("Valore massimo: " + arrayMaxValue(a));
        }
    }
    ```

    <strong>Output:</strong>

    ```text
    [100, 51, 98, 31, 50, 39, 74, 37, 35, 79]
    Valore massimo: 100
    ```

<a id="box-27-java-extrace"></a>

!!! esempio "Esempio 8.27: esecuzione passo per passo"

    In ogni tabella, la colonna $i$ è l'indice del ciclo <code>Java</code> e la colonna $i+1$ è l'indice corrispondente dello pseudocodice. La prima riga è l'inizializzazione <code>max = a[0]</code>.

    <strong>Istanza 1:</strong> $a = [9, 12, 3, 16, 19, 11, 12]$, $n=7$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span> (<code>Java</code>)</th>
    <th><span class="arithmatex">&#92;(i+1&#92;)</span> (pseudocodice)</th>
    <th><code>a[i]</code></th>
    <th><code>a[i] &gt; max</code>?</th>
    <th><code>max</code></th>
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

    <strong>Restituisce:</strong> <code>max</code> $= 19$

    <strong>Istanza 2:</strong> $a = [3, 7, 2, 9, 1]$, $n=5$

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">&#92;(i&#92;)</span> (<code>Java</code>)</th>
    <th><span class="arithmatex">&#92;(i+1&#92;)</span> (pseudocodice)</th>
    <th><code>a[i]</code></th>
    <th><code>a[i] &gt; max</code>?</th>
    <th><code>max</code></th>
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

    <strong>Restituisce:</strong> <code>max</code> $= 9$

## 8.10 Operatori bit a bit

Gli operatori bit a bit del capitolo «Introduzione a <code>C++</code>» esistono in <code>Java</code> con gli stessi simboli e lo stesso significato: <code>&amp;</code> (AND), <code>|</code> (OR), <code></code> (XOR), <code>~</code> (NOT), <code>&lt; &lt;</code> (scorrimento a sinistra) e <code>&gt; &gt;</code> (scorrimento a destra). Il metodo <code>Integer.toBinaryString(x)</code> restituisce la rappresentazione binaria di un intero.

- Un valore di tipo <code>int</code> ha $32$ bit, quindi <code>~12</code> inverte $32$ bit e dà <code>-13</code>; il risultato a $8$ bit di <code>C++</code> si ottiene con la maschera <code>0xFF</code>, come in <code>Python</code>.

- <code>Java</code> ha un terzo operatore di scorrimento, <code>&gt; &gt; &gt;</code> (scorrimento a destra senza segno), che aggiunge sempre zeri a sinistra, anche per i numeri negativi; per i numeri non negativi coincide con <code>&gt; &gt;</code>.

- Poiché una condizione deve essere di tipo <code>boolean</code>, il test del bit meno significativo si scrive <code>(n &amp; 1) == 1</code>, e non <code>(n &amp; 1)</code> come in <code>C++</code>.

<a id="box-28-java-exbitwise"></a>

!!! esempio "Esempio 8.28: operatori bit a bit"

    ```java
    int a = 12; // Binario: 1100
    int b = 10; // Binario: 1010

    System.out.println((a & b) + " " + (a | b) + " " + (a ^ b)); // AND, OR, XOR
    System.out.println(Integer.toBinaryString(a & b));           // 1000
    System.out.println((5 << 2) + " " + (20 >> 2) + " " + (20 >> 3)); // Scorrimenti
    System.out.println(~a + " " + (~a & 0xFF));  // NOT, e la sua versione a 8 bit
    System.out.println((-8 >> 1) + " " + (-8 >>> 28)); // Scorrimento con e senza segno

    int n = 15;
    System.out.println(((n & 1) == 1) ? "dispari" : "pari"); // Bit meno significativo
    ```

    <strong>Output:</strong>

    ```text
    8 14 6
    1000
    20 5 2
    -13 243
    -4 15
    dispari
    ```

    Il numero $-8$ è memorizzato come $11\dots11000$ ($32$ bit): <code>-8 &gt; &gt; 1</code> mantiene il segno e dà $-4$, mentre <code>-8 &gt; &gt; &gt; 28</code> mantiene solo i $4$ bit più a sinistra $1111$, cioè $15$.

## 8.11 <code>Java</code>, <code>C++</code> e <code>Python</code> a confronto

La tabella seguente riassume le principali differenze fra i tre linguaggi di questa parte del corso.

<div class="tabella" markdown="0"><table>
<tr>
<th></th>
<th><code>C++</code></th>
<th><code>Java</code></th>
<th><code>Python</code></th>
</tr>
<tr>
<td>Esecuzione</td>
<td>compilato (<code>g++</code>)</td>
<td>compilato in bytecode (<code>javac</code>), eseguito dalla JVM (<code>java</code>)</td>
<td>interpretato (<code>python3</code>)</td>
</tr>
<tr>
<td>Tipi di dato</td>
<td>dichiarati</td>
<td>dichiarati</td>
<td>non dichiarati</td>
</tr>
<tr>
<td>Blocchi</td>
<td><code>{}</code></td>
<td><code>{}</code></td>
<td><code>:</code> e indentazione</td>
</tr>
<tr>
<td>Fine dell'istruzione</td>
<td><code>;</code></td>
<td><code>;</code></td>
<td>fine della riga</td>
</tr>
<tr>
<td>Valori booleani</td>
<td><code>true</code>, <code>false</code> (stampati <code>1</code>, <code>0</code>)</td>
<td><code>true</code>, <code>false</code></td>
<td><code>True</code>, <code>False</code></td>
</tr>
<tr>
<td><code>10 / 3</code></td>
<td><code>3</code></td>
<td><code>3</code></td>
<td><code>3.3333333333333335</code></td>
</tr>
<tr>
<td><code>-7 / 2</code> (intero)</td>
<td><code>-3</code></td>
<td><code>-3</code></td>
<td><code>-7 // 2</code> vale <code>-4</code></td>
</tr>
<tr>
<td>Intero più grande</td>
<td><span class="arithmatex">&#92;(2^{31}-1&#92;)</span> per <code>int</code></td>
<td><span class="arithmatex">&#92;(2^{31}-1&#92;)</span> per <code>int</code></td>
<td>nessun limite</td>
</tr>
<tr>
<td>Operatori logici</td>
<td><code>&amp;&amp;</code>, <code>||</code>, <code>!</code></td>
<td><code>&amp;&amp;</code>, <code>||</code>, <code>!</code></td>
<td><code>and</code>, <code>or</code>, <code>not</code></td>
</tr>
<tr>
<td>Collezioni</td>
<td>array, liberati con <code>delete[]</code></td>
<td>array (<code>a.length</code>) e <code>ArrayList</code>, liberati automaticamente</td>
<td>liste (<code>len(a)</code>), liberate automaticamente</td>
</tr>
<tr>
<td>Indice fuori intervallo</td>
<td>non controllato</td>
<td>eccezione</td>
<td>eccezione</td>
</tr>
<tr>
<td>Più risultati</td>
<td>parametri per riferimento</td>
<td>restituzione di un array</td>
<td>restituzione di una tupla</td>
</tr>
<tr>
<td>Punto di ingresso</td>
<td>funzione <code>main</code></td>
<td>metodo <code>main</code> di una classe</td>
<td>livello più esterno del file</td>
</tr>
</table></div>

!!! chiave ""

    <strong>Punti chiave del capitolo</strong>

    - Un programma <code>Java</code> è costituito da classi; è compilato in bytecode con <code>javac</code> ed eseguito dalla JVM con <code>java</code>, a partire dal metodo <code>public static void main(String[] args)</code>.

    - Ogni variabile è dichiarata con il suo tipo di dato, che è controllato dal compilatore; il tipo di dato <code>int</code> ha $32$ bit, e la divisione fra due interi è la divisione intera.

    - Le istruzioni condizionali (<code>if</code>, <code>else if</code>, <code>else</code>, <code>?:</code>) e i cicli (<code>while</code>, <code>for</code>, e il <code>for</code> esteso) hanno la stessa sintassi di <code>C++</code>, ma una condizione deve essere di tipo <code>boolean</code>.

    - Gli array di <code>Java</code> si allocano con <code>new</code>, conoscono la loro dimensione <code>a.length</code>, sono indicizzati da $0$ a $n-1$ e sono liberati automaticamente; la classe <code>ArrayList</code> fornisce liste di dimensione variabile.

    - I parametri sono passati per valore; un metodo che riceve un array può modificarne gli elementi, e più risultati sono restituiti insieme in un array.

---

**Esercizi su questo capitolo:** [:material-pencil: Introduzione a Java](../esercizi/es-08-introduzione-java.md)
