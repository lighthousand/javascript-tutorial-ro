# Modul modern, "use strict"

Pentru o lungă perioadă de timp JavaScript evolua fără probleme de compatibilitate. Noi feature-uri erau adăugate limbajului, dar funcționalitatea veche nu s-a schimbat.

Acest lucru a avut beneficiul de a nu strica codul deja existent. Însă dezavantajul era că orice greșeală sau o decizie imperfectă făcută de către creatorii JavaScript ar fi rămas blocată în limbaj pentru totdeauna.

Așa s-a întâmplat până în 2009 când a apărut ECMAScript 5 (ES5). Acesta a adăugat noi trăsături limbajului și a modificat unele deja existente. Pentru a păstra vechiul cod care mergea, majoritatea modificărilor sunt oprite implicit. Ele trebuie activate explicit cu o directivă specială `"use strict"`.

## "use strict"

Directiva arată ca un string: `"use strict"` sau `'use strict'`. Când este localizat sus, la începutul script-ului, atunci tot scriptul funcționează în maniera "modernă",

De exemplu

```js
"use strict";

// this code works the modern way
...
```

Vom învăța funcții (o modalitate de a grupa comenzi) în curând.

Privind înainte, să observăm doar că `"use strict"` poate fi pus la începutul unei funcții (majoritatea tipurilor de funcții) în loc de începutul script-ului. Atunci modul strict este activat doar în acea funcție. Dar de obicei oamenii îl folosesc pentru întregul script.

````warn header="Ensure that \"use strict\" is at the top"
Te rog, asigură-te că `"use strict"` se află la începutul script-ului, altfel modul strict s-ar putea să nu fie activat.

Aici nu e niciun mod strict:

```js no-strict
alert("some code");
// "use strict" below is ignored, must be on the top

"use strict";

// strict mode is not activated
```

Doar comentariile pot apărea deasupra lui `"use strict"`.
````

```warn header="There's no way to cancel `use strict`"
Nu există nicio directivă `"no use strict"` sau ceva asemănător, care ar returna un comportament vechi.

Odată ce intrăm în modul strict nu mai există cale de întoarcere.
```

## Întotdeauna folosește "use strict"

Diferența dintre `"use strict"` și modul "default" urmează a fi acoperite.

În următoarele capitole, pe măsură ce învățăm caracteristicile limbajului, vom nota diferențele dintre modul strict și modul default. Din fericire nu sunt prea multe. Și defapt ele ne fac viața mai ușoară.

La acest moment în timp este suficient să știi despre el (limbaj) în general:

1. Directiva `"use strict"` comută motorul în modul modern, schimbând comportamentul unor caracteristici built-in. Vom vedea detaliile pe măsură ce învățăm.
2. Modul strict este activat de către `"use strict"` la începutul scriptului. De asemenea există câteva caracteristici de limbaj precum "clasele" (classes) și "module" (modules) ce activează modul strict în mod automat.
3. Modul strict este suportat de către toate browserele moderne.
4. Este întotdeauna recomandat să începi scripturile cu `"use strict"`. Toate exemplele din acest tutorial presupun acest lucru, dacă nu este specificat (foarte rar) altfel.