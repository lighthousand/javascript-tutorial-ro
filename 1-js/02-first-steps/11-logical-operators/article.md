# Operatori logici

Există 3 operatori logici în JavaScript: `||` (OR), `&&` (AND), `!` (NOT).

Deși sunt denumiți "logici", aceștia pot fi aplicați oricărui tip de valori, nu numai booleene. Resultatul poate fi de asemenea de orice tip.

Să vedem detaliile.

## || (OR)

Operatorul "OR" este reprezentat cu două linii verticale:

```js
result = a || b;
```

În programarea clasică OR-ul logic este folosit pentru a manipula doar valori booleene. Dacă oricare dintre argumentele lui este `true`, atunci returnează `true`, altfel returnează `false`.

În JavaScript operatorul este un pic mai complicat și mai puternic. Dar mai întâi să observăm ce se întâmplă cu valorile booleene.

Există 4 combinații logice posibile:

```js run
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```

După cum putem vedea, rezultatul este întotdeauna `true`, cu excepția cazului când ambii operanzi sunt `false`.

Dacă un operator nu este boolean, atunci este convertit la un boolean pentru a fi evaluat.

Spre exemplu, un număr `1` este tratat ca și `true`, un număr `0` ca și `false`:

```js run
if (1 || 0) { // works just like if( true || false )
  alert( 'truthy!' );
}
```

În majoritatea timpului OR `||` este folosit într-o frază `if` pentru a testa dacă *oricare* dintre condițiile date este corectă.

De exemplu:

```js run
let hour = 9;

*!*
if (hour < 10 || hour > 18) {
*/!*
  alert( 'The office is closed.' );
}
```

Putem da mai multe condiții:

```js run
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'The office is closed.' ); // it is the weekend
}
```

## OR caută prima valoare truthy

Logica descrisă mai sus este oarecum clasică. Acum să aducem și capacitățile "extra" ale JavaScript-ului.

Algoritmul extins functionează după cum urmează.

Dându-se valori OR multiple:

```js
result = value1 || value2 || value3;
```

Operatorul OR `||` face următoarele:

- Evaluează operanzii de la stânga la dreapta.
- Pentru fiecare operand, face conversie la boolean. Dacă rezultatul este `true`, atunci se oprește și returnează valoarea originală a operandului.
- Dacă toți ceilalți operanzi au fost evaluați (cu alte cuvinte toți au fost `false`), returnează ultimul operand.

O valoare este returnată în forma sa originală, fără realizarea conversiei.

Cu alte cuvine, un lanț de OR `"||"` returnează prima valoare truthy sau ultima dacă o astfel de valoare nu este găsită.

Spre exemplu:

```js run
alert( 1 || 0 ); // 1 (1 is truthy)
alert( true || 'no matter what' ); // (true is truthy)

alert( null || 1 ); // 1 (1 is the first truthy value)
alert( null || 0 || 1 ); // 1 (the first truthy value)
alert( undefined || null || 0 ); // 0 (all falsy, returns the last value)
```

Acest lucru duce la utilizări interesante în comparație cu un "OR clasic, pur boolean".

1. **Luarea primei valori truthy din lista de variabile sau expresii.**

    Imaginează-ți că avem câteva variabile, care pot conține date sau să fie `null/undefined`. Și trebuie să alegem pe prima care conține date.

    Putem folosi OR `||` pentru acest lucru:

    ```js run
    let currentUser = null;
    let defaultUser = "John";

    *!*
    let name = currentUser || defaultUser || "unnamed";
    */!*

    alert( name ); // selects "John" – the first truthy value
    ```

    Dacă ambii `currentUser` și `defaultUser` erau falsy atunci rezultatul ar fi fost `"unnamed"`.
