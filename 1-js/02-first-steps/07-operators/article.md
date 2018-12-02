# Operatori

Mulți operatori ne sunt cunoscuți de la școală. Ei sunt adunarea `+`, înmulțirea `*`, scăderea `-` și așa mai departe.

În acest capitol ne concentrăm pe aspecte ce nu sunt acoperite de aritmetica din școală.

## Termenii: "unar", "binar", "operand"

Înainte de a merge mai departe să înțelegem terminologia comună.

- *Un operand* -- este ceea ce este aplicat operatorilor. De exemplu în înmulțirea `5 * 2` sunt doi operanzi: operandul stâng este `5`, iar cel drept este `2`. Câteodată lumea spune "argumente" în loc de "operanzi".
- Un operator este *unar* dacă are un singur operand. De exemplu, negația unară `-` inversează semnul numărului:

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, unary negation was applied
    ```
- Un operator este *binar* dacă are doi operanzi. Același minus există în format binar, de asemenea:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, binary minus subtracts values
    ```

    Formal, vorbim aici de doi operatori diferiți: negția unară (un singur operator, inversează semnul) și scăderea binară (doi operanzi, scădere).

## Concatenarea string-urilor, + binar

Acum, să vedem o caracteristică specială a operatorilor din JavaScript care sunt peste aritmetica din școală.

De obicei operatorul plus `+` adună două numere.

Dar dacă `+` este aplicat string-urilor, acesta le îmbină (concatenează):

```js
let s = "my" + "string";
alert(s); // mystring
```

Observă că dacă oricare dintre operanzi este string, atunci celălalt este convertit de asemenea la un string.

Spre exemplu:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Vezi, nu contează dacă primul operand sau al doilea operand este un string. Regula este simplă: dacă oricare dintre operanzi este string, atunci convertește-l pe celălalt într-un string.

Totuși, observă că operațiile execută de la stânga la dreapta. Dacă există două numere urmate de un string, numerele vor fi adunate înainte de a fi convertite la string:


```js run
alert(2 + 2 + '1' ); // "41" and not "221"
```

Concatenarea și conversia de string-uri este o caracteristică specială a binarului plus `+`. Alți operatori aritmetici lucrează doar cu numerele. Ei întotdeauna își convertesc operanzii la numere.

De exemplu, scăderea și împărțirea:

```js run
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

## Conversia numerică, + unar

Plusul `+` există în două forme. Forma binară pe care am folosit-o mai sus și forma unară.

Plusul unar sau, cu alte cuvinte, operatorul plus `+` aplicat unei singure valori, nu face nimic cu numerele, dar dacă operandul nu este un număr, atunci este convertit într-unul.

De exemplu:

```js run
// No effect on numbers
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Converts non-numbers
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Face defapt același lucru ca și `Number(...)`, dar este mai scurt.

Nevoia de a converti string-uri în numere se ivește deseori. Spre exemplu, dacă primim valori din câmpurile formularelor din HTML, atunci ele sunt string-uri obișnuite.

Ce se întâmplă dacă încercăm să le adunăm?

Plus-ul binar le-ar aduna ca și string-uri:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

Dacă vrem să le tratăm ca și numere, atunci le putem converti și apoi le adunăm:

```js run
let apples = "2";
let oranges = "3";

*!*
// both values converted to numbers before the binary plus
alert( +apples + +oranges ); // 5
*/!*

// the longer variant
// alert( Number(apples) + Number(oranges) ); // 5
```

Din punctul de vedere al unui matematician abundența plus-urilor ar putea părea ciudată. Dar din punctul de vedere al unui programator, nu este nimic special: plus-urile unare sunt aplicate primele, ele convertesc string-urile la numere, iar apoi plus-ul binar le adună.

De ce sunt aplicate plus-urile unare, valorilor, înainte de cele binare? După cum vom vedea, acest lucru se întâmplă din cauza *precedenței mai mari*.

## Precedența operatorilor

Dacă o expresie are mai mult de un operator ordinea execuției este definită de *precedența* lor, sau, cu alte cuvinte, exista o prioritate a ordinii implicită printre operatori.

