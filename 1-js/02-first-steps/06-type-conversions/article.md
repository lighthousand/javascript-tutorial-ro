# Converisa de tipuri

În majoritatea timpului operatorii și funcțiile convertesc automat o valoare, la tipul potrivit. Aceasta se numește "conversie de tip".

De exemplu, `alert` convertește automat orice valoare la string, iar apoi o afișează. Operațiile matematice convertesc valori la numere.

Există de asemenea cazuri în care avem nevoie să convertim în mod explicit o valoare pentru a pune lucrurile în ordine.

```smart header="Not talking about objects yet"
În acest capitol nu discutăm deocamdată obiectele. Aici vom studia mai întâi primitivele. Mai târziu, după ce vom învăța obiectele, vom vedea cum funcționează conversia obiectelor, în capitolul <info:object-toprimitive>.
```

## ToString

Conversia de string are loc atunci când avem nevoie de forma string-ului unei valori.

Spre exemplu, `alert(value)` face conversie pentru a afișa valoarea.

Putem de asemenea să folosim un apel de funcție `String(value)` pentru aceasta:

```js run
let value = true;
alert(typeof value); // boolean

*!*
value = String(value); // now value is a string "true"
alert(typeof value); // string
*/!*
```

Conversia de string este în mare parte evidentă. Un `false` devine `"false"`, `null` devine `"null"` etc.

## ToNumber

Conversia numerică are loc în funcțiile matematice și expresiile automate.

De exemplu, când împărțirea `/` este aplicată non-numerelor:

```js run
alert( "6" / "2" ); // 3, strings are converted to numbers
```

Putem folosi o funcție `Number(value)` pentru a converti explicit o `valoare`:

```js run
let str = "123";
alert(typeof str); // string

let num = Number(str); // becomes a number 123

alert(typeof num); // number
```

Conversia explicită este de obicei necesară când citim o valoare dintr-o sursă bazată pe string cum ar fi un formular text, dar ne așteptăm să fie introdus un număr.

Dacă string-ul nu este un număr valid rezultatul unei astfel de conversii este `NaN`, spre exemplu:

```js run
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN, conversion failed
```

Regulile conversiei numerice:

| Valoarea |  Devine... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;and&nbsp;false</code> | `1` and `0` |
| `string` | Spațiile albe de la început și de la sfârșit sunt șterse. Apoi dacă string-ul rămas este gol rezultatul este `0`. Altfel numărul este "citit" din string. O eroare ar putea da `NaN`. |

Exemple:

```js run
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN (error reading a number at "z")
alert( Number(true) );        // 1
alert( Number(false) );       // 0
```

Te rog observă că `null` și `undefined` se comportă diferit aici: `null` devine un zero, în timp ce `undefined` devine `NaN`.

````smart header="Addition '+' concatenates strings"
Aproape toate operațiile matematice convertesc valorile în numere. Cu o excepție notabilă a adunării `+`. Dacă una dintre valorile adunate este string, atunci cealaltă este de asemenea convertită la string.

Apoi le concatenează (join):

```js run
alert( 1 + '2' ); // '12' (string to the right)
alert( '1' + 2 ); // '12' (string to the left)
```

Acest lucru se întâmplă doar când cel puțin unul dintre argumente este string. Altfel valorile sunt convertite la numere.
````

## ToBoolean

Conversia booleană este cea mai simplă.

Are loc în operațiile logice (mai târziu vom întâlni teste de condiție și altele asemenea), dar de asemenea pot fi realizate manual cu apelul lui `Boolean(value)`. 

Regula conversiei:

- Valori care sunt "goale" intuitiv, ca `0`, un string gol, `null`, `undefined` și `NaN` devin `false`.
- Alte valori devin `true`.

Spre exemplu:

```js run
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false

alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
```

````warn header="Please note: the string with zero `\"0\"` is `true`"
Unele limbaje (cu precădere PHP) tratează `"0"` ca și `false`. Dar în JavaScript un string non-empty este întotdeauna `true`.

```js run
alert( Boolean("0") ); // true
alert( Boolean(" ") ); // spaces, also true (any non-empty string is true)
```
````


## Rezumat

Există trei tipuri de conversie care sunt cel mai des folosite: to string, to number și to boolean.

**`ToString`** -- Apare atunci când returnăm ceva, poate fi realizată cu `String(value)`. Conversia la string este de obicei evidentă pentru valorile primitive.

**`ToNumber`** -- Apare în operațiile matematice, poate fi realizată cu `Number(value)`.

Conversia urmează următoarele reguli:

| Valoarea |  Devine... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;/&nbsp;false</code> | `1 / 0` |
| `string` | String-ul este citit ca "așa cum este", spațiile albe din ambele părți sunt ignorate. Un string gol devine `0`. O eroare ar putea da `NaN`. |

**`ToBoolean`** -- Apare în operațiile logice sau poate fi realizată cu `Boolean(value)`.

Urmează regulile:

| Valoarea |  Devine... |
|-------|-------------|
|`0`, `null`, `undefined`, `NaN`, `""` |`false`|
|orice altă valoare| `true` |


Majoritatea acestor reguli sunt ușor de înțeles și de memorat. Excepțiile remarcabile, când lumea greșește adesea sunt:

- `undefined` este `NaN` ca și un număr, nu `0`.
- `"0"` și string-urile space-only ca `"   "` sunt adevărate ca și boolean.

Obiectele nu sunt discutate aici, ne vom reîntoarce la ele mai târziu, în capitolul <info:object-toprimitive>, care este dedicat exclusiv obiectelor, după ce învățăm mai multe lucruri de bază ale JavaScript-ului.