### Meta
2024-09-18 10:33
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
switch(x) {
	case 'value1': // if (x === 'value1')
		...
		break;
	case 'value2': // if (x === 'value2)
		...
		break;
	default:
		...
		break;
}
```

### What it does
- Can replace multiple `if` checks.
- Provides a more descriptive way to compare a value with multiple variants.

### How it does it
- The value of `x` is checked for a strict equality to the value from the first `case`, then the second, and so on.
- If the equality is found, `switch` executes the code starting from the corresponding `case`, until the nearest `break` (or until the end of `switch`).
- If no case is matched, then the `default` code is executed (if it exists).

#### A concrete example

```JavaScript title:app.js
let a = 2 + 2;

switch (a) {
	case 3:
		console.log( 'Too small' );
		break;
	case 4:
		console.log( 'Exactly!' ); // this executes
		break;
	case 5:
		console.log( 'Too big' );
		break;
	default:
		console.log( "I don't know such values" );
}
```

#### Exception: no `break`
- **If there is no `break` then the execution continues with the next `case` without any checks.**

```JavaScript title:app.js
let a = 2 + 2;

switch (a) {
	case 3:
		console.log( 'Too small' );
	case 4:
		console.log( 'Exactly!' ); // this executes
	case 5:
		console.log( 'Too big' );
	default:
		console.log( "I don't know such values" );
}
```

- This produces the sequential execution of three `console.log()`s :

```JavaScript title:app.js
console.log( 'Exactly!' );
console.log( 'Too big' );
console.log( "I don't know such values" );
```

#### Any expression can be a `switch/case` argument
- Both `switch` and `case` allow arbitrary expressions.

```JavaScript title:app.js
let a = "1";
let b = 0;

switch (+a) {
	case b + 1:
		console.log("this runs, because +a is 1, exactly equals b+1");
		break;
	default:
		console.log("this doesn't run");
}
```

- Here `+a` gives `1`, which is compared with `b + 1` in `case`, and the corresponding code is executed.

#### Grouping of "case"
- Several variants of `case` which share the same code can be grouped.
- For example, if we want the same code to run for `case 3` and `case 5`:

```JavaScript title:app.js
let a = 3;

switch (a) {
	case 4:
		alert('Right!');
		break;

	case 3: // grouped two cases
	case 5:
		alert('Wrong!');
		alert("Why don't you take a math class?");
		break;

	default:
		alert('The result is strange. Really.')'
}
```

- Now both `3` and `5` show the same message.
- The ability to "group" cases is a side effect of how `switch/case` works without `break`. Here, the execution of `case 3` starts from line `8` and goes through `case 5` because there's no `break`.

#### Type matters
- The equality check is **always strict**.
- The values must be of the same type to match.

```JavaScript title:app.js
let arg = prompt("Enter a value?");

switch (arg) {
	case '0':
	case '1':
		alert( 'One or zero' );
		break;
	case '2':
		alert( 'Two' );
		break;
	case 3:
		alert( 'Never executes!' );
		break;
	default:
		alert( 'An unknown value' );
}
```

1) For `0`, `1`, the first `alert` runs.
2) For `2` the second `alert` runs.
3) For `3`, the result of the `prompt` is a string `"3"`, which is not strictly equal `===` to the number `3`. So we've got a dead code in `case 3`!
4) The `default` value will execute.