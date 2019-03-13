Răspunsul: prima dată `1`, apoi `2`.

```js run
alert( alert(1) || 2 || alert(3) );
```

Apelul lui `alert` nu returnează o valoare. Sau, cu alte cuvinte, returnează `undefined`. 

1. Primul OR `||` evaluează operandul său din stânga `alert(1)`. Aceasta arată primul mesaj cu `1`.
2. `alert` returnează `undefined`, așadar OR merge către cel de al doilea operand și se uită după o valoare truthy.
3. Al doilea operator `2` este truthy, așa că execuția este oprită, se returnează `2` și apoi este afișat de alert-ul din afară.

Nu va exista niciun `3`, pentru că evaluarea nu ajunge la `alert(3)`.