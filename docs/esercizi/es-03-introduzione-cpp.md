---
title: "Esercizi · Introduzione a C++"
---

# Esercizi · Introduzione a C++

<div class="info-capitolo" markdown>

**Esercizi · Capitolo 3** · ogni soluzione si apre con un clic · [:material-book-open-variant: Capitolo 3](../fondamenti/03-introduzione-cpp.md) · [:material-file-pdf-box: Eserciziario, volume 1 (PDF)](../pdf/esercizi-1-fondamenti.pdf)

</div>

Negli esercizi di questo capitolo i programmi sono scritti, compilati ed eseguiti con le convenzioni del capitolo «Introduzione a <code>C++</code>», riassunte qui sotto.

??? codice "Codice"

    - Il programma di un esercizio è salvato in un file <code>&lt;name&gt;.cpp</code>, compilato ed eseguito con i comandi

        ```bash
        g++ -Wall -std=c++17 -o <name> <name>.cpp
        ./<name>
        ```

    - Le istanze di test sono array di dimensione fissa dichiarati in <code>main</code>, ad esempio <code>int arr1[] = {9, 12, 3, 16, 19, 11, 12};</code>, e vengono passate alle funzioni tramite il puntatore al loro primo elemento (<code>int \*a</code>) insieme alla loro dimensione <code>n</code>.

    - Gli elementi di un array di dimensione $n$ sono <code>a[0]</code>, <code>a[1]</code>, …, <code>a[n-1]</code>: la componente $a[i]$ di un'istanza scritta come $a = [\dots]$ nel testo corrisponde ad <code>a[i-1]</code> nel codice.

    - I risultati che una funzione deve restituire oltre al valore di ritorno sono passati per riferimento (<code>int&amp; x</code>, <code>double&amp; x</code>).

    - Quando si stampa un array, ogni valore è seguito da uno spazio, quindi le righe stampate terminano con uno spazio.

<a id="esercizio-3-1"></a>

