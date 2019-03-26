# Bucle: while și for

Adesea suntem obligați să îndeplinim acțiuni similare de mai multe ori la rând.

De exemplu, când avem nevoie să afișăm bunuri dintr-o listă, unul după altul. Sau doar să rulăm același cod pentru fiecare număr de la 1 la 10.

*Buclele* reprezintă o metodă de a repeta aceeași bucată de cod de multiple ori.

## Bucla "while"

Bucla `while` are următoarea sintaxă:

```js
while (condition) {
  // code
  // so-called "loop body"
}
```

Cât timp `condition` este `true`, `codul` dinăuntrul corpului buclei va fi executat.

Spre exemplu, bucla de mai jos afișează `i` cât timp `i < 3`:

```js run
let i = 0;
while (i < 3) { // shows 0, then 1, then 2
  alert( i );
  i++;
}
```

O singură execuție a corpului buclei este denumită *o iterație*. Bucla din exemplul de mai sus face 3 iterații.

Dacă nu ar fi fost niciun `i++` în exemplul de mai sus, bucla ar fi repetat (în teorie) la nesfârșit. În practică, browser-ul furnizează mijloace de a opri asemenea bucle, și pentru JavaScript server-side putem "omorî" procesul.

Orice expresie sau o variabile poate fi o condiție de buclă, nu doar o comparație. Ele sunt evaluate și convertite la un boolean de către `while`.

Spre exemplu, calea scurtă de a scrie `while (i != 0)` ar putea fi `while (i)`:

```js run
let i = 3;
*!*
while (i) { // when i becomes 0, the condition becomes falsy, and the loop stops
*/!*
  alert( i );
  i--;
}
```

````smart header="Brackets are not required for a single-line body"
Dacă corpul buclei are o singură afirmație, putem omite acoladele `{…}`:

```js run
let i = 3;
*!*
while (i) alert(i--);
*/!*
```
````

## Bucla "do..while"

Verificarea condiției poate fi mutat *mai jos*, corpul buclei folosind sintaxa `do..while`:

```js
do {
  // loop body
} while (condition);
```

Bucla va executa mai întâi corpul, apoi va verifica condiția și, cât timp este adevărată, va executa din nou și din nou.

Spre exemplu:

```js run
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

Această formă a sintaxei este rar utilizată, cu excepția cazului când vrei ca bucla să execute **cel puțin odată** fără a ține cont dacă condiția este adevărată sau nu. În mod normal cealaltă formă este preferată: `while(…) {…}`.

## Bucla "for"

Bucla `for` este cea mai des utilizată.

Arată astfel:

```js
for (begin; condition; step) {
  // ... loop body ...
}
```

Să înțelegem înțelesul acestor părți după exemplu. Bucla de mai jos va executa `alert(i)` pentru `i` de la `0` până la (dar nu inclusiv) `3`:

```js run
for (let i = 0; i < 3; i++) { // shows 0, then 1, then 2
  alert(i);
}
```

Să examinăm afirmația `for` bucată cu bucată:

| bucată   |            |                                                                                |
|----------|------------|--------------------------------------------------------------------------------|
| început  | `i = 0`    | Execută odată ce intră în buclă.                                               |
| condiție | `i < 3`    | Verificată înainte de fiecare iterație a buclei, dacă eșuează bucla se oprește.|
| pas      | `i++`      | Execută după corp la fiecare iterație, dar înainte de verificarea condiției.   |
| corp     | `alert(i)` | Execută din nou și din nou cât timp condiția este adevărată.                   |

Algoritmul ciclic general funcționează astfel:
```
Începe execuția
→ (dacă condiție → execută corp și execută pas)
→ (if condition → execută corp și execută pas)
→ (if condition → execută corp și execută pas)
→ ...
```

Dacă ești începător la capitolul bucle, atunci ar putea fi de folos dacă ai merge înapoi la exemplu și să reproduci execuția pas cu pas pe hârtie.

Iată ce se întâmplă cu adevărat în cazul nostru:

```js
// for (let i = 0; i < 3; i++) alert(i)

// run begin
let i = 0
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// ...finish, because now i == 3
```

````smart header="Inline variable declaration"
Aici variabila "contor" `i` este declarată chiar în buclă. Aceasta se numește o declarație de variabilă "inline". Astfel de variabile sunt visibile doar înăuntrul buclei.

```js run
for (*!*let*/!* i = 0; i < 3; i++) {
  alert(i); // 0, 1, 2
}
alert(i); // error, no such variable
```

În locul definirii unei variabile putem să folosim una deja existentă:

```js run
let i = 0;

for (i = 0; i < 3; i++) { // use an existing variable
  alert(i); // 0, 1, 2
}

alert(i); // 3, visible, because declared outside of the loop
```

````


### Trecerea peste părți

Orice parte a lui `for` poate fi sărită.

Spre exemplu, putem omite `begin` dacă nu este necesar să facem ceva la startul buclei.

Ca și aici:

```js run
let i = 0; // we have i already declared and assigned

for (; i < 3; i++) { // no need for "begin"
  alert( i ); // 0, 1, 2
}
```

Putem de asemenea înlătura partea `pas`:

```js run
let i = 0;

for (; i < 3;) {
  alert( i++ );
}
```

Bucla a devenit identică cu `while (i < 3)`.

Pute defapt să ștergem tot, astfel creând o buclă infinită:

```js
for (;;) {
  // repeats without limits
}
```

Te rog observă că cele 2 `;` ale `for-ului`trebuie să fie prezente, altfel ar creea o eroare de sintaxă.

## Ruperea buclei

În mod normal bucla iese când condiția devine falsă.

Dar putem forța ieșirea în orice moment. Există o directivă `break` special pentru acest lucru.

Spre exemplu, bucla de mai jos cere utilizatorului o secvență de numere, dar "întrerupe" atunci când nu este introdus un număr:

```js
let sum = 0;

