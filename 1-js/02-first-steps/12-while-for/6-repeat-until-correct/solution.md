
```js run demo
let num;

do {
  num = prompt("Enter a number greater than 100?", 0);
} while (num <= 100 && num);
```

Bucla `do..while` se repetă atât timp cât ambele verificări sunt valide:

1. Verificarea `num <= 100` -- înseamnă atât timp cât valoarea introdusă nu este mai mare de `100`.
2. Verificarea `&& num` este falsă când `num` este `null` sau un string gol. Apoi bucla `while` se oprește de asemenea.

P.S. Dacă `num` este `null` atunci `num <= 100` este `true`, așadar fără cea de a doua verificare bucla nu se va opri dacă utilizatorul apasă CANCEL. Ambele validări sunt necesare.