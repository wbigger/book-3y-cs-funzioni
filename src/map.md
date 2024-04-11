# Mappatura

La funzione di mappatura associa ad ogni elemento di un array un elemento di un altro array.

La struttura di una funzione di mappatura è la seguente:

```c
void calcola_quadrato(int arr_in[], int arr_out[], int len){
    for (int i = 0; i < len; i++) {
        arr_out[i] = arr_in[i]*arr_in[i];
    }
    return; // opzionale quando la funzione ritorna void
}
```

Viene invocata nel seguente modo:

```c
int main() {
    int a1[] = {1,2,3,4};
    int a2[4];
    calcola_quadrato(a1,a2,4);
}
```

Cose a cui prestare attenzione:

- la lunghezza dell'array di input deve essere la stessa dell'array di output
- il _tipo_ degli elementi dell'array di input può essere diverso del tipo degli elementi dell'array di output

## Altri esempi

```c
void trasforma_maiuscolo(char str_in[], char str_out[], int len){
    for (int i = 0; i < len; i++) {
        str_out[i] = str_in[i] - 32;
    }
    return;
}
```

```c
void dimezza(char arr_in[], char arr_out[], int len){
    for (int i = 0; i < len; i++) {
        arr_out[i] = arr_in[i] / 2.0F; // importante .0F per forzare una divisione tra float
    }
    return;
}
```
