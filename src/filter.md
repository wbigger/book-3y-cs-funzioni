# Filtro

La funzione di filtro prende in ingresso un array e ritorna un array con alcuni elementi dell'array di ingresso.

Questa tipologia di funzione presenta un problema nuovo: prima di invocare la funzione, non so quanto sarà lungo l'array di output. Per risolvere il problema, posso usare l'allocazione di memoria dinamica, cioè la _heap_.

## Gestione della heap

La gestione della heap è responsabilità del programmatore, che deve quindi assicurarsi che tutto il ciclo di vita della variabile sia corretto.

> Nota: nella stack non dobbiamo preoccuparci del ciclo di vita della variabile perché è gestita automaticamente dal compilatore.

Il ciclo di vita è formato da:

- creazione: per creare una variabile nella heap, uso la funzione di sistema `malloc()` che prende in ingresso il numero di _byte_ che voglio riservare in memoria; malloc ritorna un puntatore alla variabile appena creata
- manipolazione: posso manipolare l'area di memoria in diversi modi, in particolare a noi interessa poter cambiare il numero di byte della memoria riservata, che si ottiene con la funzione di sistema `realloc()`
- distruzione: la memoria nella heap si libera con la funzione di sistema `free()`

## Funzione di filtro

Detto questo, torniamo ora alla nostra funzione di filtro.

La struttura di una funzione di filtro è la seguente:

```c
// voglio ritornare un array con solo i valori maggiori o uguali a 18
int* maggiorenne(int arr_in[], int n, int* counter) {
  // all'inizio l'array di output ha stessa dimensione di arr_in
  int* arr_out = malloc(sizeof(int)*n);
  for (int i = 0; i < n; i++){
    if (arr_in[i]>18) {
      arr_out[*counter] = arr_in[i];
      (*counter)++;
    }
  }
  // realloco la memoria in modo da occupare solo lo spazio necessario
  arr_out = realloc(arr_out,sizeof(int)* (*counter) );
  return arr_out;
}
```

Posso chiamare questa funzione nel seguente modo:

```c
int main() {
  int x[] = {10, 20, 30};
  int z_counter = 0;
  int* z = maggiorenne(x,3,&z_counter);
  printf("Numero di elementi filtrati: %d\n",z_counter);
  for (int i = 0; i < z_counter; i++){
    printf("Elemento %d filtrato: %d\n",i,z[i]);
  }
  
  free(z); // devo distruggere z quando non mi serve più!
  
  return 0;
}
```

Si può visualizzare la gestione della memoria di questa funzione con PythonTutor:

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=%23include%20%3Cstdio.h%3E%0A%23include%20%3Cstdlib.h%3E%0A%0A%0Aint*%20maggiorenne%28int%20arr_in%5B%5D,%20int%20n,%20int*%20counter%29%20%7B%0A%20%20//%20alloco%20la%20memoria%20nella%20heap%20con%20malloc%0A%20%20//%20all'inizio%20con%20la%20stessa%20dimensione%20di%20arr_in%0A%20%20int*%20arr_out%20%3D%20malloc%28sizeof%28int%29*n%29%3B%0A%20%20//%20int%20counter%20%3D%200%3B%0A%20%20for%20%28int%20i%20%3D%200%3B%20i%20%3C%20n%3B%20i%2B%2B%29%7B%0A%20%20%20%20if%20%28arr_in%5Bi%5D%3E18%29%20%7B%0A%20%20%20%20%20%20arr_out%5B*counter%5D%20%3D%20arr_in%5Bi%5D%3B%0A%20%20%20%20%20%20%28*counter%29%2B%2B%3B%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20//%20realloco%20la%20memoria%20in%20modo%20da%20occupare%20solo%20lo%20spazio%20necessario%0A%20%20arr_out%20%3D%20realloc%28arr_out,sizeof%28int%29*%20%28*counter%29%20%29%3B%0A%20%20return%20arr_out%3B%0A%7D%0A%0Aint%20main%28%29%20%7B%0A%20%20int%20x%5B%5D%20%3D%20%7B10,%2020,%2030%7D%3B%0A%20%20int%20z_counter%20%3D%200%3B%0A%20%20int*%20z%20%3D%20maggiorenne%28x,3,%26z_counter%29%3B%0A%20%20printf%28%22Numero%20di%20elementi%20filtrati%3A%20%25d%5Cn%22,z_counter%29%3B%0A%20%20for%20%28int%20i%20%3D%200%3B%20i%20%3C%20z_counter%3B%20i%2B%2B%29%7B%0A%20%20%20%20printf%28%22Elemento%20%25d%20filtrato%3A%20%25d%5Cn%22,i,z%5Bi%5D%29%3B%0A%20%20%7D%0A%20%20%0A%20%20free%28z%29%3B%0A%20%20%0A%20%20return%200%3B%0A%7D&codeDivHeight=400&codeDivWidth=350&cppShowMemAddrs=true&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Cose a cui prestare attenzione:

- il _tipo_ degli elementi dell'array di input __deve essere lo stesso__ del tipo degli elementi dell'array di output
- la lunghezza dell'array di input varia da un minimo di zero (array vuoto) ad un massimo della lunghezza dell'array di input
- ricordarsi sempre di distruggere la variabile (liberare la memoria) quando non uso più la variabile creata nella malloc, altrimenti genero un bug chiamato [memory leak](https://it.wikipedia.org/wiki/Memory_leak).