!!! esercizio "Esercizio 3.1: Introduzione a {\tt C++} (E1)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il valore massimo nell'array.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che trova il valore massimo in un array $a$ di $n$ numeri interi. Il programma deve:

        - Definire una funzione <code>int ArrayMaxValue(int n, int \*a)</code> che implementa l'algoritmo

        - Nella funzione <code>main()</code>, creare gli array di test e chiamare la funzione

        - Stampare i risultati per ogni caso di test

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        - Istanza 3: $a = [42]$ con $n=1$

        Mostrare i comandi di compilazione completi e l'output per tutti i casi di test.

    3. Modificare il programma creando una nuova funzione <code>int ArrayMaxValueWithIndex(int n, int \*a, int&amp; idx)</code> che restituisce il valore massimo e memorizza il suo indice nel parametro per riferimento <code>idx</code>. Eseguire questa versione modificata e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che trova il valore massimo di un array
        int ArrayMaxValue(int n, int *a) 
        {
            int max = a[0];  // Inizializza con il primo elemento

            for (int i = 1; i < n; i++) 
            {
                if (a[i] > max) 
                {
                    max = a[i];  // Aggiorna il massimo
                }
            }

            return max;
        }

        int main() 
        {
            // Caso di prova 1
            int arr1[] = {9, 12, 3, 16, 19, 11, 12};
            int n1 = 7;

            cout << "Prova 1 - Array: ";
            for (int i = 0; i < n1; i++) 
            {
                cout << arr1[i] << " ";
            }
            cout << endl;

            int max1 = ArrayMaxValue(n1, arr1);
            cout << "Valore massimo: " << max1 << endl;
            cout << endl;

            // Caso di prova 2
            int arr2[] = {5, 2, 8, 1};
            int n2 = 4;

            cout << "Prova 2 - Array: ";
            for (int i = 0; i < n2; i++) 
            {
                cout << arr2[i] << " ";
            }
            cout << endl;

            int max2 = ArrayMaxValue(n2, arr2);
            cout << "Valore massimo: " << max2 << endl;
            cout << endl;

            // Caso di prova 3
            int arr3[] = {42};
            int n3 = 1;

            cout << "Prova 3 - Array: ";
            for (int i = 0; i < n3; i++) 
            {
                cout << arr3[i] << " ";
            }
            cout << endl;

            int max3 = ArrayMaxValue(n3, arr3);
            cout << "Valore massimo: " << max3 << endl;

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o max_value max_value.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./max_value
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

    3. <strong>Programma modificato con l'indice:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che trova il valore massimo e il suo indice
        int ArrayMaxValueWithIndex(int n, int *a, int& idx) 
        {
            int max = a[0];
            idx = 0;

            for (int i = 1; i < n; i++) 
            {
                if (a[i] > max) 
                {
                    max = a[i];
                    idx = i;  // Memorizza l'indice
                }
            }

            return max;
        }

        int main() 
        {
            int arr[] = {9, 12, 3, 16, 19, 11, 12};
            int n = 7;
            int index;

            cout << "Array: ";
            for (int i = 0; i < n; i++) 
            {
                cout << arr[i] << " ";
            }
            cout << endl;

            int max = ArrayMaxValueWithIndex(n, arr, index);

            cout << "Valore massimo: " << max << endl;
            cout << "Posizione (indice): " << index << endl;

            return 0;
        }
        ```

        <strong>Output:</strong>

        ```text
        Array: 9 12 3 16 19 11 12 
        Valore massimo: 19
        Posizione (indice): 4
        ```

        Nota: il valore massimo 19 si trova all'indice 4 (l'elemento di posizione 5, poiché in <code>C++</code> gli array sono indicizzati a partire da $0$). Se il valore massimo compare più di una volta, la funzione memorizza l'indice della sua prima occorrenza, perché <code>max</code> e <code>idx</code> vengono aggiornati solo quando <code>a[i] &gt; max</code> (disuguaglianza stretta).

<a id="esercizio-3-2"></a>

!!! esercizio "Esercizio 3.2: Introduzione a {\tt C++} (E2)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di trovare il suo valore minimo.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che trova il valore minimo in un array $a$ di $n$ numeri interi. Il programma deve:

        - Definire una funzione <code>int ArrayMinValue(int n, int \*a)</code> che implementa l'algoritmo

        - Nella funzione <code>main()</code>, creare gli array di test e chiamare la funzione

        - Stampare i risultati per ogni caso di test

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [15, 7, 22, 4]$ con $n=4$

        - Istanza 3: $a = [100]$ con $n=1$

        Mostrare i comandi di compilazione completi e l'output per tutti i casi di test.

    3. Modificare il programma creando una nuova funzione <code>void ArrayMaxMin(int n, int \*a, int&amp; max, int&amp; min)</code> che trova sia il valore massimo sia il valore minimo con un solo passaggio sull'array. Eseguire questa versione modificata e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che trova il valore minimo di un array
        int ArrayMinValue(int n, int *a) 
        {
            int m = a[0];  // Inizializza con il primo elemento

            for (int i = 1; i < n; i++) 
            {
                if (a[i] < m) 
                {
                    m = a[i];  // Aggiorna il minimo
                }
            }

            return m;
        }

        int main() 
        {
            // Caso di prova 1
            int arr1[] = {9, 12, 3, 16, 19, 11, 12};
            int n1 = 7;

            cout << "Prova 1 - Array: ";
            for (int i = 0; i < n1; i++) 
            {
                cout << arr1[i] << " ";
            }
            cout << endl;

            int min1 = ArrayMinValue(n1, arr1);
            cout << "Valore minimo: " << min1 << endl;
            cout << endl;

            // Caso di prova 2
            int arr2[] = {15, 7, 22, 4};
            int n2 = 4;

            cout << "Prova 2 - Array: ";
            for (int i = 0; i < n2; i++) 
            {
                cout << arr2[i] << " ";
            }
            cout << endl;

            int min2 = ArrayMinValue(n2, arr2);
            cout << "Valore minimo: " << min2 << endl;
            cout << endl;

            // Caso di prova 3
            int arr3[] = {100};
            int n3 = 1;

            cout << "Prova 3 - Array: ";
            for (int i = 0; i < n3; i++) 
            {
                cout << arr3[i] << " ";
            }
            cout << endl;

            int min3 = ArrayMinValue(n3, arr3);
            cout << "Valore minimo: " << min3 << endl;

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o min_value min_value.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./min_value
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12 
        Valore minimo: 3

        Prova 2 - Array: 15 7 22 4 
        Valore minimo: 4

        Prova 3 - Array: 100 
        Valore minimo: 100
        ```

    3. <strong>Programma modificato per trovare sia il massimo sia il minimo:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che trova sia il massimo sia il minimo
        void ArrayMaxMin(int n, int *a, int& max, int& min) 
        {
            max = a[0];
            min = a[0];

            for (int i = 1; i < n; i++) 
            {
                if (a[i] > max) 
                {
                    max = a[i];
                }
                if (a[i] < min) 
                {
                    min = a[i];
                }
            }
        }

        int main() 
        {
            int arr[] = {9, 12, 3, 16, 19, 11, 12};
            int n = 7;
            int maximum, minimum;

            cout << "Array: ";
            for (int i = 0; i < n; i++) 
            {
                cout << arr[i] << " ";
            }
            cout << endl;

            ArrayMaxMin(n, arr, maximum, minimum);

            cout << "Valore massimo: " << maximum << endl;
            cout << "Valore minimo: " << minimum << endl;

            return 0;
        }
        ```

        <strong>Output:</strong>

        ```text
        Array: 9 12 3 16 19 11 12 
        Valore massimo: 19
        Valore minimo: 3
        ```

        Nota: questa implementazione trova sia il valore massimo sia il valore minimo con un solo passaggio sull'array. Il numero di confronti è lo stesso che con due funzioni separate, $2(n-1)$, ma l'array viene scorso una volta sola invece di due.

<a id="esercizio-3-3"></a>

!!! esercizio "Esercizio 3.3: Introduzione a {\tt C++} (E3)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare la somma e la media di tutti i suoi elementi.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che calcola la somma e la media degli elementi di un array $a$ di $n$ numeri interi. Il programma deve:

        - Definire una funzione <code>int ArraySum(int n, int \*a)</code> che calcola la somma degli elementi dell'array

        - Nella funzione <code>main()</code>, creare gli array di test e chiamare la funzione

        - Calcolare e stampare sia la somma sia la media per ogni caso di test

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [5, 12, 3, 8]$ con $n=4$

        - Istanza 2: $a = [10, 20, 30]$ con $n=3$

        - Istanza 3: $a = [7]$ con $n=1$

        Mostrare i comandi di compilazione completi e l'output per tutti i casi di test.

    3. Modificare il programma creando una nuova funzione <code>void ArraySumAndAverage(int n, int \*a, int&amp; sum, double&amp; avg)</code> che calcola sia la somma sia la media in un'unica funzione. Eseguire questa versione modificata e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        #include <iomanip>
        using namespace std;

        // Funzione che calcola la somma degli elementi dell'array
        int ArraySum(int n, int *a) 
        {
            int S = 0;

            for (int i = 0; i < n; i++) 
            {
                S = S + a[i];
            }

            return S;
        }

        int main() 
        {
            // Caso di prova 1
            int arr1[] = {5, 12, 3, 8};
            int n1 = 4;

            cout << "Prova 1 - Array: ";
            for (int i = 0; i < n1; i++) 
            {
                cout << arr1[i] << " ";
            }
            cout << endl;

            int sum1 = ArraySum(n1, arr1);
            double avg1 = (double)sum1 / n1;
            cout << "Somma: " << sum1 << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << avg1 << endl;
            cout << endl;

            // Caso di prova 2
            int arr2[] = {10, 20, 30};
            int n2 = 3;

            cout << "Prova 2 - Array: ";
            for (int i = 0; i < n2; i++) 
            {
                cout << arr2[i] << " ";
            }
            cout << endl;

            int sum2 = ArraySum(n2, arr2);
            double avg2 = (double)sum2 / n2;
            cout << "Somma: " << sum2 << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << avg2 << endl;
            cout << endl;

            // Caso di prova 3
            int arr3[] = {7};
            int n3 = 1;

            cout << "Prova 3 - Array: ";
            for (int i = 0; i < n3; i++) 
            {
                cout << arr3[i] << " ";
            }
            cout << endl;

            int sum3 = ArraySum(n3, arr3);
            double avg3 = (double)sum3 / n3;
            cout << "Somma: " << sum3 << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << avg3 << endl;

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o array_sum array_sum.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./array_sum
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 5 12 3 8 
        Somma: 28
        Media: 7.00

        Prova 2 - Array: 10 20 30 
        Somma: 60
        Media: 20.00

        Prova 3 - Array: 7 
        Somma: 7
        Media: 7.00
        ```

    3. <strong>Programma modificato con la funzione combinata:</strong>

        ```cpp
        #include <iostream>
        #include <iomanip>
        using namespace std;

        // Funzione che calcola sia la somma sia la media
        void ArraySumAndAverage(int n, int *a, int& sum, double& avg) 
        {
            sum = 0;

            for (int i = 0; i < n; i++) 
            {
                sum = sum + a[i];
            }

            avg = (double)sum / n;
        }

        int main() 
        {
            int arr[] = {5, 12, 3, 8};
            int n = 4;
            int sum;
            double average;

            cout << "Array: ";
            for (int i = 0; i < n; i++) 
            {
                cout << arr[i] << " ";
            }
            cout << endl;

            ArraySumAndAverage(n, arr, sum, average);

            cout << "Somma: " << sum << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << average << endl;

            return 0;
        }
        ```

        <strong>Output:</strong>

        ```text
        Array: 5 12 3 8 
        Somma: 28
        Media: 7.00
        ```

        Nota: il manipolatore <code>setprecision(2)</code> serve a formattare la media con 2 cifre decimali. La conversione <code>(double)</code> garantisce la divisione in virgola mobile: senza di essa, <code>sum / n</code> sarebbe la divisione intera. Poiché la media divide per $n$, le funzioni richiedono $n \ge 1$.

<a id="esercizio-3-4"></a>

!!! esercizio "Esercizio 3.4: Introduzione a {\tt C++} (E4)"

    Dato un array $a$ di $n$ numeri interi e un valore $m$, consideriamo il problema di determinare se il valore $m$ è presente o meno nell'array.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che implementa l'algoritmo di ricerca lineare per un array $a$ di $n$ numeri interi. Il programma deve:

        - Definire una funzione <code>int LinearSearch(int n, int \*a, int m)</code> che cerca il valore <code>m</code> nell'array <code>a</code>

        - Restituire l'indice dell'elemento se viene trovato, oppure <code>-1</code> se non viene trovato

        - Nella funzione <code>main()</code>, creare un array di test e cercare valori diversi

        - Stampare i risultati di ogni ricerca

    2. Eseguire il programma con la seguente istanza:

        - Array: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Ricerca di: $m=16$ (elemento presente)

        - Ricerca di: $m=25$ (elemento non presente)

        - Ricerca di: $m=9$ (primo elemento)

        - Ricerca di: $m=12$ (elemento duplicato)

        Mostrare i comandi di compilazione completi e l'output per tutti i casi di test.

    3. Modificare il programma creando una funzione <code>int CountOccurrences(int n, int \*a, int m)</code> che conta quante volte il valore <code>m</code> compare nell'array. Eseguire questa versione modificata con il valore $m=12$ nell'array di test e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che esegue la ricerca lineare
        int LinearSearch(int n, int *a, int m) 
        {
            for (int i = 0; i < n; i++) 
            {
                if (a[i] == m) 
                {
                    return i;  // Trovato: restituisce l'indice
                }
            }

            return -1;  // Non trovato
        }

        int main() 
        {
            int arr[] = {9, 12, 3, 16, 19, 11, 12};
            int n = 7;

            cout << "Array: ";
            for (int i = 0; i < n; i++) 
            {
                cout << arr[i] << " ";
            }
            cout << endl << endl;

            // Prova 1: ricerca di 16 (presente)
            int m1 = 16;
            int result1 = LinearSearch(n, arr, m1);
            cout << "Ricerca di " << m1 << ": ";
            if (result1 != -1) 
            {
                cout << "Trovato all'indice " << result1 << endl;
            } 
            else 
            {
                cout << "Non trovato" << endl;
            }

            // Prova 2: ricerca di 25 (assente)
            int m2 = 25;
            int result2 = LinearSearch(n, arr, m2);
            cout << "Ricerca di " << m2 << ": ";
            if (result2 != -1) 
            {
                cout << "Trovato all'indice " << result2 << endl;
            } 
            else 
            {
                cout << "Non trovato" << endl;
            }

            // Prova 3: ricerca di 9 (primo elemento)
            int m3 = 9;
            int result3 = LinearSearch(n, arr, m3);
            cout << "Ricerca di " << m3 << ": ";
            if (result3 != -1) 
            {
                cout << "Trovato all'indice " << result3 << endl;
            } 
            else 
            {
                cout << "Non trovato" << endl;
            }

            // Prova 4: ricerca di 12 (ripetuto)
            int m4 = 12;
            int result4 = LinearSearch(n, arr, m4);
            cout << "Ricerca di " << m4 << ": ";
            if (result4 != -1) 
            {
                cout << "Trovato all'indice " << result4 
                     << " (prima occorrenza)" << endl;
            } 
            else 
            {
                cout << "Non trovato" << endl;
            }

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o linear_search linear_search.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./linear_search
        ```

        <strong>Output:</strong>

        ```text
        Array: 9 12 3 16 19 11 12 

        Ricerca di 16: Trovato all'indice 3
        Ricerca di 25: Non trovato
        Ricerca di 9: Trovato all'indice 0
        Ricerca di 12: Trovato all'indice 1 (prima occorrenza)
        ```

    3. <strong>Programma modificato per contare le occorrenze:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che conta le occorrenze del valore m
        int CountOccurrences(int n, int *a, int m) 
        {
            int count = 0;

            for (int i = 0; i < n; i++) 
            {
                if (a[i] == m) 
                {
                    count++;
                }
            }

            return count;
        }

        int main() 
        {
            int arr[] = {9, 12, 3, 16, 19, 11, 12};
            int n = 7;

            cout << "Array: ";
            for (int i = 0; i < n; i++) 
            {
                cout << arr[i] << " ";
            }
            cout << endl;

            int x = 12;
            int count = CountOccurrences(n, arr, x);

            cout << "Il valore " << x << " compare " << count 
                 << " volte nell'array" << endl;

            return 0;
        }
        ```

        <strong>Output:</strong>

        ```text
        Array: 9 12 3 16 19 11 12 
        Il valore 12 compare 2 volte nell'array
        ```

        Nota: la funzione <code>LinearSearch</code> restituisce l'indice della prima occorrenza quando ci sono duplicati. La funzione <code>CountOccurrences</code> scorre l'intero array per contare tutte le occorrenze.

<a id="esercizio-3-5"></a>

!!! esercizio "Esercizio 3.5: Introduzione a {\tt C++} (E5)"

    Dato un array $a$ di $n \ge 1$ numeri interi, consideriamo il problema di calcolare con un solo passaggio il massimo, il minimo, la somma e la media di tutti gli elementi dell'array.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che calcola tutte le statistiche di un array $a$ di $n$ numeri interi con un solo passaggio. Il programma deve:

        - Definire una funzione <code>void ArrayStatistics(int n, int \*a, int&amp; max, int&amp; min, int&amp; sum, double&amp; avg)</code> che calcola tutte e quattro le statistiche

        - Nella funzione <code>main()</code>, creare gli array di test e chiamare la funzione

        - Stampare tutte le statistiche per ogni caso di test

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: $a = [9, 12, 3, 16, 19, 11, 12]$ con $n=7$

        - Istanza 2: $a = [5, 2, 8, 1]$ con $n=4$

        Mostrare i comandi di compilazione completi e l'output per tutti i casi di test.

    3. Discutere i vantaggi di calcolare tutte le statistiche con un solo passaggio rispetto a calcolarle separatamente con più funzioni.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        #include <iomanip>
        using namespace std;

        // Funzione che calcola tutte le statistiche in una sola passata
        void ArrayStatistics(int n, int *a, int& max, int& min, 
                             int& sum, double& avg) 
        {
            // Inizializza con il primo elemento
            max = a[0];
            min = a[0];
            sum = a[0];

            // Elabora gli elementi rimanenti
            for (int i = 1; i < n; i++) 
            {
                if (a[i] > max) 
                {
                    max = a[i];
                }
                if (a[i] < min) 
                {
                    min = a[i];
                }
                sum = sum + a[i];
            }

            // Calcola la media
            avg = (double)sum / n;
        }

        int main() 
        {
            // Caso di prova 1
            int arr1[] = {9, 12, 3, 16, 19, 11, 12};
            int n1 = 7;
            int max1, min1, sum1;
            double avg1;

            cout << "Prova 1 - Array: ";
            for (int i = 0; i < n1; i++) 
            {
                cout << arr1[i] << " ";
            }
            cout << endl;

            ArrayStatistics(n1, arr1, max1, min1, sum1, avg1);

            cout << "Massimo: " << max1 << endl;
            cout << "Minimo: " << min1 << endl;
            cout << "Somma: " << sum1 << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << avg1 << endl;
            cout << endl;

            // Caso di prova 2
            int arr2[] = {5, 2, 8, 1};
            int n2 = 4;
            int max2, min2, sum2;
            double avg2;

            cout << "Prova 2 - Array: ";
            for (int i = 0; i < n2; i++) 
            {
                cout << arr2[i] << " ";
            }
            cout << endl;

            ArrayStatistics(n2, arr2, max2, min2, sum2, avg2);

            cout << "Massimo: " << max2 << endl;
            cout << "Minimo: " << min2 << endl;
            cout << "Somma: " << sum2 << endl;
            cout << "Media: " << fixed << setprecision(2) 
                 << avg2 << endl;

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o array_stats array_stats.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./array_stats
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Array: 9 12 3 16 19 11 12 
        Massimo: 19
        Minimo: 3
        Somma: 82
        Media: 11.71

        Prova 2 - Array: 5 2 8 1 
        Massimo: 8
        Minimo: 1
        Somma: 16
        Media: 4.00
        ```

    3. <strong>Vantaggi dell'approccio a un solo passaggio:</strong>

        <strong>Vantaggi:</strong>

        - <strong>Meno scorrimenti dell'array:</strong> l'array viene scorso una sola volta invece di una volta per ogni statistica

        - <strong>Codice più compatto:</strong> una sola funzione e un solo ciclo invece di più chiamate di funzione

        - <strong>Migliore per dati in flusso:</strong> può elaborare dati che arrivano in sequenza o che non stanno interamente in memoria

        - <strong>Minore sovraccarico:</strong> una sola inizializzazione e terminazione di ciclo invece di più cicli

        <strong>Svantaggi:</strong>

        - <strong>Meno modulare:</strong> combina più operazioni in una sola funzione, che può essere più difficile da mantenere

        - <strong>Meno flessibile:</strong> se serve una sola statistica, la funzione le calcola comunque tutte

        - <strong>Riutilizzabilità del codice:</strong> non è facile riutilizzare i singoli calcoli delle statistiche in altri contesti

        <strong>Raccomandazione:</strong> l'approccio a un solo passaggio è preferibile quando:

        - servono tutte le statistiche insieme;

        - si lavora con array grandi, per i quali è importante ridurre al minimo gli accessi all'array;

        - si elaborano dati in flusso o dati che non stanno in memoria.

        Le funzioni separate sono migliori quando:

        - servono solo statistiche specifiche;

        - la chiarezza e la modularità del codice hanno priorità maggiore;

        - le singole funzioni possono essere riutilizzate in contesti diversi.

<a id="esercizio-3-6"></a>

!!! esercizio "Esercizio 3.6: Introduzione a {\tt C++} (E6)"

    Dato un array bidimensionale $a$ di $m \times n$ numeri interi, consideriamo il problema di calcolare la somma di tutti i suoi elementi.

    **Domande**

    1. Scrivere un programma <code>C++</code> completo che calcola la somma di tutti gli elementi di un array bidimensionale $a$ di $m \times n$ interi. Il programma deve:

        - Definire una funzione <code>int SumMatrix(int m, int n, int \*\*matrix)</code> che calcola la somma

        - Nella funzione <code>main()</code>, allocare le matrici di test con la memoria dinamica, inizializzarle, chiamare la funzione e stampare i risultati

        - Liberare tutta la memoria allocata dopo l'uso

    2. Eseguire il programma sulle seguenti istanze:

        - Istanza 1: una matrice $3 \times 4$ con valori sequenziali $a[i][j] = (i-1)\cdot n + j$ per $i \in \{1, 2, 3\}$ e $j \in \{1, 2, 3, 4\}$ (righe e colonne numerate da $1$, come nello pseudocodice), cioè

            $$
            \begin{bmatrix}1&2&3&4\\5&6&7&8\\9&10&11&12\end{bmatrix}
            $$

        - Istanza 2: una matrice $2 \times 3$ con valori $\begin{bmatrix} 3 & 1 & 4 \\ 1 & 5 & 9 \end{bmatrix}$

        Mostrare i comandi di compilazione completi e l'output per entrambi i casi di test.

    3. Modificare il programma aggiungendo una funzione <code>void RowSums(int m, int n, int \*\*matrix, int \*rowSums)</code> che calcola la somma di ogni riga e memorizza i risultati nell'array <code>rowSums</code>. Eseguire questa versione modificata sull'Istanza 1 e mostrare l'output.

??? soluzione "Soluzione"

    1. <strong>Complete <code>C++</code> program:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che calcola la somma di tutti gli elementi di una matrice
        int SumMatrix(int m, int n, int **matrix) 
        {
            int sum = 0;
            for (int i = 0; i < m; i++) 
            {
                for (int j = 0; j < n; j++) 
                {
                    sum += matrix[i][j];
                }
            }
            return sum;
        }

        int main() 
        {
            // Caso di prova 1: matrice 3x4 con valori consecutivi
            int m1 = 3, n1 = 4;

            int** mat1 = new int*[m1];
            for (int i = 0; i < m1; i++) 
            {
                mat1[i] = new int[n1];
            }

            int val = 1;
            for (int i = 0; i < m1; i++) 
            {
                for (int j = 0; j < n1; j++) 
                {
                    mat1[i][j] = val++;
                }
            }

            cout << "Prova 1 - Matrice " << m1 << "x" << n1 << ":" << endl;
            for (int i = 0; i < m1; i++) 
            {
                for (int j = 0; j < n1; j++) 
                {
                    cout << mat1[i][j] << " ";
                }
                cout << endl;
            }
            cout << "Somma: " << SumMatrix(m1, n1, mat1) << endl << endl;

            for (int i = 0; i < m1; i++) 
            {
                delete[] mat1[i];
            }
            delete[] mat1;

            // Caso di prova 2: matrice 2x3
            int m2 = 2, n2 = 3;
            int data[2][3] = {{3, 1, 4}, {1, 5, 9}};

            int** mat2 = new int*[m2];
            for (int i = 0; i < m2; i++) 
            {
                mat2[i] = new int[n2];
                for (int j = 0; j < n2; j++) 
                {
                    mat2[i][j] = data[i][j];
                }
            }

            cout << "Prova 2 - Matrice " << m2 << "x" << n2 << ":" << endl;
            for (int i = 0; i < m2; i++) 
            {
                for (int j = 0; j < n2; j++) 
                {
                    cout << mat2[i][j] << " ";
                }
                cout << endl;
            }
            cout << "Somma: " << SumMatrix(m2, n2, mat2) << endl;

            for (int i = 0; i < m2; i++) 
            {
                delete[] mat2[i];
            }
            delete[] mat2;

            return 0;
        }
        ```

    2. <strong>Compilazione ed esecuzione:</strong>

        Per compilare il programma:

        ```bash
        g++ -Wall -std=c++17 -o sum_matrix sum_matrix.cpp
        ```

        Per eseguire il programma:

        ```bash
        ./sum_matrix
        ```

        <strong>Output:</strong>

        ```text
        Prova 1 - Matrice 3x4:
        1 2 3 4 
        5 6 7 8 
        9 10 11 12 
        Somma: 78

        Prova 2 - Matrice 2x3:
        3 1 4 
        1 5 9 
        Somma: 23
        ```

    3. <strong>Funzione per le somme delle righe:</strong>

        ```cpp
        #include <iostream>
        using namespace std;

        // Funzione che calcola la somma di tutti gli elementi di una matrice
        int SumMatrix(int m, int n, int **matrix) 
        {
            int sum = 0;
            for (int i = 0; i < m; i++) 
            {
                for (int j = 0; j < n; j++) 
                {
                    sum += matrix[i][j];
                }
            }
            return sum;
        }

        // Funzione che calcola la somma di ogni riga
        void RowSums(int m, int n, int **matrix, int *rowSums) 
        {
            for (int i = 0; i < m; i++) 
            {
                rowSums[i] = 0;
                for (int j = 0; j < n; j++) 
                {
                    rowSums[i] += matrix[i][j];
                }
            }
        }

        int main() 
        {
            // Caso di prova 1: matrice 3x4 con valori consecutivi
            int m1 = 3, n1 = 4;

            int** mat1 = new int*[m1];
            for (int i = 0; i < m1; i++) 
            {
                mat1[i] = new int[n1];
            }

            int val = 1;
            for (int i = 0; i < m1; i++) 
            {
                for (int j = 0; j < n1; j++) 
                {
                    mat1[i][j] = val++;
                }
            }

            cout << "Matrice " << m1 << "x" << n1 << ":" << endl;
            for (int i = 0; i < m1; i++) 
            {
                for (int j = 0; j < n1; j++) 
                {
                    cout << mat1[i][j] << " ";
                }
                cout << endl;
            }
            cout << "Somma totale: " << SumMatrix(m1, n1, mat1) << endl << endl;

            int* rowSums = new int[m1];
            RowSums(m1, n1, mat1, rowSums);

            cout << "Somme delle righe:" << endl;
            for (int i = 0; i < m1; i++) 
            {
                cout << "Riga " << (i + 1) << ": " << rowSums[i] << endl;
            }

            delete[] rowSums;
            for (int i = 0; i < m1; i++) 
            {
                delete[] mat1[i];
            }
            delete[] mat1;

            return 0;
        }
        ```

        <strong>Output:</strong>

        ```text
        Matrice 3x4:
        1 2 3 4 
        5 6 7 8 
        9 10 11 12 
        Somma totale: 78

        Somme delle righe:
        Riga 1: 10
        Riga 2: 26
        Riga 3: 42
        ```
