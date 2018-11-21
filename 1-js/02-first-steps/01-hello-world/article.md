# Hello, world!

Tutorialul pe care îl citești este despre core JavaScript, care este independent de platformă. Mai mult, vei învăța Node.JS și alte platforme care îl folosesc.

Dar, avem nevoie de un mediu de lucru pentru a rula scripturile noastre, și doar pentru că cartea aceasta este online, browser-ul este o alegere bună. Vom minimiza cantitatea de comenzi specifice browser-ului (precum `alert`) pentru ca tu să nu-ți petreci timpul cu ele dacă plănuiești să te concentrezi pe un alt mediu ca Node.JS. Pe de altă parte, detaliile despre browser sunt explicate  în detaliu în [următoarea parte](/ui) a tutorialului.

Așadar pentru început, să vedem cum poți atașa un script pe o pagină web. Pentru medii server-side, îl poți executa cu o comandă ca `"node my.js"` pentru Node.JS.


## Eticheta "script" (Tag-ul "script")

Programele JavaScript pot fi inserate în orice parte a unui document HTML cu ajutorul tagului `<script>`

Spre exemplu:

```html run height=100
<!DOCTYPE HTML>
<html>

<body>

  <p>Before the script...</p>

*!*
  <script>
    alert( 'Hello, world!' );
  </script>
*/!*

  <p>...After the script.</p>

</body>

</html>
```

```online
Poți rula exemplul făcând click pe butonul "Play" din colțul dreapta-sus.
```

Tag-ul `<script>` conține cod JavaScript care este executat în mod automat când browser-ul întâlneșete eticheta(tag-ul).

## Marcarea modernă

Eticheta `<script>` are câteva atribute care sunt destul de rar folosite în zilele noastre, dar le putem găsi în cod vechi:

Atributul `type`: <code>&lt;script <u>type</u>=...&gt;</code>
 : Vechiul standard HTML4 necesita ca un script să aibă tip. De obicei acesta era `type="text/javascript"`. Nu mai este necesar. De asemenea, standardul modern a schimbat total înțelesul acestui atribut. Acum el poate fi folosit pentru module JavaScript. Dar acesta este un subiect avansat; vom vorbi despre module mai târziu, într-o altă parte a tutorialului.

Atributul `language`: <code>&lt;script <u>language</u>=...&gt;</code>
  : Acest atribut era menit să afișeze limbajul script-ului. Acest atribut nu mai are sens, pentru JavaScript este limbajul implicit. Nu e necesar să-l folosim.

Comentarii înainte și după script-uri.
: În cărțiile și ghidurile destul de antice, pot fi găsite comentarii înăuntr-ul `<script>`, astfel:

    ```html no-beautify
    <script type="text/javascript"><!--
        ...
    //--></script>
    ```

    Acest truc nu este folosit în JavaScript-ul modern. Aceste comentarii erau folosite pentru a ascunde codul JavaScript de browserele vechi care nu știau de tag-ul `<script>`. Cum browserele lansate în ultimii 15 ani nu au această problemă, acest tip de comentariu te poate ajuta să identifici cod cu adevărat vechi. 


## Script-uri externe

Dacă avem mult cod JavaScript, îl putem pune într-un fișier separat.

Fișierul script este atașat HTML-ului cu atributul `src`:

```html
<script src="/path/to/script.js"></script>
```

Aici `/path/to/script.js` este o cale absolută către fișierul cu script-ul(din site-ul rădăcină).

Este de asemenea posibil să furnizezi o cale relativă către pagina curentă. De exemplu, `src="script.js"` înseamnă un fișier `"script.js"` în folder-ul curent.

Putem da un URL complet de asemenea. De exemplu:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js"></script>
```

Pentru a atașa mai multe script-uri, folosim etichetele:

```html
<script src="/js/script1.js"></script>
<script src="/js/script2.js"></script>
…
```

```smart
Ca și regulă, doar script-urile cele mai simple sunt puse în HTML. Cele mai complexe vor sta în fișiere separate.

Beneficiul unui fișier separat este că browser-ul îl va descărca și îl va stoca în [cache](https://en.wikipedia.org/wiki/Web_cache).

După aceasta, alte pagini care vor vrea același script îl vor lua din cache în loc să-l descarce. Așadar fișierul este defapt descărcat doar odată.

Acest lucru salvează trafic și face paginile mai rapide.
```

````warn header="If `src` is set, the script content is ignored."
Un singur tag `<script>` nu poate avea atât atributul `src` cât și cod în interior.

Asta nu va merge:

```html
<script *!*src*/!*="file.js">
  alert(1); // the content is ignored, because src is set
</script>
```

Trebuie să alegem: ori este un script extern `<script src="…">` ori unul obișnuit `<script>` cu cod.

Exemplul de mai sus poate fi rupt în două script-uri pentru a funcționa:

```html
<script src="file.js"></script>
<script>
  alert(1);
</script>
```
````

## Rezumat

- Putem folosi eticheta `<script>` pentru a adăuga cod JavaScript paginii.
- Atributele `type` și `language` nu sunt necesare.
- Un script dintr-un fișier extern poate fi inserat cu `<script src="path/to/script.js"></script>`.

Mai este mult de învățat despre script-urile de browser și interacțiunile lor cu pagina web. Dar să ne amintim că această parte a tutorialului este dedicată limbajului JavaScript, așa că nu ar trebui să ne distragem atenția de la acest lucru. Vom folosi un browser ca mijloc de rulare a JavaScript-ului, ceea ce este foarte convenabil pentru citirea online, dar totuși unul dintre multe altele.