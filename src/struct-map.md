# Uso delle funzioni con strutture: mappatura

Immaginiamo di voler inserire gli animali in un catalogo, nel quale però ci interessa salvare solo specie e razza

Creiamo una nuova struct `AnimaleCatalogo` e facciamo la mappatura.

```c
struct AnimaleCatalogo {
  char specie[20];
  char razza[20];
};

void mappa_catalogo(struct Animale animale_in[], struct AnimaleCatalogo animale_out[], int len) {
  for (int i = 0; i < len; i++) {
        strncpy(animale_out[i].specie,animale_in[i].specie, 20);
        strncpy(animale_out[i].razza,animale_in[i].razza, 20);
    }
    return;
}

int main() {
  struct Animale animali[] = {
    {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F},
    {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F}
  };
  struct AnimaleCatalogo animaliCatalogo[2];
  mappa_catalogo(animali,animaliCatalogo,2);
  for (int i = 0; i < 2; i++) {
    printf("animaliCatalogo[%d]: specie %s, razza %s\n",i,animaliCatalogo[i].razza,animaliCatalogo[i].specie);
  }
  return 0;
}
```

