### Meta
2024-09-18 13:23
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function showMessage(from, text) {
	console.log(from + ": " + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello!
showMessage('Ann', "What's up?"); // Ann: What's up?
```

### What it does
- We can pass arbitrary data to functions using parameters (i.e. `from` and `text`).

### How it does it
- When the function is called on lines `5` and `6`, the given values are copied to the local variables `form` and `text`. Then the function uses them.
- Another example:

```JavaScript title:app.js
function showMessage(from, text) {
	from = '*' + from + '*';
	console.log( from + ': ' + text);
}

let from = 'Ann';

showMessage(from, 'Hello'); // *Ann*: Hello

console.log(from); // Ann
```

- When a value is passed as a function parameter, its' called an **argument**.
- In other words:
	- A *parameter* is a variable listed inside the parentheses in the function declaration (i.e. it's a *declaration time term*).
	- An *argument* is the value that is passed to the function when it is called (i.e. it's a *call time term*).
- We declare functions listing their parameters, then call them passing arguments.