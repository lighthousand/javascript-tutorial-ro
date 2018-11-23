
```js no-beautify
"" + 1 + 0 = "10" // (1)
"" - 1 + 0 = -1 // (2)
true + false = 1
6 / "3" = 2
"2" * "3" = 6
4 + 5 + "px" = "9px"
"$" + 4 + 5 = "$45"
"4" - 2 = 2
"4px" - 2 = NaN
7 / 0 = Infinity
" -9\n" + 5 = " -9\n5"
" -9\n" - 5 = -14
null + 1 = 1 // (3)
undefined + 1 = NaN // (4)
```

1. The addition with a string `"" + 1` converts `1` to a string: `"" + 1 = "1"`, and then we have `"1" + 0`, the same rule is applied.
2. Scăderea `-` (ca majoritatea operațiilor matematice) funcționeză doar cu numere, convertește un string gol `""` la `0`.
3. `null` devine `0` după conversia numerică.
4. `undefined` devine `NaN` după conversia numerică.