2. **Evaluare scurt-circuitată.**

    Operanzii pot fi nu numai valori, ci și expresii arbitrare. OR evaluează și testează de la stânga spre dreapta. Evaluarea se oprește când se ajunge la o valoare truthy, iar aceasta este apoi returnată. Procesul se numește "evaluare scurt-circuitată" pentru merge cât de puțin (scurt) posibil de la stânga la dreapta.

    Acest lucru se vede clar când expresia dată pe post de al doilea argument are un efect secundar. Precum o asignare de variabilă.

    Dacă rulăm exemplul de mai jos, lui `x` nu i s-ar mai asigna:

    ```js run no-beautify
    let x;

    *!*true*/!* || (x = 1);

    alert(x); // undefined, because (x = 1) not evaluated
    ```

    ...Și dacă primul argument este `false`, atunci `OR` continuă și îl evaluează pe cel de al doilea astfel executând asignarea:

    ```js run no-beautify
    let x;

    *!*false*/!* || (x = 1);

    alert(x); // 1
    ```

    O asignare este un caz simplu, alte efecte adverse pot fi implicate.

    După cum putem vedea, un astfel de context de utilizare este "o modalitate mai scurtă pentru a face `if`". Primul operand este convertit la boolean și dacă este fals atunci cel de al doilea este evaluat.

    În majoritatea timpului este mai bine să folosim un `if` "normal" pentru a face codul mai inteligibil, dar uneori acest lucru este util.

## && (AND)

Operatorul AND este reprezentat de 2 simboluri ampersand `&&`:

```js
result = a && b;
```

În programarea clasică AND returnează `true` dacă ambii operanzi sunt truthy și `false` în caz contrar:

```js run
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

Un exemplu cu `if`:

```js run
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
  alert( 'Time is 12:30' );
}
```
La fel ca și pentru OR, orice valoare este permisă ca și un operand al lui AND:

```js run
if (1 && 0) { // evaluated as true && false
  alert( "won't work, because the result is falsy" );
}
```

## AND caută prima valoare falsy

Fiind date mai multe valori AND:

```js
result = value1 && value2 && value3;
```

Operatorul AND `&&` face următoarele:

- Evaluează operanzii de la stânga la dreapta.
- Pentru fiecare operand, îl convertește la boolean. Dacă rezultatul este `false`, se oprește și returnează valoare originală a acelui operand.
- Dacă toți ceilalți operanzi au fost evaluați (cu alte cuvinte dacă toți sunt truthy), returnează ultimul operand.

Altfel spus AND returnează prima valoare falsy sau ultima valoare dacă niciuna nu a fost găsită.

Regulile de mai sus sunt similare cu OR. Diferența este că AND returnează prima valoare *falsy* cât timp OR returnează prima valoare *truthy*.

Exemple:

```js run
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

Putem de asemenea transmite câteva valori consecutive. Vezi cum este returnată prima valoare falsy:

```js run
alert( 1 && 2 && null && 3 ); // null
```

Când toate valoriile sunt truthy, este returnată ultima valoare:

```js run
alert( 1 && 2 && 3 ); // 3, the last one
```

````smart header="Precedence of AND `&&` is higher than OR `||`"
Precedența operatorului AND `&&` este mai mare decât cea a lui OR `||`.

Așadar codul `a && b || c && d` este în esență același ca și cum `&&` ar fi între paranteze: `(a && b) || (c && d)`.
````

La fel ca OR, operatorul AND `&&` poate fi înlocuit uneori de către `if`.

Spre exemplu:

```js run
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

Acțiunea din partea dreaptă a lui `&&` ar executa doar dacă evaluarea va ajunge acolo. Asta se întâmplă doar dacă `(x > 0)` este adevărat.

Astfel avem ceva analog pentru:

```js run
let x = 1;

if (x > 0) {
  alert( 'Greater than zero!' );
}
```

Varianta cu `&&` pare să fie mai scurtă. Dar `if` este mai evident și tinde să fie un pic mai lizibil.

Așadar este recomandat să folosim fiecare construcție pentru scopul ei. Folosim `if` dacă dorim if. Și folosim `&&` dacă dorim AND:

## ! (NOT)

Operatorul boolean NOT este reprezentat cu un semn al exclamării `!`.

Sintaxa este destul de simplă:

```js
result = !value;
```

Operatorul acceptă un singur argument și face următoarele:

1. Convertește operandul la tipul boolean: `true/false`.
2. Returnează o valoare inversă.

Spre exemplu:

```js run
alert( !true ); // false
alert( !0 ); // true
```

Un NOT `!!` dublu este folosit câteodată pentru a converti o valoare către tipul boolean:

```js run
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

Asta înseamnă că primul NOT convertește valoarea la boolean și returnează inversul, și al doilea NOT îl inversează din nou. La sfârșit avem o conversie valoare-la-boolean.

Există o formă mai detaliată de a face același lucru -- o funcție built-in, `Boolean`:

```js run
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```

Precedența lui NOT `!` este cea mai mare dintre toți operatorii logici, așa că va executa întotdeauna primul, înainte de  orice `&&`, `||`.