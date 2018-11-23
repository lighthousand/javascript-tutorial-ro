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

Tipul `symbol` este folosit pentru a creea identificatori unici pentru obiecte. Trebuie să menționăm aici pentru completitudine, dar este mai bine să le studiezi după obiecte. 

## Operatorul typeof [#type-typeof]

Operatorul `typeof` returnează tipul argumentului. Este folositor atunci când vrem să procesăm valori de tipuri diferite, în mod diferit, sau doar vrem să facem o verificare rapidă.

Suportă două forme de sintaxă:

1. Ca și operator: `typeof x`.
2. Ca funcție: `typeof(x)`.

Cu alte cuvinte funcționează cu sau fără paranteze. Rezultatul este același.

Apelul lui `typeof x` returnează un string cu numele tipului:

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

Ultimele trei linii ar putea avea nevoie de explicații adiționale:

1. `Math` este un obiect built-in (încorporat) care furnizează operații matematice. Îl vom învăța în capitolul <info:number>. Aici servește doar ca și exemplu de obiect.
2. Rezultatul lui `typeof null` este `"object"`. Ceea ce este greșit. Este o eroare recunoscută oficial a lui `typeof`, păstrată pentru compatibilitate. Desigur, `null` nu este un obiect. Este o valoare specială cu un tip separat al său. Așadar, din nou, Aceasta este o eroare a limbajului.
3. Rezultatul lui `typeof alert` este `"function"`, pentru că `alert` este o funcție a limbajului. Vom studia funcțiile în capitolul următor și vom vedea că nu există nici o funcție specială pe nume "function", în limbaj. Funcțiile aparțin tipului obiect. Dar `typeof` le tratează în mod diferit. Din punct de vedere formal este incorect, dar este foarte convenabil în practică.


## Rezumat

Există 7 tipuri de bază în JavaScrit.

- `number` pentru numere de orice gen: întregi sau reale.
- `string` pentru string-uri. Un string poate avea unul sau mai multe caractere, nu există niciun tip separat pentru un singur caracter.
- `boolean` pentru `true`/`false`.
- `null` pentru valori necunoscute -- un tip de sine stătător, care are o singură valoare, `null`.
- `undefined` pentru valori neasignate -- un tip de sine stătător care are o singură valoare, `undefined`.
- `object` pentru structuri de date mai complexe.
- `symbol` pentru identificatori unici.

Operatorul `typeof` ne permite să vedem ce tip este stocat în variabilă.

- Două forme: `typeof x` sau `typeof(x)`. 
- Returnează un string cu numele tipului, precum `"string"`.
- Pentru `null` returnează `"object"` -- aceasta este o eroare în limbaj, nu este un obiect, defapt.

În următoarele capitole ne vom concentra pe valorile primitive și odată ce suntem familiarizați cu ele, vom trece la obiecte.