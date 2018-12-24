# Operatorii condiționali: if, '?'

Câteodată avem nevoie să realizăm diferite acțiuni bazate pe o condiție.

Pentru acest lucru există afirmația `if` și de asemenea operatorul condițional (ternar) pentru evaluarea condițională la care ne vom referi ca și operatorul "semnul întrebării" `?`, pentru simplitate.

## Afirmația "if"

Afirmația `if` primește o condiție, o evaluează și dacă rezultatul este `true`, atunci va executa codul.

De exemplu:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

*!*
if (year == 2015) alert( 'You are right!' );
*/!*
```

În exemplul de mai sus condiția este o simplă verificare de egalitate: `year == 2015`, dar poate fi mult mai complexă.

Dacă există mai mult de o afirmație care să fie executată, trebuie să înconjurăm blocul de cod în acolade:

```js
if (year == 2015) {
  alert( "That's correct!" );
  alert( "You're so smart!" );
}
```

Este recomandat să înconjori blocul de cod cu acolade `{}` de fiecare dată când folosești `if`, chiar dacă este ai doar o singură afirmație. Acest lucru îmbunătățește lizibilitatea.

## Conversie booleană

Afirmația `if (…)` evaluează expresia din paranteze și o convertește la tipul boolean.

Să ne aducem aminte de regulile de conversie din capitolul <info:type-conversions>:

- Un număr `0`, un string gol `""`, `null`, `undefined` și `NaN` devin `false`. Din această cauză ele sunt denumite valori "falsy"
- Alte valori devin `true`, așadar sunt denumite "truthy".

Deci, codul din acestă condiție nu va fi executat niciodată:

```js
if (0) { // 0 is falsy
  ...
}
```

...Și înăuntrul acestei condiții -- întotdeauna merge:

```js
if (1) { // 1 is truthy
  ...
}
```

Putem transmite o valoare booleană pre-evaluată către `if`, ca și aici:

```js
let cond = (year == 2015); // equality evaluates to true or false

if (cond) {
  ...
}
```

## Clauza "else"

Afirmația `if` poate conține un bloc "else" opțional. Acesta execută când condiția este greșită.

Spre exemplu:
```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' ); // any value except 2015
}
```

## Câteva condiții: "else if"

Câteodată am vrea să testăm câteva variante ale unei condiții. Există o clauză `else if` pentru acest lucru.

De exemplu:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

În codul de deasupra JavaScript verifică mai întâi `year < 2015`. Dacă este falsy atunci merge către următoarea condiție `year > 2015`, altfel afișează ultimul `alert`.

Pot fi mai multe blocuri `else if`. Terminația `else` este opțională.

## Operatorul ternar '?'

Uneori trebui să atribuim o variabilă în funcție de o condiție.

Spre exemplu:

```js run no-beautify
let accessAllowed;
let age = prompt('How old are you?', '');

*!*
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
*/!*

alert(accessAllowed);
```

Așa numitul operator "ternar" sau "semnul întrebării" ne permite să facem acest lucru într-un mod mai scurt și mai simplu.

Operatorul este reprezentat de către semnul întrebării `?`. Termenul formal "ternar" înseamnă că operatorul are 3 operanzi. Este defapt singurul operator din JavaScript care are atât de mulți.

Sintaxa este:
```js
let result = condition ? value1 : value2
```

`Condiția` este evaluată, dacă este truthy atunci este returnat `value1`, aștfel -- `value2`.

De exemplu:

```js
let accessAllowed = (age > 18) ? true : false;
```

Din punct de vedere tehnic putem omite parantezele dimprejurul `age > 18`. Operatorul semnul întrebării marchează o precedență scăzută. Aceasta execută după comparația `>`, așa că va face același lucru:

```js
// the comparison operator "age > 18" executes first anyway
// (no need to wrap it into parentheses)
let accessAllowed = age > 18 ? true : false;
```

Dar parantezele fac codul mult mai citibil, așa că este recomandat să fie folosite.

````smart
In the example above it's possible to evade the question mark operator, because the comparison by itself returns `true/false`:

```js
// the same
let accessAllowed = age > 18;
```
````

## '?' multiplii

O secvență de operatori `?` permit returnarea unei valori care depinde de mai mult de o condiție.

Spre exemplu:
```js run
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

La început poate fi dificil să înțelegi ce se întâmplă. Dar după o privire mai atentă putem vedea că este doar o secvență de teste obișnuită.

1. Primul semn de întrebare verifică dacă `age < 3`.
2. Dacă este true -- returnează `'Hi, baby!'`, altfel -- merge după `":"` și verifică dacă `age < 18`.
3. Dacă aceasta este true -- returnează `'Hello!'`, altfel -- merge la următoarele `":"` și verifică dacă `age < 100`.
4. Dacă acest lucru este true -- returnează `'Greetings!'`, altfel -- merge după ultimele `":"` și returnează `'What an unusual age!'`.

Aceeași logică folosind `if..else`:

```js
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

## Folosirea lui '?' non-tradițională

Uneori semnul întrebării `?` este folosit ca și înlocuitpr pentru `if`:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
*/!*
```

În funcție de condiția `company == 'Netscape'`, fie prima sau cea de a doua parte de după `?` este executată și afișează alert-ul.

Nu asignăm un rezultat unei variabile, aici. Ideea este să executăm cod diferit în funcție de condiție.

**Nu este recomandat să folosim operatorul semnul întrebării în acest fel.**

Notația pare a fi mai scurtă decât `if`, ceea ce atrage pe unii programatori. Dar este mai puțin citibil.

Aici avem același cod cu `if` pentru comparație:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
if (company == 'Netscape') {
  alert('Right!');
} else {
  alert('Wrong.');
}
*/!*
```

Ochii noștri pot scana codul, vertical. Construcțiile ce se întind pe mai multe linii sunt mai ușor de înțeles decât un set de instrucțiuni orizontal, lung.

Ideea semnului întrebării `?` este de a returna una sau altă valoare în funcție de codiție. Te rog folosește-l doar pentru acest lucru. Există `if` pentru a executa diferite ramuri ale codului.