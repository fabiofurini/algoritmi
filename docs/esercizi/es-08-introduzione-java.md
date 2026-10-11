---
title: "Esercizi · Introduzione a Java"
---

# Esercizi · Introduzione a Java

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 8** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 8](../linguaggi/08-introduzione-java.md) · [:material-file-pdf-box: Eserciziario, volume 2 (PDF)](../pdf/esercizi-2-linguaggi-di-programmazione.pdf)

</div>

Negli esercizi di questo capitolo i programmi sono scritti, compilati ed eseguiti con le convenzioni del capitolo «Introduzione a <code>Java</code>», riassunte qui sotto.

??? codice "Codice"

    - Il programma di un esercizio è una classe <code>Main</code>, salvata nel file <code>Main.java</code> (ogni esercizio in una cartella propria), compilata ed eseguita con i comandi

        ```text
        javac Main.java
        java Main
        ```

    - I metodi sono metodi <code>static</code> della classe <code>Main</code>. Le istanze di test sono array scritti nel codice, ad esempio <code>int[] arr1 = {9, 12, 3, 16, 19, 11, 12};</code>, e sono passate ai metodi senza la loro dimensione: un metodo ottiene la dimensione $n$ di un array <code>a</code> con <code>a.length</code>.

    - Gli elementi di un array di dimensione $n$ sono <code>a[0]</code>, <code>a[1]</code>, …, <code>a[n-1]</code>: la componente $a[i]$ di un'istanza scritta come $a = [\dots]$ nel testo corrisponde ad <code>a[i-1]</code> nel codice, e gli indici stampati dai programmi partono da $0$.

    - Un metodo restituisce al più un valore: i risultati che un metodo deve restituire insieme sono restituiti in un array (<code>int[]</code> o <code>double[]</code>).

    - Quando un array è stampato con un ciclo, ogni valore è seguito da uno spazio, quindi le righe stampate terminano con uno spazio.

    - Il formato <code>%.4f</code> di <code>printf</code> visualizza un numero in virgola mobile con esattamente $4$ cifre dopo la virgola decimale. Gli output sono quelli di un calcolatore con impostazioni in inglese: con le impostazioni in italiano <code>printf</code> scrive la virgola decimale (<code>11,7143</code>).

<a id="esercizio-8-1"></a>

