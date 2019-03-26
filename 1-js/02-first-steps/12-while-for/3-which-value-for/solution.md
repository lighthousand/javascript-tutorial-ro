**Răspunsul: de la `0` la `4` în ambele cazuri.**

```js run
for (let i = 0; i < 5; ++i) alert( i );

for (let i = 0; i < 5; i++) alert( i );
```

Acest lucru poate fi dedus ușor din algoritmul lui `for`:

1. Execută odată `i = 0` înainte de orice altceva (început).
2. Verifică condiția `i < 5`
3. Dacă `true` -- execută corpul buclei `alert(i)` și apoi `i++`

Incrementarea `i++` este separată de condiția de verificare (2). Aceasta este doar o altă afirmație.

Valoarea returnată de incrementare nu este folosită aici, așadar nu există nicio diferentă între `i++` și `++i`.