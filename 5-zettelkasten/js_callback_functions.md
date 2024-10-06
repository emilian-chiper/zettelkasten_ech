### Meta
2024-09-18 22:29
**Tags:** [[javascript]] [[javascript_fundamentals]] [[js_function_expressions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function ask(question, yes, no) {
	if (confirm(question)) yes()
	else no();
}

function showOk() {
	alert( "You agreed." );
}

function showCancel() {
	alert( "You canceled the execution." );
}

ask("Do you agree?", showOk, showCancel);
```

### What it does
- Passes functions as values to other functions.

### How it does it
- The arguments `showOk` and `showCancel` of `ask` are called ***callback functions*** or simply ***callbacks***.
- The idea is that we pass a function and expect it to be "called back" later if necessary.
- We can use function expressions to write an equivalent, shorter version:

```JavaScript title:app.js
function ask(question, yes, no) {
	if (confirm(question)) yes()
	else no();
}

ask(
	"Do you agree?",
	function() { alert("You agreed."); },
	function() { alert("You canceled the execution."); }
)
```

- Here, functions are declared inside the `ask(...)` call.
- They have no name, and are thus called ***anonymous functions***.
- They are not accessible outside of `ask` (because they are not assigned to variables).

###### A function is a value representing an action
- Regular values like strings or numbers represent the *data*.
- A function can be perceived as an *action*.
- We can pass it between variables and run when we want.