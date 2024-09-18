### Meta
2024-09-18 13:32
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
function showMessage(from, text = 'no text given') {
	console.log( frm + ": " + text);
}

showMessage("Ann"); // Ann: no text given
```

### What it does
- Assigns a default value to a function parameter.

### How it does it
- If a function is called, but an argument is not provided, the corresponding value becomes `undefined`. That is NOT an error.
- We can specify the so-called 'default' (to use if omitted) value for a parameter using the assignment operator `=` in the function declaration.
- If the parameter is not passed, it will get and use the default value.
- The default value also jumps in if the parameter exists, but strictly equals `undefined`, like so:

```JavaScript title:app.js
showMessage("Ann", undefined); // Ann: no text given
```

- More complex expressions can also be assigned as default parameters.

```JavaScript title:app.js
function showMessage(from, text = anotherFunction());
```

#### Evaluation of default parameters
