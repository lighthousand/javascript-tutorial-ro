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

It actually does the same as `Number(...)`, but is shorter.

A need to convert strings to numbers arises very often. For example, if we are getting values from HTML form fields, then they are usually strings.

What if we want to sum them?

The binary plus would add them as strings:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

If we want to treat them as numbers, then we can convert and then sum:

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

From a mathematician's standpoint the abundance of pluses may seem strange. But from a programmer's standpoint, there's nothing special: unary pluses are applied first, they convert strings to numbers, and then the binary plus sums them up.

Why are unary pluses applied to values before the binary one? As we're going to see, that's because of their *higher precedence*.

## Operators precedence

If an expression has more than one operator, the execution order is defined by their *precedence*, or, in other words, there's an implicit priority order among the operators.

From school we all know that the multiplication in the expression `1 + 2 * 2` should be calculated before the addition. That's exactly the precedence thing. The multiplication is said to have *a higher precedence* than the addition.

Parentheses override any precedence, so if we're not satisfied with the order, we can use them, like: `(1 + 2) * 2`.

There are many operators in JavaScript. Every operator has a corresponding precedence number. The one with the bigger number executes first. If the precedence is the same, the execution order is from left to right.

An extract from the [precedence table](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence) (you don't need to remember this, but note that unary operators are higher than corresponding binary ones):

| Precedence | Name | Sign |
|------------|------|------|
| ... | ... | ... |
| 16 | unary plus | `+` |
| 16 | unary negation | `-` |
| 14 | multiplication | `*` |
| 14 | division | `/` |
| 13 | addition | `+` |
| 13 | subtraction | `-` |
| ... | ... | ... |
| 3 | assignment | `=` |
| ... | ... | ... |

As we can see, the "unary plus" has a priority of `16`, which is higher than `13` for the "addition" (binary plus). That's why in the expression `"+apples + +oranges"` unary pluses work first, and then the addition.

## Assignment

Let's note that an assignment `=` is also an operator. It is listed in the precedence table with the very low priority of `3`.

That's why when we assign a variable, like `x = 2 * 2 + 1`, then the calculations are done first, and afterwards the `=` is evaluated, storing the result in `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

It is possible to chain assignments:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Chained assignments evaluate from right to left. First the rightmost expression `2 + 2` is evaluated then assigned to the variables on the left: `c`, `b` and `a`. At the end, all variables share a single value.

````smart header="The assignment operator `\"=\"` returns a value"
An operator always returns a value. That's obvious for most of them like an addition `+` or a multiplication `*`. But the assignment operator follows that rule too.

The call `x = value` writes the `value` into `x` *and then returns it*.

Here's the demo that uses an assignment as part of a more complex expression:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

In the example above, the result of `(a = b + 1)` is the value which is assigned to `a` (that is `3`). It is then used to subtract from `3`.

Funny code, isn't it? We should understand how it works, because sometimes we can see it in 3rd-party libraries, but shouldn't write anything like that ourselves. Such tricks definitely don't make the code clearer and readable.
````

## Remainder %

The remainder operator `%` despite its look does not have a relation to percents.

The result of `a % b` is the remainder of the integer division of `a` by `b`.

For instance:

```js run
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

## Exponentiation **

The exponentiation operator `**` is a recent addition to the language.

For a natural number `b`, the result of `a ** b` is `a` multiplied by itself `b` times.

For instance:

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

The operator works for non-integer numbers of `a` and `b` as well, for instance:

```js run
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

## Increment/decrement

<!-- Can't use -- in title, because built-in parse turns it into – -->

Increasing or decreasing a number by one is among the most common numerical operations.

So, there are special operators for that:

- **Increment** `++` increases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter++;      // works the same as counter = counter + 1, but is shorter
    alert( counter ); // 3
    ```
- **Decrement** `--` decreases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter--;      // works the same as counter = counter - 1, but is shorter
    alert( counter ); // 1
    ```

```warn
Increment/decrement can be applied only to a variable. An attempt to use it on a value like `5++` will give an error.
```

Operators `++` and `--` can be placed both after and before the variable.

- When the operator goes after the variable, it is called a "postfix form": `counter++`.
- The "prefix form" is when the operator stands before the variable: `++counter`.

Both of these records do the same: increase `counter` by `1`.

Is there any difference? Yes, but we can only see it if we use the returned value of `++/--`.

Let's clarify. As we know, all operators return a value. Increment/decrement is not an exception here. The prefix form returns the new value, while the postfix form returns the old value (prior to increment/decrement).

To see the difference, here's the example:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

Here in the line `(*)` the prefix call `++counter` increments `counter` and returns the new value that is `2`. So the `alert` shows `2`.

Now let's use the postfix form:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

In the line `(*)` the *postfix* form `counter++` also increments `counter`, but returns the *old* value (prior to increment). So the `alert` shows `1`.

To summarize:

- If the result of increment/decrement is not used, then there is no difference in which form to use:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- If we'd like to increase the value *and* use the result of the operator right now, then we need the prefix form:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- If we'd like to increment, but use the previous value, then we need the postfix form:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement among other operators"
Operators `++/--` can be used inside an expression as well. Their precedence is higher than most other arithmetical operations.

For instance:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compare with:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Though technically allowable, such notation usually makes the code less readable. One line does multiple things -- not good.

While reading the code, a fast "vertical" eye-scan can easily miss such `counter++`, and it won't be obvious that the variable increases.

The "one line -- one action" style is advised:

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Bitwise operators

Bitwise operators treat arguments as 32-bit integer numbers and work on the level of their binary representation.

These operators are not JavaScript-specific. They are supported in most programming languages.

The list of operators:

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
