# Variabile

În majoritatea timpului, o aplicație JavaScript trebuie să lucreze cu informații. Iată aici 2 exemple:
1. Un magazin online -- informațiile ar putea include produse ce sunt de vânzare și un coș de cumpărături.
2. O aplicație chat -- informațiile ar putea include utilizatori, mesaje și mult mai multe.

Variabilele sunt folosite pentru a stoca informații.

## O variabilă

O [variabilă](https://en.wikipedia.org/wiki/Variable_(computer_science)) este un "depozit cu nume" pentru date. Putem folosi variabile pentru a stoca bunuri, vizitatori și alte date.

Pentru a creea o variabilă în JavaScript trebuie să folosim cuvântul cheie `let`.

Afirmația de mai jos creează (cu alte cuvinte: *declară* sau *definește*) o variabilă cu numele "message":

```js
let message;
```

Acum putem pune ceva date în ea folosind operatorul de asignare (atribuire) `=`:

```js
let message;

*!*
message = 'Hello'; // store the string
*/!*
```
String-ul este acum salvat în zona de memorie asociată cu variabila. O putem accesa folosind numele variabilei:

```js run
let message;
message = 'Hello!';

*!*
alert(message); // shows the variable content
*/!*
```

Pentru a fi preciși putem îmbina declarațiile și asignările variabilelor într-o singură linie:

```js run
let message = 'Hello!'; // define the variable and assign the value

alert(message); // Hello!
```

Putem de asemenea declara variabile multiple pe o singură linie:

```js no-beautify
let user = 'John', age = 25, message = 'Hello';
```

Asta ar putea părea scurt, dar nu este neapărat recomandat. De dragul lizibilității mai mari, te rog folosește o singurp linie per variabilă.

Varianta multilinie este un pic mai lungă, dar mai ușor de citit:

```js
let user = 'John';
let age = 25;
let message = 'Hello';
```

Unele persoane de asemenea scriu multe dintre variabile în acest mod:
```js no-beautify
let user = 'John',
  age = 25,
  message = 'Hello';
```

...Sau chiar în stilul "comma-first" (virgula prima):

```js no-beautify
let user = 'John'
  , age = 25
  , message = 'Hello';
```

Din punct de vedere tehnic toate aceste variante fac același lucru. Așadar este o problemă de gust sau estetică.


````smart header="`var` instead of `let`"
În script-uri mai vechi poți găsi un alt cuvânt cheie: `var` în loc de `let`:

```js
*!*var*/!* message = 'Hello';
```

Cuvântul cheie `var` este *aproape* la fel ca `let`. Declară de asemenea o variabilă, dar într-o manieră "old-school", puțin diferită.

Există diferențe subtile între `let` și `var`, dar ele nu contează pentru noi, încă. Le vom discuta în detaliu, mai târziu, în capitolul <info:var>.
````

## O analogie din lumea reală

Putem să înțelegem cu ușurință  conceptul de unei "variabile" dacă ne-o imaginăm ca și o "cutie" pentru date, cu un sticker, denumit unic, pe ea.

De exemplu, variabila `message` poate fi imaginată ca o cutie etichetată cu `"message"`, cu valoarea `"Hello!"` înăuntrul ei:

![](variable.png)

Putem pune orice valoare în cutie.

De asemenea o putem schimba. Valoarea poate fi schimbată de câte ori este nevoie:

```js run
let message;

message = 'Hello!';

message = 'World!'; // value changed

alert(message);
```

Când valoarea este schimbată, vechile date sunt șterse din variabilă:

![](variable-change.png)

Putem de asemenea declara două variabile și putem copia datele dintr-una într-alta.

```js run
let hello = 'Hello world!';

let message;

*!*
// copy 'Hello world' from hello into message
message = hello;
*/!*

// now two variables hold the same data
alert(hello); // Hello world!
alert(message); // Hello world!
```

```smart header="Functional languages"
Poate părea interesant să știi că există limbaje de programare [funcționale](https://en.wikipedia.org/wiki/Functional_programming) care interzic schimbarea valorii unei variabile. De exemplu, [Scala](http://www.scala-lang.org/) sau [Erlang](http://www.erlang.org/).

În astfel de limbaje, odată ce valoarea a fost stocată "în cutie" este acolo pentru totdeauna. Dacă trebuie să stocăm altceva, limbajul ne forțează să creăm o cutie nouă (declarăm o nouă variabilă). Nu o putem folosi pe cea veche.

Deși ar putea părea puțin ciudat la prima vedere, aceste limbaje sunt destul de capabile de development serios. Mai mult decât atât, există zone precum procesare paralelă unde această limitație conferă anumite beneficii. Studierea unui astfel de limbaj (chiar dacă nu este planifict a fi folosit în curând) este recomandat pentru a mări orizonturile.
```

## Denumirea variabilelor [#variable-naming]

Există două limitări pentru o variabilă din JavaScript:

1. Numele trebuie să conțină doar litere, cifre, simbolurile `$` și `_`.
2. Primul caracter nu trebuie să fie cifră.

Nume valide, spre exemplu:

```js
let userName;
let test123;
```

Când numele conține mai multe cuvinte, în mod normal este folosit [camelCase](https://en.wikipedia.org/wiki/CamelCase). Asta înseamnă: cuvintele se pun unele după celelalte, fiecare cuvânt începe cu o majusculă: `myVeryLongName`.

Ce este interesant -- semnul dolar `'$'` și underscore `'_'` pot fi de asemenea folosite în denumiri. Ele sunt simboluri obișnuite, ca și literele, fără un înțeles special.

Aceste denumiri sunt valide:

```js run untrusted
let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"

alert($ + _); // 3
```

Exemple de denumiri ale variabilelor incorecte:

```js no-beautify
let 1a; // cannot start with a digit

let my-name; // a hyphen '-' is not allowed in the name
```

```smart header="Case matters"
Variabilele denumite `apple` și `AppLE` -- sunt două variabile diferite.
```

````smart header="Non-English letters are allowed, but not recommended"
Este posibil să folosești orice limbă, inclusiv litere chirilice sau hieroglife, astfel:

```js
let имя = '...';
let 我 = '...';
```

Din punct de vedere tehnic aici nu este nici o eroare, astfel de denumiri sunt permise, dar există o tradiție internațională de a folosi engleza în denumirile variabilelor. Chiar dacă scriem un script micuț, ar putea avea o viață lungă înainte. Oameni din alte țări e posibil să trebuiască să-l citească cândva.
````

````warn header="Reserved names"
Există o [listă de cuvinte rezervate](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords), ce nu pot fi folosite pe post de denumire de variabile, pentru că  ele sunt folosite de limbajul însăși.

De exemplu, cuvintele `let`, `class`, `return`, `function` sunt rezervate.

Codul de mai jos va da o eroare de sintaxă:

```js run no-beautify
let let = 5; // can't name a variable "let", error!
let return = 5; // also can't name it "return", error!
```
````

````warn header="An assignment without `use strict`"

În mod normal trebuie să definim o variabilă înainte de a o folosi. Dar în vremurile mai vechi era posibil, tehnic vorbind, să creezi o variabilă prin simpla asignare a valorii, fără a folosi `let`. Acest lucru încă funcționează și acum dacă nu punem `use strict`. Comportamentul este ținut pentru compatibilitatea cu script-urile vechi.

```js run no-strict
// note: no "use strict" in this example

num = 5; // the variable "num" is created if didn't exist

alert(num); // 5
```

Aceasta reprezintă o practică rea, va da eroare în modul strict:

```js run untrusted
"use strict";

*!*
num = 5; // error: num is not defined
*/!*
```

````

## Constante

Pentru a declara o constantă variabilă (neschimbată), se poate folosi `const` în loc de `let`:

```js
const myBirthday = '18.04.1982';
```

Variabilele declarate folosind `const` sunt denumite "constante". Ele nu pot fi schimbate. O încercare de a face aceasta va cauza o eroare:

```js run
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

Când un programator este sigur că variabilele nu ar trebui să se schimbe vreodată acesta poate folosi `const` pentru a garanta acest lucru, și pentru a arăta aceasta și celorlalți.


### Constante cu majuscule

Există o practică comună de a folosi constante ca și aliasuri pentru valori care sunt greu de ținut minte și sunt știute dinainte de execuție.

Astfel de constante sunt denumite folosind litere majuscule sau underscores.

Ca aici:

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...when we need to pick a color
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

Beneficii:

- `COLOR_ORANGE` este mult mai ușor de ținut minte decât `"#FF7F00"`.
- Este mult mai ușor să scrii greșit `"#FF7F00"` decât `COLOR_ORANGE`. 
- Când citim codul `COLOR_ORANGE` are mai mult înțeles decât `#FF7F00`.

Când ar trebui să folosim majuscule pentru constante și când ar trebui să le denumim normal? Să clarificăm acest lucru.

A fi o "constantă" îmseamnă doar că valoarea nu se schimbă niciodată. Dar există constante care sunt cunoscute dinainte de execuție (precum valoare hexazecimală pentru roșu) și mai sunt cele care sunt "calculate" la run-time, în timpul execuției, dar nu se schimbă după asignare.

Spre exemplu:
```js
const pageLoadTime = /* time taken by a webpage to load */;
```

Valoarea lui `pageLoadTime` nu este știută înainte ca pagina să se încarce, așa că este denumită normal. Dar este totuși o constantă, pentru că nu se modifică după asignare.

Cu alte cuvinte, constantele denumite cu majusculă sunt folosite doar ca și aliasuri pentru valori "hard-coded".

## Denumește lucrurile corect

Vorbind de variabile, mai este un lucru extrem de important.

Te rog denumește variabilele chibzuit. Ia-ți timp și gândeștete dacă este necesar.

Denumirea variabilelor este una dintre cele mai importante și mai complexe abilități din programare. O scurtă privire la numele variabilelor poate descoperi care cod este scris de un începător și care este scris de un developer experimentat.

Într-un proiect real, marea parte a timpului este petrecută modificând și extinzând codul de bază deja existent, și nu scriind ceva complet separat, de la zero. Iar atunci când ne reîntoarcem la cod după ceva timp în care am făcut altceva este mult mai ușor să găsim informații care sunt corect denumite. Sau cu alte cuvinte când variabilele au nume potrivite.

Te rog, petrece ceva timp gândindu-te la denumirea potrivită a unei variabile înainte de a o declara. Acest lucru de va răsplăti mult.

Câteva reguli bune de urmat ar fi:

- Folosește denumiri ce pot fi citite de către oameni precum `userName` sau `shoppingCart`.
- Stai departe de abrevieri sau nu scurte ca `a`, `b`, `c`, doar dacă chiar știi ce faci.
- Fă denumirea maxim descriptivă și concisă. Exemple de nume rele sunt `data` and `value`. Un astfel de nume nu spune nimic. Este în regulă să le folosim doar dacă este excepțional de evident , din context, ce date sau valori se vor a fi.
- Pune-te de acord cu echipa și cu propria ta minte. Dacă un vizitator al site-ului este numit "user" atunci ar trebui să denumim variabililele care au legătură ca și `currentUser` sau `newUser`, dar nu ca și `currentVisitor` sau `newManInTown`.

Sună simplu? Într-adevăr este, dar în practică, crearea de nume descriptive și concies nu este așa. Du-te!

```smart header="Reuse or create?"
Ca și o ultimă observație. Există programatori leneși care în loc să  declare o variabilă nouă tind să reutilizeze variabile deja existente.

Ca și rezultat variabila este ca o cutie unde oamenii aruncă diferite lucruri fără a schimba eticheta. Ce este acum înăuntru? Cine știe... Trebuie să ne apropiem și să verificăm.

Un astfel de programator câștigă puțin ca declarație a variabilelor, dar pierde de zece ori mai mult pe debugging-ul codului.

O variabilă în plus este bine, nu malefic.

Minificatoarele moderne de JavaScript și browserele optimizează codul destul de bine, așa că nu va creea probleme de performanță. Folosirea a diferite variabile pentru valori diferite poate chiar ajuta motorul să optimizeze.
```

## Rezumat

Putem declara variabile pentru a stoca date. Acest lucru poate fi făcut folosind `var` sau `let` sau `const`.

- `let` -- este o declarație de variabilă modernă. Codul trebuie să fie în modul strict pentru a utiliza `let` în Chrome (V8).
- `var` -- este o declarație de variabilă de modă veche. În mod normal nu le folosim pe toate, dar vom acoperi diferențele subtile ale `let` în capitolul <info:var>, în cazul în care ai nevoie de ele.
- `const` -- este ca `let`, dar valoarea variabile nu poate fi modificată.

Variabilele ar trebui denumite într-un mod în care să ne permită să înțelegem ușor ce se află înăuntru.