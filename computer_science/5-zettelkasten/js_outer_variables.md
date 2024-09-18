### Meta
2024-09-18 13:15
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let userName = 'Jon';

function showMessage() {
	let message = 'Hello, ' + userName;
	console.log(message);
}

showMessage(); // Hello, John
```

### What it does
- A function can access an outer variable.

### How it does it
- The function has full access to the outer variable. It can modify it.

```JavaScript title:app.js
let userName = 'Jon';

function showMessage() {
	userName = 'Bob'; // changes the outer variable
}

console.log(userName); // Jon
showMessage();
console.log(userName); // Bob
```

- The outer variable is used if there is no local one.

#### Edge case
- If a same-named variable is declared inside the function, then it *shadows* the outer one.

```JavaScript title:app.js
let userName = 'Jon'; // declare outer variable

function showMessage() {
	let userName = 'Bob'; // declare local variable

	let message = 'Hello, ' + userName;
	console.log(message);
}

/*
The function creates and uses its own userName.
This is called 'scoping'
**/
showMessage(); // Hello, Bob

console.log(userName); // Jon
```

#### Global variables
- Variables declared outside of any function, such as the outer `userName` in the code above, are called **global** variables.
- They are visible from any function (unless shadowed by locals).
- **Best practice:*** minimize the usage of global variables.