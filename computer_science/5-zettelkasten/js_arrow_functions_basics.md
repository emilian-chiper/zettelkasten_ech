### Meta
2024-09-19 11:05
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_arrow_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let func = (arg1, arg2, ..., argN) => expression;
```

### What it does
- Creates a function `func` that accepts arguments `arg1, ..., argN`, then evaluates the expression on the right side with their use and returns its result.

### How it does it
```JavaScript title:app.js
let sum = (a, b) => a + b;

/*
This is a shorter form of:

let sume = function(a, b) {
	return a + b;
}
**/

alert( sum(1, 2) ); // 3
```

- If we have only one parameter, the parentheses around it can be omitted.

```JavaScript title:app.js
let double = n => n * 2;

alert( double(3) ); // 6
```

- If there are no parameters, parentheses are empty,  but must be present.

```JavaScript title:app.js
let sayHi = () => alert("Hello!");

sayHi();
```

- Arrow functions can be used in the same way as function ***expressions***, as in dynamically creating a function.

```JavaScript title:app.js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
	() => alert('Hello!') :
	() => alert("Greetings!");

welcome();
```