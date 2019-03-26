Task-ul demonstrează cum formele postfixată/prefixată pot duce la rezultate diferite atunci când sunt folosite în comparații.

1. **De la 1 la 4**

    ```js run
    let i = 0;
    while (++i < 5) alert( i );
    ```

    Prima valoare este `i = 1`, pentru că `++i` incrementează mai întâi pe `i` și apoi returnează noua valoare. Așadar prima comparație este `1 < 5` și `alert` afișează `1`.

    Apoi urmează `2, 3, 4…` -- valorile apar una după cealaltă. Comparația folosește întotdeauna valoarea incrementată, pentru că `++` este înaintea variabilei.

    În cele din urmă `i = 4` este incrementat la `5`, comparația `while(5 < 5)` eșuează iar bucla se oprește. Așadar `5` nu este afișat.
2. **De la 1 la 5**

    ```js run
    let i = 0;
    while (i++ < 5) alert( i );
    ```

    Prima valoare este din nou `i = 1`. Forma postfixată a lui `i++` incrementează pe `i` și returnează *vechea* valoare, așadar comparația `i++ < 5` va folosi `i = 0` (contrar lui `++i < 5`).

    Dar apelul lui `alert` este separat. Este o altă afirmație care execută după incrementare și după comparație. Așa că folosește `i = 1`.

    Apoi urmează `2, 3, 4…` 

    Să ne oprim la `i = 4`. Forma prefixată `++i` ar incrementa-o și ar folosi `5` în comparație. Dar aici avem forma postfixată `i++`. Așa că incrementează pe `i` la `5`, dar returnează vechea valoare. Așadar comparația este defapt `while(4 < 5)` -- adevărat, și controlul merge la `alert`.

    Valoarea `i = 5` este ultima, pentru că la următorul pas `while(5 < 5)` este fals.