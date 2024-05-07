# Uso delle funzioni con strutture: mappatura

Immaginiamo di voler inserire gli animali in un catalogo, nel quale però ci interessa salvare solo specie e razza; vogliamo inoltre aggiungere un identificativo sotto forma di numero intero.

Creiamo una nuova struct `AnimaleCatalogo` e la relativa funzione di stampa.

```c
struct AnimaleCatalogo {
  char specie[20];
  char razza[20];
  int id; // identificativo
};

// Creo la funzione di stampa della nuova struct
void stampa_animale_catalogo(struct AnimaleCatalogo animale) {
  printf("animaliCatalogo: id %d, specie %s, razza %s\n", animale.id,
         animale.razza, animale.specie);
  return;
}
```

Ora scriviamo la funzione che mappa l'array degli animali con quelli di animali catalogo. Copiamo solo i campi che ci interessano e per gli altri mettiamo dei valori di default come richiesto dallo scenario.

```c
void mappa_catalogo(struct Animale arr_in[],
                    struct AnimaleCatalogo arr_out[], int len) {
  for (int i = 0; i < len; i++) {
    strncpy(arr_out[i].specie, arr_in[i].specie, 20);
    strncpy(arr_out[i].razza, arr_in[i].razza, 20);
    arr_out[i].id = i; // come identificativo metto la posizione nell'array
  }
  return;
}

int main() {
  struct Animale animali[] = {
      {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F},
      {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F}};
  struct AnimaleCatalogo animaliCatalogo[2];
  mappa_catalogo(animali, animaliCatalogo, 2);

  for (int i = 0; i < 2; i++) {
    stampa_animale_catalogo(animaliCatalogo[i]);
  }
  return 0;
}
```

