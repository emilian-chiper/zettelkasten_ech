### Meta
2024-09-18 11:31
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
function showMessage() {
	alert( 'Hello everyone!' );
}
```

### What it does
- Declares a function.

### How it does it
- The `function` keyword goes first, followed by the *[name]([[js_naming_functions]])* of the function, then a list of *[parameters]([[js_alternative_default_parameters]])* between the parentheses (comma-separated, empty in the example above) and finally the code of the function, aka the *function body*, between curly braces.

```JavaScript title:app.js
function name(parameter1, parameter2, ... parameterN) {
	// body
}
```