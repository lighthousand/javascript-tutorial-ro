# Tipuri de date

O variabilă în JavaScript poate conține orice fel de date. O variabilă poate fi la un moment dat un string, iar mai târziu poate primi o valoare numerică:

```js
// no error
let message = "hello";
message = 123456;
```

Limbajele de programare care permit un astfel de lucru se numesc "tipizate dinamic" (dynamically typed), aceasta însemnând că există tipuri de date, dar variabilele nu sunt legate de nici unul dintre ele.

Există șapte tipuri de date de bază în JavaScript. Aici le vom studia pe cele de bază, iar în capitolele următoare vom vorbi despre ele, separat, în detaliu.

## Un număr

```js
let n = 123;
n = 12.345;
```

Tipul *number* servește atât ca întreg cât și ca număr real (floating point).

Există multe operații pentru numere, de exemplu înmulțirea `*`, împărțirea `/`, adunarea `+`, scăderea `-` și așa mai departe.

În afară de numerele obișnuite, mai există așa-numitele "valori numerice speciale" care aparțin de asemenea acelui tip: `Infinity`, `-Infinity` și `NaN`. 

- `Infinity` reprezintă [infinitul matematic](https://en.wikipedia.org/wiki/Infinity) ∞. Este o valoare specială care este mai mare decât orice alt număr.

    O putem obține ca și rezultat al împărțirii la zero:

    ```js run
    alert( 1 / 0 ); // Infinity
    ```

    Sau menționând-o direct, în cod:

    ```js run
    alert( Infinity ); // Infinity
    ```
- `NaN` reprezintă o eroare de procesare. Este rezultatul unei operații incorecte sau nedefinite, de exemplu:

    ```js run
    alert( "not a number" / 2 ); // NaN, such division is erroneous
    ```

    `NaN` este lipicios. Orice operație asupra lui `NaN` va da `NaN`:

    ```js run
    alert( "not a number" / 2 + 5 ); // NaN
    ```

    Așa că, dacă există `NaN` undeva într-o expresie matematică, se va propaga în întregul rezultat. 

```smart header="Mathematical operations are safe"
Calculul matematic este sigur în JavaScript. Putem face orice: împărțire la zero, tratarea de string-uri non-numerice ca și numere, etc.

Script-ul nu se va opri niciodată cu o eroare fatală ("moare"). În cel mai rău caz vom obține `NaN` ca și rezultat.
```

Valorile numerice speciale aparțin în mod formal tipului "number". Desigur ele nu sunt numere în adevăratul sens al cuvântului.

Vom vedea mai multe despre lucrul cu numere în capitolul <info:number>.

## Un string

Un string în JavaScript trebuie să fie între ghilimele.

```js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed ${str}`;
```

În JavaScript, există 3 tipuri de ghilimele.

1. Double quotes: `"Hello"`.
2. Single quotes: `'Hello'`.
3. Backticks: <code>&#96;Hello&#96;</code>.

Ghilimelele duble și apostroafele sunt "pur și simplu" ghilimele. Nu există nicio diferență între ele, în JavaScript.

Backtick-urile sunt ghilimele pentru "extindere a funcționalității". Ele ne permit să încorporăm variabile și expresii într-un string, învelindu-le în `${…}`, spre exemplu:

```js run
let name = "John";

// embed a variable
alert( `Hello, *!*${name}*/!*!` ); // Hello, John!

// embed an expression
alert( `the result is *!*${1 + 2}*/!*` ); // the result is 3
```

Expresia dinăuntrul `${…}` este evaluată, iar rezultatul devine parte din string. Putem pune orice acolo: o variabilă precum `name` sau o expresie aritmetică ca și `1 + 2` sau ceva mult mai complex.

Te rog observă ca acest lucru poate fi făcut doar cu backticks. Alte ghilimele nu permit astfel de încorporare!
```js run
alert( "the result is ${1 + 2}" ); // the result is ${1 + 2} (double quotes do nothing)
```

Vom acoperi string-urile mult mai detaliat în capitolul <info:string>.

```smart header="There is no *character* type."
În unele limbaje există un tip "character" special, pentru un singur caracter. De exemplu, în limbajul C și în Java acesta este `char`.

În JavaScript nu există un astfel de tip. Este prezent doar un singur tip: `string`. Un string poate fi format din doar un caracter sau din mai multe.
```

## Un boolean (tipul logic)

Tipul boolean are doar două valori: `true` (adevărat) și `false` (fals).

Acest tip este folosit de obicei pentru a stoca valorile da/nu (yes/no): `true` înseamnă "yes, correct", și `false` înseamnă "no, incorrect".

De exemplu:

```js
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked
```

Valorile booleene pot apărea ca și rezultat al comparărilor:

```js run
let isGreater = 4 > 1;

alert( isGreater ); // true (the comparison result is "yes")
```

Vom acoperi booleenele mai în profunzime, mai târziu, în capitolul <info:logical-operators>.

## Valoarea "null"

Valoarea specială `null` nu aparține niciunui tip din cele descrise mai sus.

Formează un tip separat numai al său, care conține doar valoarea `null`:

```js
let age = null;
```

În JavaScript `null` nu este o "referință către un obiect inexistent" sau un "pointer null" ca în alte limbaje.

Este doar o valoare specială care are înțelesul de "nimic", "gol" sau "valoare necunoscută".

Codul de mai sus afirmă că `age` este necunoscut sau gol dintr-un motiv anume.

## Valoarea "undefined"

Valoarea specială `undefined` este izolată. Își creează propriul său tip, la fel ca `null`.

Înțelesul lui `undefined` este "valoarea nu este atribuită".

Dacă o variabilă este declarată, dar nu este asignată, atunci valoarea acesteia este exact `undefined`:

```js run
let x;

alert(x); // shows "undefined"
```

Din punct de vedere tehnic este posibil să asignăm `undefined` oricărei variabile:

```js run
let x = 123;

x = undefined;

alert(x); // "undefined"
```

...Dar nu este recomandat să facem asta. În mod normal, vom folosi `null` pentru a scrie o valoare "goală" sau "necunoscută" într-o variabilă, și `undefined` este folosit doar pentru verificări, pentru a vedea dacă variabila este atribuită, sau asemăntor.

## Obiecte și simboluri

Tipul `object` este special.

Toate celelalte tipuri sunt numite "primitive", pentru că valorile lor pot conține doar un singur lucru (fie un string sau un număr sau orice altceva). În contrast, obiectele sunt folosite pentru a stoca colecții de date și entități mult mai complexe. Vom avea de aface cu ele mai târziu, în capitolul <info:object>, după ce aflăm mai multe despre primitive.

The `symbol` type is used to create unique identifiers for objects. We have to mention it here for completeness, but it's better to study them after objects.

## The typeof operator [#type-typeof]

The `typeof` operator returns the type of the argument. It's useful when we want to process values of different types differently, or just want to make a quick check.

It supports two forms of syntax:

1. As an operator: `typeof x`.
2. Function style: `typeof(x)`.

In other words, it works both with parentheses or without them. The result is the same.

The call to `typeof x` returns a string with the type name:

```js
typeof undefined // "undefined"

typeof 0 // "number"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

*!*
typeof Math // "object"  (1)
*/!*

*!*
typeof null // "object"  (2)
*/!*

*!*
typeof alert // "function"  (3)
*/!*
```

The last three lines may need additional explanations:

1. `Math` is a built-in object that provides mathematical operations. We will learn it in the chapter <info:number>. Here it serves just as an example of an object.
2. The result of `typeof null` is `"object"`. That's wrong. It is an officially recognized error in `typeof`, kept for compatibility. Of course, `null` is not an object. It is a special value with a separate type of its own. So, again, that's an error in the language.
3. The result of `typeof alert` is `"function"`, because `alert` is a function of the language. We'll study functions in the next chapters, and we'll see that there's no special "function" type in the language. Functions belong to the object type. But `typeof` treats them differently. Formally, it's incorrect, but very convenient in practice.


## Summary

There are 7 basic types in JavaScript.

- `number` for numbers of any kind: integer or floating-point.
- `string` for strings. A string may have one or more characters, there's no separate single-character type.
- `boolean` for `true`/`false`.
- `null` for unknown values -- a standalone type that has a single value `null`.
- `undefined` for unassigned values -- a standalone type that has a single value `undefined`.
- `object` for more complex data structures.
- `symbol` for unique identifiers.

The `typeof` operator allows us to see which type is stored in the variable.

- Two forms: `typeof x` or `typeof(x)`.
- Returns a string with the name of the type, like `"string"`.
- For `null` returns `"object"` -- that's an error in the language, it's not an object in fact.

In the next chapters we'll concentrate on primitive values and once we're familiar with them, then we'll move on to objects.
