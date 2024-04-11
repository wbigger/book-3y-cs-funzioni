# Uso delle funzioni con strutture: riduzione

Le funzioni che abbiamo visto con gli array di elementi semplici possono essere facilmente estesi con array di strutture.

## Scenario

Immaginiamo di avere un negozio di animali. Creiamo la struttura per rappresentare un animale in vendita.

```c
struct Animale {
  char specie[20];
  char razza[20];
  int eta; // giorni
  float peso; // chilogrammi
  char mangime[50];
  float prezzo_vendita; // euro
};
```

Scriviamo anche la funzione di stampa:

```c
void stampa_animale(struct Animale animale) {
  printf("Specie %s, razza %s, ha %d giorni, pesa %.1f kg, "
         "mangia %s.\n", animale.specie, animale.razza, animale.eta, animale.peso,
         animale.mangime);
  printf("Il prezzo di vendita è %.2f euro.\n", animale.prezzo_vendita);
}
```

Ed infine testiamo la funzione nel main:

```c
int main() {
  struct Animale gatto = {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F};
  stampa_animale(gatto);
  return 0;
}
```

### Stampa migliorata

Quando stampiamo l'età, è utile stamparla in modo più chiaro per l'utente.

Vogliamo che:

- se l'età è inferiore ad un mese, stampiamo solo i giorni
- se l'età è maggiore di un mese ma minore di un anno, stampiamo mesi e giorni
- se l'età è maggiore di un anno, stampiamo anni, mesi e giorni
- è accettabile un'età approssimativa con mesi di 30 giorni e anni di 365 giorni

La nuova funzione di stampa diventa:

```c
void stampa_animale(struct Animale animale) {
  int anni = animale.eta / 365;
  int mesi = (animale.eta % 365) / 30;
  int giorni = (animale.eta % 365) % 30;
  printf("Specie %s, razza %s, pesa %.1f kg, "
         "mangia %s.\n",
         animale.specie, animale.razza, animale.peso, animale.mangime);
  if (animale.eta <= 30) {
    printf("L'animale ha %d giorni\n", giorni);
  } else if (animale.eta < 365) {
    printf("L'animale ha %d mesi e %d giorni\n", mesi, giorni);
  } else {
    printf("L'animale ha %d anni, %d mesi e %d giorni\n", anni, mesi, giorni);
  }
  printf("Il prezzo di vendita è %.2f euro.\n", animale.prezzo_vendita);
}
```

## Array di struct

Creiamo un array con tutti gli animali del negozio.

Ci sono diversi metodi per creare un array di struct, ne facciamo vedere alcuni. Tutti i seguenti blocchi portano allo stesso risultato.

```c
// Dichiaro gli oggetti e poi li assegno
struct Animale gatto = {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F};
struct Animale cane = {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F};
struct Animale animali[2];
animali[0] = gatto;
animali[1] = cane;
```

```c
// Dichiaro gli oggetti e poi li assegno nell'inzializzazione dell'array
struct Animale gatto = {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F};
struct Animale cane = {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F};
struct Animale animali[] = {gatto, cane}; // non serve specificare la dimensione dell'array
```

```c
// Dichiaro l'array e poi lo assegno
struct Animale animali[2];

strncpy(animali[0].specie,"gatto",20);
strncpy(animali[0].razza,"siamese",20);
animali[0].eta = 100;
animali[0].peso = 1.2F;
strncpy(animali[0].mangime,"cibo per gatti",50);
animali[0].prezzo_vendita = 600.00F;

strncpy(animali[1].specie,"cane",20);
strncpy(animali[1].razza,"labrador",20);
animali[1].eta = 80;
animali[1].peso = 5.5F;
strncpy(animali[0].mangime,"croccantini",50);
animali[1].prezzo_vendita = 800.00F;
```

```c
// Dichiaro l'array e lo inizializzo nella stessa riga
struct Animale animali[] = {
    {"gatto", "siamese", 100, 1.2F, "cibo per gatti", 600.00F},
    {"cane", "labrador", 80, 5.5F, "croccantini", 800.00F}
};
```

Quale uso? Ovviamente dipende, da quanto è grande la struct, se ho già gli oggetti da inserire, preferenze personali, etc. In generale preferire sempre la chiarezza e rendere difficili gli errori, quindi se la struttura ha tanti campi, meglio non rischiare di sbagliare facendo inizializzazioni manuali troppo lunghe.

## Riduzione

Calcoliamo il prezzo medio degli animali del negozio. L'impostazione della funzione è la stessa che abbiamo già visto.

```c
float calcola_media(struct Animale animali[], int len) {
    float ret = 0.0F;
    float somma = 0.0F;
    for (int i = 0; i < len; i++) {
        somma += animali[i].prezzo_vendita;
    }
    return somma/len;
}
```