Din școală știm cu toții că înmulțirea din expresia `1 + 2 * 2` ar trebui calculată înaintea sumei. Asta este exact precedența. Se spune că înmulțirea are *o procedență mai mare* decât suma.

Parantezele suprascriu orice precedență, așa că dacă nu suntem satisfăcuți cu ordinea le putem folosi, ca aici: `(1 + 2) * 2`.

Există mulți operatori în JavaScript. Fiecare operator are un număr de precedență, ce-i corespunde. Cel cu numărul mai mare execută primul. Dacă precedența este aceeași, ordinea execuției este de la stânga la dreapta.

Un extract din [tabelul de precedență](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence) (nu trebuie să ții minte asta, dar observă că operatorii unari sunt mai mari decât corespondenții lor binari):

| Precedență | Nume | Semn |
|------------|------|------|
| ... | ... | ... |
| 16 | plus unar | `+` |
| 16 | negație unară | `-` |
| 14 | înmulțire | `*` |
| 14 | împărțire | `/` |
| 13 | adunare | `+` |
| 13 | scădere | `-` |
| ... | ... | ... |
| 3 | asignare | `=` |
| ... | ... | ... |

După cum vedem, "plus-ul unar" are o prioritate de `16`, care este mai mare decât `13` pentru "sumă" (plus binar). De aceea în expresia `"+apples + +oranges"` plus-urile unare execută primele, iar apoi suma.

## Atribuire

Să observăm că o asignare `=` este de asemenea un operator. Este listat în tabelul de precedență cu prioritatea foarte mică de `3`.

De aceea atunci când asignăm o variabile, ca `x = 2 * 2 + 1`, calculele sunt realizate primele, și apoi `=` este evaluat, stocând rezultatul în `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

Este posibil să înlănțuim asignările:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Asignările înlănțuite sunt evaluate de la dreapta la stânga. În primul rând, expresia cea mai din dreapta `2 + 2` este evaluată și apoi asignată variabilelor din stânga: `c`, `b` și `a`. La sfârșit, toate variabilele împărtășesc o singurp valoare.

````smart header="The assignment operator `\"=\"` returns a value"
Un operator returnează întotdeauna o valoare. Asta este evident pentru majoritatea operatorilor ca adunarea `+` sau înmulțirea `*`. Dar operatorul de asignare folosește aceeași regulă.

Apelul `x = value` scrie valoarea `value` în `x` *și apoi o returnează*.

Aici este demo-ul care folosește o asignare ca și parte a unei expresii mai complexe:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

În exemplul de mai sus, rezultatul lui `(a = b + 1)` este valoarea care este atribuită lui `a` (care este `3`). Este folosit apoi pentru a scădea din `3`.

Amuzant cod, nu ? Ar trebui să înțelegem cum funcționează, pentru că uneori îl putem vedea în biblioteci 3rd-party, dar nu ar trebui să scriem așa ceva noi înșine. Astfel de trucuri cu siguranță nu fac codul mai curat și mai lizibil.
````

## Restul %

Operatorul rest `%` în ciuda aparenței sale nu are o relație cu procentele.

Rezultatul lui `a % b` este restul împărțirii întregi a lui `a` la `b`.

Spre exemplu:

```js run
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

## Exponențierea **

Operatorul de exponențiere `**` este o adiție recentă limbajului.

Pentru un număr natural `b` rezultatul lui `a ** b` este `a` înmulțit cu el însuși de `b` ori.

De exemplu:

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

Operatorul funcționează pentru numere non-întregi a lui `a` și `b` de asemenea, de exemplu:

```js run
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

## Incrementare/decrementare

<!-- Can't use -- in title, because built-in parse turns it into – -->

Adunând sau scăzând 1 dintr-un număr este una dintre cele mai comune operații numerice.

Așadar, există operatori speciali pentru acest lucru:

- **Incrementarea** `++` crește o variabile cu 1:

    ```js run no-beautify
    let counter = 2;
    counter++;      // works the same as counter = counter + 1, but is shorter
    alert( counter ); // 3
    ```
- **Decrementarea** `--` descrește o variabilă cu 1:

    ```js run no-beautify
    let counter = 2;
    counter--;      // works the same as counter = counter - 1, but is shorter
    alert( counter ); // 1
    ```

