importanță: 4

---

# Constantă uppercase?

Examinează următorul cod:

```js
const birthday = '18.04.1982';

const age = someCode(birthday);
```

Aici avem o constantă `birthday` și `age` care este calculată din `birthday` cu ajutorul a puțin cod (nu este dat din cauza lungimii, și pentru că detaliile nu contează aici).

Ar fi potrivit să folosești upper case pentru `birthday`? Pentru `age`? Sau chiar pentru amândouă?

```js
const BIRTHDAY = '18.04.1982'; // make uppercase?

const AGE = someCode(BIRTHDAY); // make uppercase?
```

