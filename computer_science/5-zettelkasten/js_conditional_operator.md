### Meta
2024-09-17 23:03
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_conditionals]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let result = condition ? value1 : value2;
```

### What it does
-  Executes an `if ... else` statement in a shorter format.
- Sometimes called `ternary` operator, because of its three operands.

### How it does it
- The `condition` is evaluated.
- If it's `truthy`, then `value1` is returned.
- Otherwise, `value2` is returned.

#### Multiple conditional operators
- A sequence of conditional operators can return a value that depends on more than one condition.

```JavaScript title:app.js
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
	(age < 19) ? 'Hello!' :
	(age < 100) ? 'Greetings!' :
	'Whan an unusual age';

console.log( message );
```

- Parsing the above code block, we observe:
	1) The first `?` checks whether `age < 3`.
	2) If `true`, it returns `Hi, baby!`. Otherwise, it continues to the expression after the colon `:`, checking `age < 18`.
	3) If that is `true`, it returns `Hello!`. Otherwise, it continues to the expression after the next colon `:`, checking `age < 100`.
	4) If that is `true`, it returns `Greetings!`. Otherwise, it continues to the expression after the last colon `:`, returning `What an unusual age!`.

- Here's how it looks using `if ... else`:

```JavaScript title:app.js
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

#### Non-traditional use of the conditional operator
- A sequence of conditional operators can return a value that depends on more than one condition.

```JavaScript file:app.js
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
	(age < 19) ? 'Hello!' :
	(age < 100) ? 'Greetings!' :
	'Whan an unusual age';

console.log( message );
```

- Parsing the above code block, we observe:
	1) The first `?` checks whether `age < 3`.
	2) If `true`, it returns `Hi, baby!`. Otherwise, it continues to the expression after the colon `:`, checking `age < 18`.
	3) If that is `true`, it returns `Hello!`. Otherwise, it continues to the expression after the next colon `:`, checking `age < 100`.
	4) If that is `true`, it returns `Greetings!`. Otherwise, it continues to the expression after the last colon `:`, returning `What an unusual age!`.

- Here's how it looks using `if ... else`:

```JavaScript title:app.js
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
