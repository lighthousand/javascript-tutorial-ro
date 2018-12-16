# Interacțiune: alert, prompt, confirm

Această parte a tutorialului țintește să acopere JavaScript-ul "așa cum este", fără trucurile specifice mediului.

Dar totuși folosim browser-ul ca și mediu de demo. Așadar ar trebui să știm câteva funcții de interfață. În acest capitol ne vom familiariza cu funcțiile browser-ului `alert`, `prompt` and `confirm`.

## alert

Sintaxă:

```js
alert(message);
```

Acest cod afișează un mesaj și pauzează script-ul până când user-ul apasă "OK".

De exemplu:

```js run
alert("Hello");
```

Mini fereastra cu mesajul este denumită *fereastră modal*. Cuvântul "modal" semnifică faptul că vizitatorul nu poate interacționa cu restul paginii, să apese alt buton etc, până ce nu s-a ocupat de pagină. În acest caz -- până când acesta apasă "OK".

## prompt

Funcția `prompt` acceptă două argumente:

```js no-beautify
result = prompt(title[, default]);
```

Afișează o fereastră modal cu un mesaj text, un câmp input pentru vizitator și butoanele OK/CANCEL.

`title`
: Textul de arătat vizitatorului.

`default`
: Un parametru secundar opțional, valoarea inițială pentru câmpul input.

Vizitatorul poate tipări ceva în câmpul de input din prompt și să apese OK. Sau acesta poate poate anula inputul apăsând butonul CANCEL sau apăsând tasta `key:Esc`.

Apelul lui `prompt` returnează textul din câmp sau `null` dacă input-ul a fost anulat.

Spre exemplu:

```js run
let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
```

````warn header="IE: always supply a `default`"
Al doilea parametru este opțional. Dar dacă nu îl dăm Internet Explorer va insera textul `"undefined"` în prompt.

Rulează acest cod în Internet Explorer pentru a vedea acest lucru:

```js run
let test = prompt("Test");
```

Așadar pentru a arăta bine în IE este recomandat ca întotdeauna să se furnizeze al doilea argument:

```js run
let test = prompt("Test", ''); // <-- for IE
```
````

## confirm

Sintaxa:

```js
result = confirm(question);
```

Funcția `confirm` afișează o fereastră modal cu o `întrebare` și două butoane: OK și CANCEL.

Rezultatul este `true` dacă OK a fost apăsat și `false` altfel.

De exemplu:

```js run
let isBoss = confirm("Are you the boss?");

alert( isBoss ); // true if OK is pressed
```

## Rezumat

Am acoperit 3 funcții de interacțiune cu vizitatorul, specifice browser-ului:

`alert`
: afișează un mesaj.

`prompt`
: afișează un mesaj, cerând utilizatorului să introducă text. Returnează textul sau dacă butoanele CANCEL sau `key:Esc` sunt apăsate toate browserele vor returna `null`.

`confirm`
: afișează un mesaj și așteaptă ca utilizatorul să apese "OK" or "CANCEL". Va returna `true` pentru OK și `false` for CANCEL/`key:Esc`.

Toate aceste metode sunt de tip modal: ele vor pauza execuția scriptului și nu vor permite vizitatorului să interacționeze cu restul paginii până ce mesajul a fost respins.

Există două limitări împărțite de toate metodele de mai sus:

1. Locația exactă a ferestrei modal este determinată de browser. De obicei este în centru.
2. Aspectul exact al ferestrei depinde de asemenea de browser. Nu îl putem modifica.

Acesta este prețul pentru simplitate. Există alte modalități de a arăta ferestre mai frumoase și interacțiune mai bogată cu vizitatorul, dar dacă "clopotele și fluierele" nu contează prea mult, aceste metode vor fi suficiente.