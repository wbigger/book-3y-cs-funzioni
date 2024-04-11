# Funzioni

La funzione è un blocco di codice che può essere usato più volte con parametri diversi.

```c
int somma(int a, int b) {       // line 1
    int c = a+b;                // line 2
    return c;                   // line 3
}                               // line 4
```

Analizziamo la struttura di una funzione:

- il primo `int` nella riga 1 è il _tipo_ del valore di ritorno
- la parola `somma` è il _nome_ della funzione
- le variabili `a` e `b` sono i _parametri_ della funzione
- il blocco di codice nelle parentesi graffe è il codice che verrà eseguito dalla funzione
- nella riga 3, la parola chiave `return` fa restituire alla funzione il valore `c` e termina il blocco

> Nota: se la funzione non ritorna nessun valore, il tipo del valore di ritorno è `void`

Abbiamo anche le seguenti definizioni:

- la riga 1 è chiamata _dichiarazione_ della funzione, dove dichiaro appunto il nome della funzione, il valore di ritorno ed i parametri
- il blocco di codice viene chiamato _definizione_ della funzione

La funzione può essere usata (si dice anche _chiamata_ o _invocata_) nei seguenti modi:

```c
int main() {
    int s1 = somma(1,2);
    int s2 = somma(5,9);
    int s3 = somma(s1,10);
    int s3 = somma(-4,s2);
    int s4 = somma(s1,s3);
    // etc...
    return 0;
}
```

Quindi facciamo attenzione:

- il _numero_ dei parametri con cui chiamo la funzione deve essere la stesso della definizione della funzione
- il _tipo_ dei parametri deve essere lo stesso, e nello stesso ordine

Fate inoltre attenzione che il nome dei parametri _all'interno_ della funzione dipende solo dalla dichiarazione della funzione, non da come viene chiamata! Nel nostro esempio, nel main chiamo la funzione in molti modi diversi, ma dentro la funzione il primo parametro si chiama sempre `a` ed il secondo sempre `b`.

In linea generale, posso scrivere una funzione che faccia qualsiasi cosa, ma la maggior parte delle volte le operazioni che voglio fare rientrano in alcuni casi tipici che è bene saper individuare e risolvere in maniera corretta. Nelle prossime pagine vedremo alcuni dei casi più comuni che riguardano funzioni che hanno in ingresso un array.
