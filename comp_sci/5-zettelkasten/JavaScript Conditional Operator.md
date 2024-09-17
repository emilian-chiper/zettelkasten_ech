### Meta
- - -
- 2024-09-17 11:11
- Tags: [[javascript]] [[javascript conditionals]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let result = condition ? value1 : value2;
```

### What it does
- - -
-  Executes an `if ... else` statement in a shorter format.
- Sometimes called `ternary` operator, because of its three operands.

### How it does it
---
- The `condition` is evaluated.
- If it's `truthy`, then `value1` is returned.
- Otherwise, `value2` is returned.

### Multiple `?`
- - -
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

```JavaScript file:app.js
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

### Non-traditional use of `?`
- - -
- Sometimes, `?` is used as a replacement for `if`:

```JavaScript file:app.js
let company = prompt('Which company created JavaScript?', '');

(company == 'Netscape') ?
	console.log('Right!') :
	console.log('Wrong.');
```

- Depending on the condition `company == Netscape`, either the first or the second expression after the `?` will be executed.
- **Note:** It is not recommended to use the conditional operator in this way. It is less readable than an `if` statement.