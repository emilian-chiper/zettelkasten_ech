### Meta
2024-09-18 22:17
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_function_expressions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let sayHi = function() {
	alert( "Hello" );
}
```

### What it does
- Allows the creation of a new function in the middle of any expression.

### How it does it
- Function creation happens in the context of the assignment expression (to the right side of `=`).
- There is no `name` for the `function` keyword. This is allowed.
