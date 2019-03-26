Răspunsul: `1`.

```js run
let i = 3;

while (i) {
  alert( i-- );
}
```

Fiecare iterație a buclei decrementează `i` cu `1`. Verificarea `while(i)` oprește bucla când `i = 0`.

De aceea pașii buclei formează următoarea secvență ("buclă nerulată"):

```js
let i = 3;

alert(i--); // shows 3, decreases i to 2

alert(i--) // shows 2, decreases i to 1

alert(i--) // shows 1, decreases i to 0

// done, while(i) check stops the loop
```
