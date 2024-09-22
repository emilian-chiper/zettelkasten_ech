### Meta
2024-09-18 22:21
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_function_expressions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function sayHi() { // (1)
	alert( "Hello" );
}

let func = sayHi; // (2)

func(); // Hello
sayHi(); // Hello
```

### What it does
- In JavaScript, a function is a value, so we can deal with it as a value.
- Here's what happens above:
	1) The function declaration `(1)` creates the function and puts into the variable named `sayHi`.
	2) Line `(2)` copies it into the variable `func`. Note that there are no parentheses afte `sayHi`. If there were, then `func = sayHi()` would write *the result of the call* `sayHi()` into `func`, not *the function* `sayHi` itself.
	3) Now the function can be called as both `sayHi()` and `func()`.
- We can also use a function expression to declare `sayHi` in the first line.

```JavaScript title:app.js
let sayHi = function() {
	alert( "Hello" );
};

let func = sayHi;
// ...
```

#### Why is there a semicolon at the end?
- A function expression is create here as `function(...) {...}` inside the assignment `let sayHi = ...;`.
- The semicolon `;` is recommended at the end of the statement, but is not part of the function syntax.
- The semicolon would be there for a simple assignment, like `let sayHi = 5;`, ad is also there for a function assignment.
