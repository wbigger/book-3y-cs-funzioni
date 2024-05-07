# Uso delle funzioni con strutture: filtro

Immaginiamo di volere un array con solo gli animali con un prezzo inferiore ai 700 euro.

Creiamo la funzione `filtra_prezzo` per questo scopo.

```c
struct Animale *filtra_prezzo(struct Animale animali[], int n, int *counter) {

  struct Animale *arr_out = malloc(sizeof(struct Animale) * n);

  for (int i = 0; i < n; i++) {
    if (animali[i].prezzo_vendita <= 700.0F) {
      arr_out[*counter] = animali[i];
      (*counter)++;
    }
  }
  arr_out = realloc(arr_out, sizeof(struct Animale) * (*counter));

  return arr_out;
}
```

Ora testiamo la funzione nel main, per controllare che il nuovo array contenga effettivamente solo gli animali con il prezzo richiesto.

```c
int main() {
  struct Animale animali[] = {
      {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F},
      {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F}};
  int counter = 0;
  struct Animale *animaliEconomici =
      filtra_prezzo(animali, 2, &counter);
  for (int i = 0; i < counter; i++) {
    stampa_animale(animaliEconomici[i]);
  }
  free(animaliEconomici);
}
```
