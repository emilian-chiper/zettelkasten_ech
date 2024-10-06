### Meta
2024-09-18 22:39
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_function_expressions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
// Function Declaration
function sum(a, b) {
    return a + b;
}

// Function Expression
let sum = function(a, b) {
    return a + b;
}

```

### What it does
- A ***function declaration*** is a function declared as a separate statement, in the main code flow.
- A **function expressions*** is a function created inside an expression or other syntax construct.

### How it does it

##### Creation
- A ***function expression*** is created ***when the execution reaaches it*** and is usable only from that moment.
- A ***function declaration*** can be called **earlier than it is defined**.
- When JavaScript prepares to run the script, it first looks for global **function declarations** and creates them. We can think of it as an ***initialization stage.***
- After all function declarations are process, the code is executed.

```JavaScript title:app.js
sayHi("John"); // Hello, John

function sayHi(name) {
    alert( `Hello, ${name}` );
}
```

- If the above were a **function declaration**, we would produce an **error**.

```JavaScript title:app.js
sayHi("John"); // error

let sayHi = function(name) {
    alert( `Hello, ${name}` );
}
```

- **Function expressions** are created when the execution reaches them.

##### Scope
- In **strict mode**, when a ***function declaration*** is within a code block, it's visible everywhere inside that block, but **NOT** outside it.

```JavaScript title:app.js
let age = prompt("What is your age?", 18);

// conditionally declarea function
if (age < 18) {
	function welcome() {
		alert("Hello!");
	}
} else {
	function welcome() {
		alert("Greetings!");
	}
}

welcome(); // error: Welcome is not defined
```

- To make `welcome()` visible outside the `if` statement, we can use a ***function expression***.

```JavaScript title:app.js
let age = prompt("What is your age?", 18);

let welcome;

if (age < 18) {
  welcome = function() {
    alert("Hello!");
  };
} else {
  welcome = function() {
    alert("Greetings!");
  };
}

welcome();
```

- To simplify even further, a *ternary* operator and ***anonymous functions*** be employed:

```JavaScript title:app.js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
	function() { alert("Hello!"); } :
	function() { alert("Greetings!"); };

welcome();
```

### When to choose Declarations vs. Expressions?
- Always consider **declarations first**, as it allows more freedom in organizing code, because we can call them before declaration.
- This also improves readability.
- If a declaration is unsuitable, or we need a *conditional* declaration, use an **expression**.