!!! esercizio "Esercizio 8.1: Introduzione a {\tt Java} (E1)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il valore massimo nell'array.

    **Domande**

    1. Scrivere un programma <code>Java</code> completo che trova il valore massimo in un array $a$ di $n$ numeri interi. Il programma deve:

        - definire un metodo statico <code>int arrayMaxValue(int[] a)</code> dentro la classe <code>Main</code>;

        - nel metodo <code>main</code>, creare gli array di test e chiamare il metodo;

        - stampare i risultati per ogni caso di test.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare i comandi di compilazione ed esecuzione e l'output per tutti i casi di test.

    3. Modificare il metodo in modo che restituisca sia il valore massimo sia il suo indice. Poiché un metodo <code>Java</code> restituisce un solo valore, restituire un array <code>int[]</code> di due elementi: <code>{maxValue, maxIndex}</code>. Eseguire la versione modificata sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Java</code> completo:</strong>

        ```java
        public class Main {

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
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                System.out.print("Prova 1 - Array: ");
                for (int x : arr1) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore massimo: " + arrayMaxValue(arr1));
                System.out.println();

                int[] arr2 = {5, 2, 8, 1};
                System.out.print("Prova 2 - Array: ");
                for (int x : arr2) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore massimo: " + arrayMaxValue(arr2));
                System.out.println();

                int[] arr3 = {42};
                System.out.print("Prova 3 - Array: ");
                for (int x : arr3) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore massimo: " + arrayMaxValue(arr3));
            }
        }
        ```

        Gli array sono stampati con il ciclo <code>for</code> esteso, che visita direttamente i loro elementi. Per l'Istanza 3 la condizione <code>1 &lt; a.length</code> è falsa fin dall'inizio, il ciclo non esegue nessuna iterazione, e il metodo restituisce l'unico elemento <code>a[0]</code>.

    2. <strong>Compilazione ed esecuzione:</strong>

        ```text
        javac Main.java
        java Main
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12
        Valore massimo: 19

        Prova 2 - Array: 5 2 8 1
        Valore massimo: 8

        Prova 3 - Array: 42
        Valore massimo: 42
        ```

    3. <strong>Metodo modificato che restituisce il valore massimo e il suo indice:</strong>

        ```java
        public class Main {

            // Restituisce int[]{maxValue, maxIndex}
            static int[] arrayMaxValueWithIndex(int[] a) {
                int max = a[0];
                int idx = 0;

                for (int i = 1; i < a.length; i++) {
                    if (a[i] > max) {
                        max = a[i];
                        idx = i; // Memorizza l'indice
                    }
                }
                return new int[]{max, idx};
            }

            public static void main(String[] args) {
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                int[] result = arrayMaxValueWithIndex(arr1);
                System.out.println("Valore massimo: " + result[0]
                                 + ", all'indice: " + result[1]);
            }
        }
        ```

        <strong>Output:</strong>

        ```text
        Valore massimo: 19, all'indice: 4
        ```

        Per l'Istanza 1 il metodo restituisce l'array $\{19,\ 4\}$: il valore massimo $19$ è all'indice $4$ (indici da $0$), cioè nella posizione $5$ dell'array $a[1..7]$ del testo. Se il valore massimo compare più volte, il metodo restituisce l'indice della sua prima occorrenza, perché <code>max</code> e <code>idx</code> sono aggiornati solo quando <code>a[i] &gt; max</code> (disuguaglianza stretta).

<a id="esercizio-8-2"></a>

!!! esercizio "Esercizio 8.2: Introduzione a {\tt Java} (E2)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il valore minimo nell'array.

    **Domande**

    1. Scrivere un programma <code>Java</code> completo che trova il valore minimo in un array $a$ di $n$ numeri interi. Il programma deve:

        - definire un metodo statico <code>int arrayMinValue(int[] a)</code> dentro la classe <code>Main</code>;

        - nel metodo <code>main</code>, creare gli array di test e chiamare il metodo;

        - stampare i risultati per ogni caso di test.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare i comandi di compilazione ed esecuzione e l'output per tutti i casi di test.

    3. Modificare il metodo in modo che restituisca sia il valore minimo sia il suo indice. Poiché un metodo <code>Java</code> restituisce un solo valore, restituire un array <code>int[]</code> di due elementi: <code>{minValue, minIndex}</code>. Eseguire la versione modificata sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Java</code> completo:</strong>

        ```java
        public class Main {

            static int arrayMinValue(int[] a) {
                int min = a[0]; // Inizializza con il primo elemento

                for (int i = 1; i < a.length; i++) {
                    if (a[i] < min) {
                        min = a[i]; // Aggiorna il minimo
                    }
                }
                return min;
            }

            public static void main(String[] args) {
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                System.out.print("Prova 1 - Array: ");
                for (int x : arr1) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore minimo: " + arrayMinValue(arr1));
                System.out.println();

                int[] arr2 = {5, 2, 8, 1};
                System.out.print("Prova 2 - Array: ");
                for (int x : arr2) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore minimo: " + arrayMinValue(arr2));
                System.out.println();

                int[] arr3 = {42};
                System.out.print("Prova 3 - Array: ");
                for (int x : arr3) System.out.print(x + " ");
                System.out.println();
                System.out.println("Valore minimo: " + arrayMinValue(arr3));
            }
        }
        ```

        Gli array sono stampati con il ciclo <code>for</code> esteso, che visita direttamente i loro elementi. Per l'Istanza 3 la condizione <code>1 &lt; a.length</code> è falsa fin dall'inizio, il ciclo non esegue nessuna iterazione, e il metodo restituisce l'unico elemento <code>a[0]</code>.

    2. <strong>Compilazione ed esecuzione:</strong>

        ```text
        javac Main.java
        java Main
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12
        Valore minimo: 3

        Prova 2 - Array: 5 2 8 1
        Valore minimo: 1

        Prova 3 - Array: 42
        Valore minimo: 42
        ```

    3. <strong>Metodo modificato che restituisce il valore minimo e il suo indice:</strong>

        ```java
        public class Main {

            // Restituisce int[]{minValue, minIndex}
            static int[] arrayMinValueWithIndex(int[] a) {
                int min = a[0];
                int idx = 0;

                for (int i = 1; i < a.length; i++) {
                    if (a[i] < min) {
                        min = a[i];
                        idx = i; // Memorizza l'indice
                    }
                }
                return new int[]{min, idx};
            }

            public static void main(String[] args) {
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                int[] result = arrayMinValueWithIndex(arr1);
                System.out.println("Valore minimo: " + result[0]
                                 + ", all'indice: " + result[1]);
            }
        }
        ```

        <strong>Output:</strong>

        ```text
        Valore minimo: 3, all'indice: 2
        ```

        Per l'Istanza 1 il metodo restituisce l'array $\{3,\ 2\}$: il valore minimo $3$ è all'indice $2$ (indici da $0$), cioè nella posizione $3$ dell'array $a[1..7]$ del testo. Se il valore minimo compare più volte, il metodo restituisce l'indice della sua prima occorrenza, perché <code>min</code> e <code>idx</code> sono aggiornati solo quando <code>a[i] &lt; min</code> (disuguaglianza stretta).

