Există mulți algoritmi pentru această sarcină.

Să folosim o buclă îmbricată:

```js
For each i in the interval {
  check if i has a divisor from 1..i
  if yes => the value is not a prime
  if no => the value is a prime, show it
}
```

Codul folosind o etichetă:

```js run
let n = 10;

nextPrime:
for (let i = 2; i <= n; i++) { // for each i...

  for (let j = 2; j < i; j++) { // look for a divisor..
    if (i % j == 0) continue nextPrime; // not a prime, go next i
  }

  alert( i ); // a prime
}
```

Poate fi optimizat în multe moduri. Spre exemplu, am putea căuta pentru divizori de la `2` până la rădăcina pătrată a lui `i`. Dar totuși, dacă vrem să fie cu adevărat eficient pe intervale mari trebuie să schimbăm abordarea și să ne bazăm pe matematică avansată și pe algoritmi complexi ca [Quadratic sieve](https://en.wikipedia.org/wiki/Quadratic_sieve), [General number field sieve](https://en.wikipedia.org/wiki/General_number_field_sieve) etc.