### Meta
2024-09-29 21:55
**Tags:** [[javascript]]
**State:** #completed 

- JavaScript has a built-in [Math]([[js_obj_Math]]) which contains a small library of mathematical functions and constants.

`Math.random`
- Returns a random number from 0 to 1 (not including 1).

```JavaScript title:app.js
alert( Math.random() ); // 0.1234567894322
alert( Math.random() ); // 0.5435252343232
alert( Math.random() ); // ... (any random numbers)
```

`Math.max(a, b, c ...)` and `Math.min(a, b, c ...)`
- Returns the greatest and smallest from the arbitrary number of arguments.

```JavaScript title:app.js
alert( Math.max(3, 5, -10, 0, 1) ); // 5
alert( Math.min(1, 2) ); // 1
```

`Math.pow(n, power)`
- Returns `n` raised to the given `power`.

```JavaScript title:app.js
alert( Math.pow(2, 10) ); // 2 in power 10 = 1024
```