<a id="esercizio-8-3"></a>

!!! esercizio "Esercizio 8.3: Introduzione a {\tt Java} (E3)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare la somma e la media di tutti i suoi elementi.

    **Domande**

    1. Scrivere un programma <code>Java</code> completo che calcola la somma e la media degli elementi di un array $a$ di $n$ numeri interi. Il programma deve:

        - definire un metodo statico <code>int arraySum(int[] a)</code> che restituisce la somma;

        - definire un metodo statico <code>double arrayAverage(int[] a)</code> che restituisce la media;

        - nel metodo <code>main</code>, creare gli array di test, chiamare entrambi i metodi e stampare i risultati, con la media arrotondata a $4$ cifre decimali.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare i comandi di compilazione ed esecuzione e l'output per tutti i casi di test.

    3. Scrivere un unico metodo <code>arraySumAndAverage(int[] a)</code> che restituisce sia la somma sia la media. Poiché un metodo <code>Java</code> restituisce un solo valore, restituire il risultato come un array <code>double[]</code> di due elementi: <code>{sum, average}</code>. Eseguirlo sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Java</code> completo:</strong>

        ```java
        public class Main {

            static int arraySum(int[] a) {
                int total = 0;
                for (int i = 0; i < a.length; i++) {
                    total += a[i];
                }
                return total;
            }

            static double arrayAverage(int[] a) {
                return (double) arraySum(a) / a.length;
            }

            static void printTest(int k, int[] a) {
                System.out.print("Prova " + k + " - Array: ");
                for (int x : a) System.out.print(x + " ");
                System.out.println();
                System.out.println("Somma: " + arraySum(a));
                System.out.printf("Media: %.4f%n", arrayAverage(a));
            }

            public static void main(String[] args) {
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                printTest(1, arr1);
                System.out.println();

                int[] arr2 = {5, 2, 8, 1};
                printTest(2, arr2);
                System.out.println();

                int[] arr3 = {42};
                printTest(3, arr3);
            }
        }
        ```

        La conversione <code>(double)</code> è necessaria: senza di essa, <code>arraySum(a) / a.length</code> sarebbe la divisione intera, e per l'Istanza 1 la media sarebbe $82/7 = 11$. Il metodo <code>printTest</code> stampa l'array e i due risultati, ed evita di scrivere tre volte le stesse istruzioni.

    2. <strong>Compilazione ed esecuzione:</strong>

        ```text
        javac Main.java
        java Main
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12
        Somma: 82
        Media: 11.7143

        Prova 2 - Array: 5 2 8 1
        Somma: 16
        Media: 4.0000

        Prova 3 - Array: 42
        Somma: 42
        Media: 42.0000
        ```

        Per l'Istanza 1 la media esatta è $82/7 = 11.714285\ldots$, visualizzata come $11.7143$.

    3. <strong>Metodo combinato:</strong>

        ```java
        public class Main {

            // Restituisce double[]{somma, media}
            static double[] arraySumAndAverage(int[] a) {
                int total = 0;
                for (int x : a) total += x;
                double avg = (double) total / a.length;
                return new double[]{total, avg};
            }

            public static void main(String[] args) {
                int[] arr1 = {9, 12, 3, 16, 19, 11, 12};
                double[] result = arraySumAndAverage(arr1);
                System.out.printf("Somma: %.0f, Media: %.4f%n",
                                  result[0], result[1]);
            }
        }
        ```

        <strong>Output:</strong>

        ```text
        Somma: 82, Media: 11.7143
        ```

        L'intero <code>total</code> è convertito automaticamente in un <code>double</code> quando viene memorizzato nell'array <code>double[]</code>; per questo motivo è stampato con il formato <code>%.0f</code> (nessuna cifra decimale) invece di <code>%d</code>, che accetta solo interi.

