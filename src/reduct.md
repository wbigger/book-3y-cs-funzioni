# Riduzione

Quando ho una funzione che prende come parametro un singolo array e ritorna un unico valore _scalare_ (cioè un valore unico, non un array), la funzione prende il nome di _funzione di riduzione_, perché riduce una serie di valori ad un singolo valore.

Ad esempio la somma applicata ad un array è una funzione di riduzione:

```c
int somma(int array[], int len) {           // line 1
    int ret = 0;                            // line 2
    for (int i = 0; i < len; i++) {         // line 3
        ret += array[i];                    // line 4
    }                                       // line 5
    return ret;                             // line 6
}                                           // line 7
```

Le funzioni di riduzione hanno tutte la stessa struttura:

- nella dichiarazione, la funzione prende esattamente due parametri, un array e la lunghezza dell'array
- ritorna sempre un tipo (non può essere `void`)
- il tipo di ritorno può essere diverso dal tipo degli elementi dell'array
- nella riga 2, dichiaro una variabile con lo stesso tipo del valore di ritorno
- all'interno ha un for che itera su tutti gli elementi dell'array
- all'interno del for eseguo un'operazione specifica per la funzione di riduzione che sto scrivendo
- l'ultima riga è un return che torna la variabile dichiarata nella riga 2

Questa funzione viene chiamata nel seguente modo:

```c
int main() {
    int arr[] = {10,15,18,20};
    int s = somma(arr,4);
    printf("La somma dell'array è: %d\n");
    return 0;
}
```

## Altri esempi

```c
int prodotto(int array[], int len) {
    int ret = 0;
    for (int i = 0; i < len; i++) {
        ret *= array[i];
    }
    return ret;
}
```

```c
float media(int array[], int len) {
    float ret = 0;
    int somma = 0;
    for (int i = 0; i < len; i++) {
        counter += array[i];
    }
    ret = somma / len;
    return ret;
}
```

```c
int max(int array[], int len) {
     // inizializzo il valore di ritorno con il primo valore dell'array
    int ret = array[0];
    for (int i = 0; i < len; i++) {
        // controllo se l'elemento corrente è maggiore, in caso aggiorno ret
        if (array[i] > ret) {
            ret = array[i];
        }
    }
    return ret;
}
```