while (true) {

  let value = +prompt("Enter a number", '');

*!*
  if (!value) break; // (*)
*/!*

  sum += value;

}
alert( 'Sum: ' + sum );
```

Directiva `break` este activată la linia `(*)` dacă utilizatorul introduce o linie goală sau anulează input-ul. Oprește bucla imediat, cedând controlul primei linii de după buclă. Adică, `alert`.

Combinația "buclă infinită + `break` după cum este cazul" este foarte bună în situații în care condiția trebuie să fie verificată nu la începutul/sfârșitul buclei, ci la mijloc, sau chiar în câteva locuri în corp.

## Continuă la următoarea iterație [#continue]

Directiva `continue` este o "versiune mai ușoară" a lui `break`. Nu oprește întreaga buclă. În loc de asta oprește iterația curentă și forțează bucla să pornească una nouă (dacă condiția îi permite).

O putem folosi dacă am terminat cu iterația curentă și vrem să trecem la următoarea.

Bucla de mai jos folosește `continue` pentru a afișa doar valori impare:

```js run no-beautify
for (let i = 0; i < 10; i++) {

  // if true, skip the remaining part of the body
  *!*if (i % 2 == 0) continue;*/!*

  alert(i); // 1, then 3, 5, 7, 9
}
```

Pentru valori pare ale lui `i` directiva `continue`oprește execuția corpului, cedând controlul iterației următoare din `for` (cu următorul număr). Așadar `alert` este apelat doar pentru valori impare.

````smart header="The directive `continue` helps to decrease nesting level"
O buclă care afișează valori impare poate arăta astfel:

```js
for (let i = 0; i < 10; i++) {

  if (i % 2) {
    alert( i );
  }

}
```

Dintr-un punct de vedere tehnic este identic cu exemplul de mai sus. Cu siguranță putem înconjura codul în blocul `if` în loc de `continue`.

Dar ca și efect secundar am creeat încă un nivel de imbricare (apelul lui `alert` dinăuntrul acoladelor). Dacă codul dinăuntrul lui `if` este mai mare de câteva linii, acest lucru ar putea descrește lizibilitatea în general.
````

````warn header="No `break/continue` to the right side of '?'"
Te rog, observă că construcțiile sintactice care nu sunt expresii nu pot fi folosite împreună cu operatorul ternar `?`. În mod special, directivele precum `break/continue` nu sunt permise aici.

De exemplu, dacă ne uităm peste acest cod:

```js
if (i > 5) {
  alert(i);
} else {
  continue;
}
```

...Și-l rescriem folosind semnul întrebării:


```js no-beautify
(i > 5) ? alert(i) : *!*continue*/!*; // continue not allowed here
```

...Apoi nu mai funcționează. Acest fel de cod va da eroare de sintaxă:


Acesta este doar un alt motiv împotriva folosirii operatorului ternar `?` în loc de `if`.
````

## Etichete pentru break/continue

Câteodată avem nevoie să ieșim din bucle multiple, îmbricate, deodată.

Spre exemplu, în codul de mai jos ciclăm peste `i` și `j` afișând cordonatele `(i, j)` de la `(0,0)` la `(3,3)`:

```js run no-beautify
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // what if I want to exit from here to Done (below)?

  }
}

alert('Done!');
```

Avem nevoie de o modalitate de a opri procesul dacă utilizatorul anulează inputul.

`break-ul` normal, după `input` ar ieși doar din bucla internă. Acesta nu este suficient. Etichetele vin în ajutor.

O *Etichetă* este un identificatpr cu două puncte, înainte de o buclă:
```js
labelName: for (...) {
  ...
}
```

Afirmația `break <labelName>` din buclă iese unde este eticheta.

Ca și aici:

```js run no-beautify
*!*outer:*/!* for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // if an empty string or canceled, then break out of both loops
    if (!input) *!*break outer*/!*; // (*)

    // do something with the value...
  }
}
alert('Done!');
```

În codul de mai sus `break outer` se uită după eticheta de mai sus, denumită `outer` și iese din buclă.

Așadar controlul merge direct de la `(*)` la `alert('Done!')`.

Putem de asemenea să mutăm eticheta pe o linie separată:

```js no-beautify
outer:
for (let i = 0; i < 3; i++) { ... }
```

Directiva `continue` poate fi de asemenea folosită cu o etichetă. În acest caz execuția sare la următoarea iterație buclei etichetate.

````warn header="Labels are not a \"goto\""
Etichetele nu ne permit să sărim într-o parte arbitrară a codului.

Spre exemplu, este imposibil să facem asta:
```js
break label;  // jumps to label? No.

label: for (...)
```

Apelul la `break/continue` este posibil doar dinăuntrul buclei, iar eticheta trebuie să fie undeva mai sus de directivă.
````

## Rezumat

Am acoperit 3 tipuri de bucle:

- `while` -- Condiția este verificată înainte de fiecare iterație.
- `do..while` -- Condiția este verificată după fiecare iterație.
- `for (;;)` -- Condiția este verificată înainte de fiecare iterație, setări adiționale sunt disponibile.

Pentru a face o buclă "infinită", deobicei este folosită construcția `while(true)`. O astfel de buclă, la fel ca oricare alta, poate fi oprită cu o directivă `break`.

Dacă nu vrem să facem nimic în iterația curentă și am dori să trecem la linia următoare, directiva `continue` ne va ajuta să realizăm acest lucru.

`break/continue` sprijină etichetele de dinainte de buclă. O etichetă este singura cale pentru a ieși, scăpa de îmbricare și să ajungem la bucla exterioară.