Răspunsul: `1`, și apoi `undefined`.

```js run
alert( alert(1) && alert(2) );
```

Apelul lui `alert` returnează `undefined` (doar afișează un mesaj, așa că nu este un return semnificativ).

Din această cauză `&&` evaluează operandul stâng (returnează `1`) și apoi se oprește imediat, pentru că `undefined` este o valoare falsy. Iar `&&` caută o valoare falsy și o returnează, și gata.