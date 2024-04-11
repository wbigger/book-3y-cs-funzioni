# Strutture

Le strutture sono tipi di dato che permettono di raggruppare insieme più variabili per creare qualcosa di semanticamente più elaborato.

> Vedi capitolo del libro A7 a pag.A187

Immaginiamo ad esempio di voler memorizzare le informazioni riguardanti gli studenti di una classe. Posso creare una struct che contenga tutte le informazioni insieme:

```c
struct Nominativo {
  char nome[20];
  char indirizzo[20];
  unsigned int anno; // anno di nascita
  unsigned int mese; // mese di nascita
  unsigned int giorno;  // giorno di nascita
};
```

> Nota: a differenza del libro, qui useremo solo la prima lettera maiuscola per il nome delle struct, che è una convenzione più usata. Anche tutto maiuscolo va bene comunque. NON va bene invece tutto minuscolo, in quanto il nome della struttura è un _tipo_, non una variabile, e quindi non può iniziare con una lettera minuscola.

Per utilizzare questa struttura:

```c
int main(void) {
  struct Nominativo prof; // dichiaro una variabile di tipo struct Nominativo
  strncpy(prof.nome, "Claudio Capobianco", 20);
  strncpy(prof.indirizzo, "Via Tal dei Tali", 20);
  prof.anno = 2000;
  prof.mese = 1;
  prof.giorno = 1;

  return 0;
}
```

Le variabili all'interno di una struct si definiscono anche `campi` o `attributi`.

Cose a cui prestare attenzione:

- deve essere sempre chiaro cosa deve contenere un campo di una struct, mettendo un nome autoesplicativo (es. `int anno_nascita`) oppure un commento (es. `int anno; //anno di nascita`); senza questi accorgimenti non sarebbe chiaro cosa deve contenere la variabile (anno di nascita? iscrizione? diploma?)

## Stampa dei campi di una struct

Ogni volta che creiamo una struct, è utile scrivere una funzione che ne stampi i valori in modo opportuno. Ad esempio, per la nostra struct nominativo:

```c
void stampa_nominativo(struct NOMINATIVO n) {
  printf("Nome: %s\n", n.nome);
  printf("Indirizzo: %s\n", n.indirizzo);
  printf("Data di nascita: %d/%d/%d\n", n.giorno, n.mese, n.anno);
}
```

Possiamo implementare la nostra funzione stampa in modo da rendere più leggibili i valori, ad esempio nel nostro caso abbiamo scritto la data di nascita in una sola riga, come si fa convenzionalmente.

Prestate sempre quindi attenzione a stampare i valori in modo corretto:

- tutte le grandezze devono avere l'unità di misura (metri, secondi, anni, litri, etc.)
- i valori devono essere stampati nel modo in cui l'utente se li aspetta (ad esempio, non 1.5 ore ma 1h 30m)
