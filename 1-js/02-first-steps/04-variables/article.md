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

## Variable naming [#variable-naming]

There are two limitations for a variable name in JavaScript:

1. The name must contain only letters, digits, symbols `$` and `_`.
2. The first character must not be a digit.

Valid names, for instance:

```js
let userName;
let test123;
```

When the name contains multiple words, [camelCase](https://en.wikipedia.org/wiki/CamelCase) is commonly used. That is: words go one after another, each word starts with a capital letter: `myVeryLongName`.

What's interesting -- the dollar sign `'$'` and the underscore `'_'` can also be used in names. They are regular symbols, just like letters, without any special meaning.

These names are valid:

```js run untrusted
let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"

alert($ + _); // 3
```

Examples of incorrect variable names:

```js no-beautify
let 1a; // cannot start with a digit

let my-name; // a hyphen '-' is not allowed in the name
```

```smart header="Case matters"
Variables named `apple` and `AppLE` -- are two different variables.
```

````smart header="Non-English letters are allowed, but not recommended"
It is possible to use any language, including cyrillic letters or even hieroglyphs, like this:

```js
let имя = '...';
let 我 = '...';
```

Technically, there is no error here, such names are allowed, but there is an international tradition to use English in variable names. Even if we're writing a small script, it may have a long life ahead. People from other countries may need to read it some time.
````

````warn header="Reserved names"
There is a [list of reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords), which cannot be used as variable names, because they are used by the language itself.

For example, words `let`, `class`, `return`, `function` are reserved.

The code below gives a syntax error:

```js run no-beautify
let let = 5; // can't name a variable "let", error!
let return = 5; // also can't name it "return", error!
```
````

````warn header="An assignment without `use strict`"

Normally, we need to define a variable before using it. But in the old times, it was technically possible to create a variable by a mere assignment of the value, without `let`. This still works now if we don't put `use strict`. The behavior is kept for compatibility with old scripts.

```js run no-strict
// note: no "use strict" in this example

num = 5; // the variable "num" is created if didn't exist

alert(num); // 5
```

That's a bad practice, it gives an error in the strict mode:

```js run untrusted
"use strict";

*!*
num = 5; // error: num is not defined
*/!*
```

````

## Constants

To declare a constant (unchanging) variable, one can use `const` instead of `let`:

```js
const myBirthday = '18.04.1982';
```

Variables declared using `const` are called "constants". They cannot be changed. An attempt to do it would cause an error:

```js run
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

When a programmer is sure that the variable should never change, they can use `const` to guarantee it, and also to clearly show that fact to everyone.


### Uppercase constants

There is a widespread practice to use constants as aliases for difficult-to-remember values that are known prior to execution.

Such constants are named using capital letters and underscores.

Like this:

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...when we need to pick a color
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

Benefits:

- `COLOR_ORANGE` is much easier to remember than `"#FF7F00"`.
- It is much easier to mistype in `"#FF7F00"` than in `COLOR_ORANGE`.
- When reading the code, `COLOR_ORANGE` is much more meaningful than `#FF7F00`.

When should we use capitals for a constant, and when should we name them normally? Let's make that clear.

Being a "constant" just means that the value never changes. But there are constants that are known prior to execution (like a hexadecimal value for red), and there are those that are *calculated* in run-time, during the execution, but do not change after the assignment.

For instance:
```js
const pageLoadTime = /* time taken by a webpage to load */;
```

The value of `pageLoadTime` is not known prior to the page load, so it's named normally. But it's still a constant, because it doesn't change after assignment.

In other words, capital-named constants are only used as aliases for "hard-coded" values.  

## Name things right

Talking about variables, there's one more extremely important thing.

Please name the variables sensibly. Take time to think if needed.

Variable naming is one of the most important and complex skills in programming. A quick glance at variable names can reveal which code is written by a beginner and which by an experienced developer.

In a real project, most of the time is spent on modifying and extending the existing code base, rather than writing something completely separate from scratch. And when we return to the code after some time of doing something else, it's much easier to find information that is well-labeled. Or, in other words, when the variables have good names.

Please spend some time thinking about the right name for a variable before declaring it. This will repay you a lot.

Some good-to-follow rules are:

- Use human-readable names like `userName` or `shoppingCart`.
- Stay away from abbreviations or short names like `a`, `b`, `c`, unless you really know what you're doing.
- Make the name maximally descriptive and concise. Examples of bad names are `data` and `value`. Such a name says nothing. It is only ok to use them if it's exceptionally obvious from the context which data or value is meant.
- Agree on terms within your team and in your own mind. If a site visitor is called a "user" then we should name related variables like `currentUser` or `newUser`, but not `currentVisitor` or a `newManInTown`.

Sounds simple? Indeed it is, but creating good descriptive-and-concise names in practice is not. Go for it.

```smart header="Reuse or create?"
And the last note. There are some lazy programmers who, instead of declaring a new variable, tend to reuse the existing ones.

As a result, the variable is like a box where people throw different things without changing the sticker. What is inside it now? Who knows... We need to come closer and check.

Such a programmer saves a little bit on variable declaration, but loses ten times more on debugging the code.

An extra variable is good, not evil.

Modern JavaScript minifiers and browsers optimize code well enough, so it won't create performance issues. Using different variables for different values can even help the engine to optimize.
```

## Summary

We can declare variables to store data. That can be done using `var` or `let` or `const`.

- `let` -- is a modern variable declaration. The code must be in strict mode to use `let` in Chrome (V8).
- `var` -- is an old-school variable declaration. Normally we don't use it at all, but we'll cover subtle differences from `let` in the chapter <info:var>, just in case you need them.
- `const` -- is like `let`, but the value of the variable can't be changed.

Variables should be named in a way that allows us to easily understand what's inside.