<a id="esercizio-8-4"></a>

!!! esercizio "Esercizio 8.4: Introduzione a {\tt Java} (E4)"

    Dato un array $a$ di $n$ numeri interi e un valore $m$, consideriamo il problema di determinare se il valore $m$ è presente o no nell'array.

    **Domande**

    1. Scrivere un programma <code>Java</code> completo che esegue una <strong>ricerca lineare</strong> in un array $a$. Il programma deve:

        - definire un metodo statico <code>int linearSearch(int[] a, int m)</code> che cerca il valore <code>m</code> nell'array <code>a</code>;

        - restituire l'indice della prima occorrenza di <code>m</code> se viene trovato, oppure <code>-1</code> se non viene trovato;

        - nel metodo <code>main</code>, eseguire i casi di test e stampare i risultati.

    2. Eseguire il programma sull'array $a = [9, 12, 3, 16, 19, 11, 12]$ con i seguenti valori:

        - $m = 16$ (presente nell'array)

        - $m = 12$ (presente due volte: si restituisce l'indice della prima occorrenza)

        - $m = 7$ (non presente nell'array)

        Mostrare i comandi di compilazione ed esecuzione e l'output per tutti i casi di test.

    3. Modificare il metodo in modo che restituisca un array <code>int[]</code> contenente <strong>tutti gli indici</strong> in cui compare il valore $m$ (invece della sola prima occorrenza). Usare una <code>ArrayList&lt;Integer&gt;</code> dentro il metodo e convertirla in un <code>int[]</code> prima di restituirla. Eseguirlo con $m = 12$ e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Java</code> completo:</strong>

        ```java
        public class Main {

            static int linearSearch(int[] a, int m) {
                for (int i = 0; i < a.length; i++) {
                    if (a[i] == m) {
                        return i; // Trovato: restituisce l'indice
                    }
                }
                return -1; // Non trovato
            }

            static void printResult(int[] a, int m) {
                int idx = linearSearch(a, m);
                if (idx != -1) System.out.println("Valore " + m + " trovato all'indice " + idx);
                else           System.out.println("Valore " + m + " non trovato");
            }

            public static void main(String[] args) {
                int[] a = {9, 12, 3, 16, 19, 11, 12};
                System.out.print("Array: ");
                for (int x : a) System.out.print(x + " ");
                System.out.println();
                System.out.println();

                printResult(a, 16);
                printResult(a, 12);
                printResult(a, 7);
            }
        }
        ```

        L'istruzione <code>return i</code> termina il metodo, e quindi il ciclo, alla prima occorrenza di <code>m</code>; l'istruzione <code>return -1</code> viene raggiunta solo quando il ciclo ha visitato l'intero array senza trovare <code>m</code>. Si usa il valore <code>-1</code> perché non può essere un indice dell'array.

    2. <strong>Compilazione ed esecuzione:</strong>

        ```text
        javac Main.java
        java Main
        ```

        <strong>Output:</strong>

        ```text
        Array: 9 12 3 16 19 11 12

        Valore 16 trovato all'indice 3
        Valore 12 trovato all'indice 1
        Valore 7 non trovato
        ```

        Il valore $12$ si trova negli indici $1$ e $6$, e il metodo restituisce il primo. Nell'array $a[1..7]$ del testo, gli indici $3$ e $1$ corrispondono alle posizioni $4$ e $2$.

    3. <strong>Metodo che restituisce tutte le occorrenze:</strong>

        ```java
        import java.util.ArrayList;

        public class Main {

            static int[] linearSearchAll(int[] a, int m) {
                ArrayList<Integer> indices = new ArrayList<>();
                for (int i = 0; i < a.length; i++) {
                    if (a[i] == m) {
                        indices.add(i);
                    }
                }
                // Conversione della ArrayList<Integer> in un int[]
                int[] result = new int[indices.size()];
                for (int i = 0; i < indices.size(); i++) {
                    result[i] = indices.get(i);
                }
                return result;
            }

            public static void main(String[] args) {
                int[] a = {9, 12, 3, 16, 19, 11, 12};
                int m = 12;
                int[] occurrences = linearSearchAll(a, m);

                if (occurrences.length > 0) {
                    System.out.print("Valore " + m + " trovato agli indici: ");
                    for (int idx : occurrences) System.out.print(idx + " ");
                    System.out.println();
                } else {
                    System.out.println("Valore " + m + " non trovato");
                }
            }
        }
        ```

        <strong>Output:</strong>

        ```text
        Valore 12 trovato agli indici: 1 6
        ```

        Il numero di occorrenze non è noto in anticipo, quindi gli indici sono prima raccolti in una <code>ArrayList</code>, che cresce con <code>add</code>; poi si alloca e si riempie un array della dimensione giusta <code>indices.size()</code>. A differenza di <code>linearSearch</code>, questo metodo visita sempre l'intero array. Se <code>m</code> non è presente, il metodo restituisce un array di lunghezza $0$.

<a id="esercizio-8-5"></a>

!!! esercizio "Esercizio 8.5: Introduzione a {\tt Java} (E5)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare in un solo passaggio il massimo, il minimo, la somma e la media di tutti gli elementi dell'array.

    **Domande**

    1. Scrivere un programma <code>Java</code> completo che calcola in un <strong>solo passaggio</strong> le quattro statistiche (massimo, minimo, somma, media) di un array $a$ di $n$ numeri interi. Il programma deve:

        - definire un metodo statico <code>arrayStats(int[] a)</code> che calcola i quattro valori con un solo ciclo;

        - restituire i risultati come un array <code>double[]</code> di quattro elementi: <code>{max, min, sum, average}</code>;

        - nel metodo <code>main</code>, eseguire i casi di test e stampare i risultati.

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare i comandi di compilazione ed esecuzione e l'output per tutti i casi di test.

    3. Modificare il metodo in modo che restituisca anche gli indici dell'elemento massimo e dell'elemento minimo, come un array <code>double[]</code> di sei elementi: <code>{max, maxIdx, min, minIdx, sum, average}</code>. Eseguirlo sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Programma <code>Java</code> completo:</strong>

        ```java
        public class Main {

            // Restituisce double[]{massimo, minimo, somma, media}
            static double[] arrayStats(int[] a) {
                int max = a[0];
                int min = a[0];
                int total = a[0];

                for (int i = 1; i < a.length; i++) {
                    if (a[i] > max) max = a[i];
                    if (a[i] < min) min = a[i];
                    total += a[i];
                }

                double avg = (double) total / a.length;
                return new double[]{max, min, total, avg};
            }

            static void printStats(int k, int[] a) {
                double[] s = arrayStats(a);
                System.out.print("Prova " + k + " - Array: ");
                for (int x : a) System.out.print(x + " ");
                System.out.println();
                System.out.println("  Massimo: " + (int) s[0]);
                System.out.println("  Minimo:  " + (int) s[1]);
                System.out.println("  Somma:   " + (int) s[2]);
                System.out.printf("  Media:   %.4f%n", s[3]);
            }

            public static void main(String[] args) {
                printStats(1, new int[]{9, 12, 3, 16, 19, 11, 12});
                System.out.println();
                printStats(2, new int[]{5, 2, 8, 1});
                System.out.println();
                printStats(3, new int[]{42});
            }
        }
        ```

        Le tre variabili sono inizializzate con il primo elemento, e il ciclo visita una sola volta gli altri $n-1$ elementi. I quattro risultati hanno tipi di dato diversi, quindi sono tutti memorizzati come <code>double</code> nell'array restituito; i risultati interi sono riconvertiti con <code>(int)</code> prima della stampa, in modo che siano visualizzati senza la parte decimale (<code>19</code> invece di <code>19.0</code>). L'espressione <code>new int[]{…}</code> crea un array direttamente nella chiamata.

    2. <strong>Compilazione ed esecuzione:</strong>

        ```text
        javac Main.java
        java Main
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12
          Massimo: 19
          Minimo:  3
          Somma:   82
          Media:   11.7143

        Prova 2 - Array: 5 2 8 1
          Massimo: 8
          Minimo:  1
          Somma:   16
          Media:   4.0000

        Prova 3 - Array: 42
          Massimo: 42
          Minimo:  42
          Somma:   42
          Media:   42.0000
        ```

    3. <strong>Metodo esteso che restituisce anche gli indici:</strong>

        ```java
        public class Main {

            // Restituisce double[]{max, maxIdx, min, minIdx, somma, media}
            static double[] arrayStatsWithIndices(int[] a) {
                int max = a[0], maxIdx = 0;
                int min = a[0], minIdx = 0;
                int total = a[0];

                for (int i = 1; i < a.length; i++) {
                    if (a[i] > max) { max = a[i]; maxIdx = i; }
                    if (a[i] < min) { min = a[i]; minIdx = i; }
                    total += a[i];
                }

                double avg = (double) total / a.length;
                return new double[]{max, maxIdx, min, minIdx, total, avg};
            }

            public static void main(String[] args) {
                int[] a = {9, 12, 3, 16, 19, 11, 12};
                double[] r = arrayStatsWithIndices(a);
                System.out.println("Max:   " + (int) r[0] + " all'indice " + (int) r[1]);
                System.out.println("Min:   " + (int) r[2] + " all'indice " + (int) r[3]);
                System.out.println("Somma: " + (int) r[4]);
                System.out.printf("Media: %.4f%n", r[5]);
            }
        }
        ```

        <strong>Output:</strong>

        ```text
        Max:   19 all'indice 4
        Min:   3 all'indice 2
        Somma: 82
        Media: 11.7143
        ```

        Il massimo $19$ è all'indice $4$ e il minimo $3$ all'indice $2$ (indici da $0$), cioè nelle posizioni $5$ e $3$ dell'array $a[1..7]$ del testo.
