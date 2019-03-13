Răspunsul: `3`.

```js run
alert( null || 2 && 3 || 4 );
```
Precedența lui AND `&&` este mai mare decât `||`, așa că execută primul.

Rezultatul este `2 && 3 = 3`, așa că expresia devine:

```
null || 3 || 4
```

Acum rezultatul este prima valoare truthy: `3`.