```warn
Incrementarea/decrementarea poate fi aplicată doar variabilelor. O încercare de a o folosi pe o valoare ca `5++` va da eroare.
```

Operatorii `++` și `--` pot fi așezați amândoi înainte sau după variabilă.

- Când operatorul este pus după variabilă, se numește "formă postfixată": `counter++`. 
- "Forma prefixată" este atunci când operatorul stă înaintea variabilei: `++counter`.

Ambele fac același lucru: cresc variabila `counter` cu `1`.  

Există vreo diferență? Da, dar o putem vedea doar dacă folosim valoare returnată de `++/--`.

Să clarificăm. După cum știm, toți operatorii returnează o valoare. Incrementarea/decrementarea nu este o excepție. Forma prefixată returnează valoarea nouă, în timp ce forma postfixată returnează valoarea veche (precedentă incrementării/decrementării).

Pentru a vedea diferența, aici este exemplul:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

Aici la linia `(*)` apelul prefixat `++counter` incrementează `counter` și returnează noua valoare care este `2`. Așa că `alert` afișează `2`.

Acum, să folosim forma postfixată:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

În linia `(*)` forma *postfixată* `counter++` incrementează de asemenea pe `counter`, dar returnează valoarea *veche* (înainte de incrementare). Așadar `alert` afișează `1`.

Pentru a rezuma:

- Dacă rezultatul incrementării/decrementării nu este folosit, atunci nu este nici o diferență cu privire la ce formă să fie folosită:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- Dacă am vrea să mărim valoarea *și* să folosim rezultatul operatorului chiar acum, atunci avem nevoie de forma prefixată:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- Dacă am vrea să incrementăm, dar să folosim valoarea precedentă, atunci avem nevoie de forma postfixată:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement among other operators"
Operatorii `++/--` pot fi folosiți în interiorul unei expresii de asemenea. Precedența lor este mai mare decât cea a majorității operatorilor aritmetici.

De exemplu:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compară cu:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Deși tehnic admisibil, asemenea notație de obicei face codul mai puțin citibil. O singură linie face lucruri multiple -- nu e bine.

Când citim codul, o scanare vizuală "verticală" poate cu ușurință să rateze un asemenea `counter++` și nu va fi evident că variabila se mărește.

Este sfătuit să se folosească stilul "o linie -- o acțiune":

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Operatorii pe biți

Operatorii pe biți tratează argumentele ca și numere întregi pe 32 de biți și lucrează  la nivelul reprezentării lor binare.

Acești operatori nu sunt specifici JavaScript-ului. Ei sunt suportați în majoritatea limbajelor de programare.

Lista operatorilor:

- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )


These operators are used very rarely. To understand them, we should delve into low-level number representation, and it would not be optimal to do that right now. Especially because we won't need them any time soon. If you're curious, you can read the [Bitwise Operators](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) article in MDN. It would be more practical to do that when a real need arises.

## Modify-in-place

We often need to apply an operator to a variable and store the new result in it.

For example:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

This notation can be shortened using operators `+=` and `*=`:

```js run
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Short "modify-and-assign" operators exist for all arithmetical and bitwise operators: `/=`, `-=` etc.

Such operators have the same precedence as a normal assignment, so they run after most other calculations:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

## Comma

The comma operator `,` is one of most rare and unusual operators. Sometimes it's used to write shorter code, so we need to know it in order to understand what's going on.

The comma operator allows us to evaluate several expressions, dividing them with a comma `,`. Each of them is evaluated, but the result of only the last one is returned.

For example:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (the result of 3 + 4)
```

Here, the first expression `1 + 2` is evaluated, and its result is thrown away, then `3 + 4` is evaluated and returned as the result.

```smart header="Comma has a very low precedence"
Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above.

Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns    `a = 3`, and then the number after the comma `7` is not processed anyhow, so it's ignored.
```

Why do we need such an operator which throws away everything except the last part?

Sometimes people use it in more complex constructs to put several actions in one line.

For example:

```js
// three operations in one line
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Such tricks are used in many JavaScript frameworks, that's why we mention them. But usually they don't improve the code readability, so we should think well before writing like that.
