# Structura codului

Primul lucru ce trebuie studiat sunt elementele fundamentale ale codului.

## Afirmații (statements)

Statement-urile sunt constructorii de sintaxă și comenzile care realizează acțiuni.

Am văzut deja un statement `alert('Hello, world!')`, care arată mesajul "Hello world!".

Putem avea câte afirmații vrem, în cod. O altă afirmație poate fi separată cu punct și virgulă (;).

De exemplu, aici putem rupe mesajul în două:

```js run no-beautify
alert('Hello'); alert('World');
```

De obicei fiecare afirmație este scrisă pe o linie separată -- astfel codul devine mult mai lizibil:

```js run no-beautify
alert('Hello');
alert('World');
```

## Caracterele punct și virgulă [#semicolon]

Un caracter punct și virgulă poate fi omis în majoritatea cazurilor când există o rupere de linie (break line);

Aceasta ar funcționa de asemenea:

```js run no-beautify
alert('Hello')
alert('World')
```

Aici, JavaScript interpretează un line break ca și punct și virgulă "implicit". Acest lucru este de asemenea denumit [inserție automată de punct și virgulă](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion).

**În majoritatea cazurilor o linie nouă implică un caracter punct și virgulă. Dar "în majoritatea cazurilor" nu înseamnă "întotdeauna"!**

Există cazuri când o linie nouă nu înseamnă punct și virgulă, spre exemplu:

```js run no-beautify
alert(3 +
1
+ 2);
```

Codul returnează `6` pentru că JavaScript nu inserează punct și virgulă aici. Este, în mod intuitiv, evident faptul că dacă linia se termină cu un plus `"+"`, atunci aceasta este o "expresie incompletă", așa că punctul și virgula nu sunt necesare. Iar în acest caz totul funcționează după cum ne așteptăm.

**Dar există și situații când JavaScript "eșuează" în a intui un punct și virgulă unde este cu adevărat necesar.**

Erorile care apar în asemenea cazuri sunt destul de greu de găsit și reparat.

````smart header="An example of an error"
Dacă ești curios să vezi un exemplu de astfel de eroare, aruncă o privire pe codul ăsta:

```js run
[1, 2].forEach(alert)
```

Încă nu e nevoie să-ți bați capul în legătură cu ce reprezintă parantezele drepte `[]` sau `forEach`. Le vom studia mai târziu, pentru moment nu contează. Să ne reamintim rezultatul: se afișează `1`, apoi `2`.

Acum să adăugăm un `alert` înaintea codului și să *nu* încheiem cu punct și virgulă:

```js run no-beautify
alert("There will be an error")

[1, 2].forEach(alert)
```

Acum dacă îl rulăm, doar primul `alert` este afișat și apoi avem o eroare!

Dar totul este în regulă din nou, dacă adăugăm un punct și virgulă după `alert`:
```js run
alert("All fine now");

[1, 2].forEach(alert)  
```

Acum avem mesajul "All fine now", iar apoi `1` și `2`.

Eroarea din varianta fără niciun punct și virgulă apare deoarece JavaScript nu adaugă un punct și virgulă înainte de parantezele drepte `[...]`.

Așadar, pentru că punctul și virgula nu sunt auto-generate, codul din primul exemplu este tratat ca un singur statement. Așa îl vede engine-ul:

```js run no-beautify
alert("There will be an error")[1, 2].forEach(alert)
```

Dar ar trebui să fie două afirmații separate, nu una singură. O astfel de îmbinare în acest caz este greșită, de aici și eroarea. Există alte situații în care se întâmplă un astfel de lucru.
````

Este recomandat să punem punct și virgulă între afirmații chiar dacă acestea sunt separate de caractere de linie nouă. Această regulă este larg adoptată de către comunitate. Să observăm din nou -- *este posibil* să nu punem punct și virgulă în majoritatea timpului. Dar este mai sigur -- în special pentru un începător -- să le folosească.

## Comentarii

Pe măsură ce timpul trece, programul devine din ce în ce mai complex. Devine necesar să se adauge *comentarii* care să descrie ce se întâmplă și de ce.

Comentariile pot fi puse în orice loc în script. Ele nu afectează execuția pentru că motorul pur și simplu le ignoră.

**Comentariile pe o singură linie încep cu două caractere forward slash `//`.**

Restul liniei este un comentariu. Poate ocupa o linie completă doar el sau poate să urmeze o afirmație. 

Cum ar fi aici:
```js run
// This comment occupies a line of its own
alert('Hello');

alert('World'); // This comment follows the statement
```

**Comentariile multilinie încep cu un forward slash și cu un asterisk <code>/&#42;</code> și se termină cu asterisk și cu un forward slash <code>&#42;/</code>.**

Cum ar fi aici:

```js run
/* An example with two messages.
This is a multiline comment.
*/
alert('Hello');
alert('World');
```

Conținutul comentariilor este ignorat, așa că dacă punem cod înăuntru <code>/&#42; ... &#42;/</code> acesta nu se va executa.

Câteodată ne este la îndemână să dezactivăm temporar o parte din cod:

```js run
/* Commenting out the code
alert('Hello');
*/
alert('World');
```

```smart header="Use hotkeys!"
În majoritatea editoarelor o linie de cod poate fi comentată cu `tastele:Ctrl+/` pentru un comentariu single-line și cu `tastele:Ctrl+Shift+/` -- pentru comentarii multilinie (selectează o bucată de cod și apasă tastele arătate). Pnetru Mac încearcă `tasta:Cmd` în loc de `tasta:Ctrl`.
```

````warn header="Nested comments are not supported!"
Nu poate exista `/*...*/` în interiorul la `/*...*/`.

Astfel de cod va "muri" cu o eroare:

```js run no-beautify
/*
  /* nested comment ?!? */
*/
alert( 'World' );
```
````

Te rog, nu ezita să-ți comentezi codul.

Comentariile cresc urma globală a codului, dar asta nu reprezintă o problemă. Există multe tool-uri care minimizează codul înainte ca acesta să fie publicat pe server-ul de producție. Sunt scoase comentariile, ca să nu apară în scripturile care sunt executate. Astfel comentariile nu au deloc efecte negative asupra producției.

Mai departe, în tutorial va fi un capitol <info:coding-style> care de asemenea explică cum să scrii comentarii mai bune.