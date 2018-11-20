# Introducere în JavaScript

Să vedem ce e atât de special la JavaScript, ce putem realiza cu el și ce alte tehnologii se înțeleg bine cu acesta.

## Ce este JavaScript?

*JavaScript* a fost creat inițial pentru *"make web pages alive"*.

În acest limbaj programele sunt numite *scripts*(script-uri). Acestea pot fi scrise direct în HTML și executate în mod automat pe măsură ce pagina se încarcă.

Script-urile sunt furnizate și executate ca și text simplu. Ele nu au nevoie de pregătire specială sau de compilație pentru a rula.

În ceea ce privește acest aspect, JavaScript este foarte diferit de un alt limbaj cu nume asemănător [Java](https://en.wikipedia.org/wiki/Java_(programming_language)).

```smart header="Why <u>Java</u>Script?"
Când JavaScript a fost creat, inițial avea un alt nume: "LiveScript". Dar la acel moment limbajul Java era foarte popular, așa că a fost decis că poziționarea unui nou limbaj ca și "frate mai mic" al lui Java, va ajuta.

Dar cum acesta a evoluat, JavaScript a devenit un limbaj complet independent, cu propriile specificații, numite [ECMAScript](http://en.wikipedia.org/wiki/ECMAScript), iar acum nu mai are nici o legătură cu Java.
```

În prezent, JavaScript nu doar că poate executa în browser, dar de asemenea poate executa pe server, sau chiar pe orice dispozitiv care are un program special numit [ the JavaScript engine(motorul JavaScript)](https://en.wikipedia.org/wiki/JavaScript_engine).

Browser-ul are un motor încorporat, uneori denumit "JavaScript virtual machine"(mașină virtuală JavaScript).

Diferite motoare au diferite "nume de cod", spre exemplu:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- în Chrome și Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- în Firefox.
- ...Mai există și alte nume de cod precum "Trident" și "Chakra" pentru diferite versiuni de IE, "ChakraCore" pentru Microsoft Edge, "Nitro" și "SquirrelFish" pentru Safari, etc.

Termenii de mai sus e bine să fie memorați, pentru că ei sunt folosiți în articole ale dezvoltatorilor, pe internet. De exemplu, dacă "o caracteristică X este suportată de către V8", atunci probabil că merge și în Chrome și în Opera.

```smart header="How do engines work?"

Motoarele sunt complicate. Dar fundamentele sunt ușoare.

1. Motorul (încorporat dacă este un browser) citește("parsează") script-ul.
2. Apoi convertește("compilează") script-ul în limbajul mașină.
3. Apoi codul mașină rulează, destul de repede.

Motorul aplică optimizări la fiecare stadiu al procesului. Ba chiar observă script-ul compilat cum rulează, analizează datele care trec prin el și aplică optimizări asupra codului mașină, bazate pe informațiile strânse. La sfârșit script-urile sunt chiar rapide.
```

## Ce poate in-browser JavaScript să facă?

JavaScript-ul modern este un limbaj de programare "sigur". Nu furnizează acces low-level la memorie sau la CPU, pentru că inițial a fost creat pentru browsere, care nu necesitau acest lucru.

Capacitățile depind mult de mediul care rulează JavaScript. De exemplu, [Node.JS](https://wikipedia.org/wiki/Node.js) suportă funcții care permit JavaScript-ului să citească/scrie fișiere arbitrare, să realizeze request-uri de rețea, etc.

In-browser Javascript poate face orice în legătură cu manipularea paginii web, interacțiunea cu utilizatorului, și cu serverul web.

De exemplu, in-browser JavaScript este capabil să: 

- Adauge HTML nou în pagină, schimbe  conținutul existent, modifice stiluri.
- Reacționeze la acțiunile utilizatorului, execute la click de mouse, mișcări ale cursorului, sau apăsări de taste.
- Trimită request-uri prin rețea către servere remote(la distanță), descarce și încarce fișiere (așa-numitele tehnologii [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming) și [COMET](https://en.wikipedia.org/wiki/Comet_(programming)).
- Preia și să seteze cookie-uri, pună întrebări vizitatorului, arate mesaje.
- Să-și amintească date pe partea de client("local storage").

## Ce nu poate in-browser JavaScript să facă?

Abilitățile JavaScript-ului în browser sunt limitate pentru siguranța utilizatorului. Scopul este acela de a preveni o pagină web malițioasă să acceseze informații private sau să corupă datele utilizatorului.

Exemplele acestor restricții sunt:

- JavaScript, pe o pagină web, nu poate citi/scrie fișiere arbitrare pe hard disk, nu le poate copia sau să execute un program. Nu are acces direct la funcțiile sistemului de operare.

	Browserele moderne îi permit să lucreze cu fișiere, dar accesul este limitat și furnizat doar dacă utilizatorul realizează anumite acțiuni, cum ar fi "scăparea" unui fișier într-o fereastră de browser sau selectarea lui printr-un tag `<input>`.

	Există mijloace prin care se poate interacționa cu camera/microfonul sau alte dispozitive, dar ele necesită permisiunea explicită a utilizatorului. Așadar o pagină pe care este activat JavaScript-ul nu ar putea activa o cameră web în mod viclean, și privească împrejurimile și să trimită informații către [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- În general, diferite tab-uri/ferestre nu știu unele despre celelalte. Câteodată aceste știu, de exemplu când o fereastră folosește JavaScript pentru a deschide cealaltă fereastră. Dar chiar și în acest caz, JavaScript nu poate accesa cealaltă fereastră dacă ambele ferestre vin de pe site-uri diferite (de la un domeniu, protocol sau port diferit).

    This is called the "Same Origin Policy". To work around that, *both pages* must contain a special JavaScript code that handles data exchange.

    The limitation is again for user's safety. A page from `http://anysite.com` which a user has opened must not be able to access another browser tab with the URL `http://gmail.com` and steal information from there.
- JavaScript can easily communicate over the net to the server where the current page came from. But its ability to receive data from other sites/domains is crippled. Though possible, it requires explicit agreement (expressed in HTTP headers) from the remote side. Once again, that's safety limitations.

![](limitations.png)

Such limits do not exist if JavaScript is used outside of the browser, for example on a server. Modern browsers also allow installing plugin/extensions which may get extended permissions.

## What makes JavaScript unique?

There are at least *three* great things about JavaScript:

```compare
+ Full integration with HTML/CSS.
+ Simple things are done simply.
+ Supported by all major browsers and enabled by default.
```

Combined, these three things exist only in JavaScript and no other browser technology.

That's what makes JavaScript unique. That's why it's the most widespread tool to create browser interfaces.

While planning to learn a new technology, it's beneficial to check its perspectives. So let's move on to the modern trends that include new languages and browser abilities.


## Languages "over" JavaScript

The syntax of JavaScript does not suit everyone's needs. Different people want different features.

That's to be expected, because projects and requirements are different for everyone.

So recently a plethora of new languages appeared, which are *transpiled* (converted) to JavaScript before they run in the browser.

Modern tools make the transpilation very fast and transparent, actually allowing developers to code in another language and auto-converting it "under the hood".

Examples of such languages:

- [CoffeeScript](http://coffeescript.org/) is a "syntactic sugar" for JavaScript, it introduces shorter syntax, allowing to write more precise and clear code. Usually Ruby devs like it.
- [TypeScript](http://www.typescriptlang.org/) is concentrated on adding "strict data typing", to simplify the development and support of complex systems. It is developed by Microsoft.
- [Dart](https://www.dartlang.org/) is a standalone language that has its own engine that runs in non-browser environments (like mobile apps). It was initially offered by Google as a replacement for JavaScript, but as of now, browsers require it to be transpiled to JavaScript just like the ones above.

There are more. Of course, even if we use one of those languages, we should also know JavaScript, to really understand what we're doing.

## Summary

- JavaScript was initially created as a browser-only language, but now it is used in many other environments as well.
- At this moment, JavaScript has a unique position as the most widely-adopted browser language with full integration with HTML/CSS.
- There are many languages that get "transpiled" to JavaScript and provide certain features. It is recommended to take a look at them, at least briefly, after mastering JavaScript.
