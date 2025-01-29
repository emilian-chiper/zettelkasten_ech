### Meta
2024-09-18 15:10
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function sum(a, b) {
	return a + b;
}

let result = sum(1, 2);
console.log(result); // 3
```

### What it does
- A function can *return* a value back into the calling code.

### How it does it
- The directive `return` can be in any place of the function.
- When the execution reaches it, the function stops, and the value is returned to the calling code (assigned to `result` above).
- There can be many occurrences of `return` in a single function:

```JavaScript title:app.js
function checkAge(age) {
	if (age >= 18) {
		return true;
	} else {
		return confirm('Do you have permission from your   parents?)
	}
}

let age = prompt('How old are you?', 18);

if ( checkAge(age) ) {
	console.log( 'Access granted' );
} else {
	console.log( 'Access denied' );
}
```

- It is possible to use `return` without a value. That causes the function to exit immediately.

```JavaScript title:app.js
function showMovie(age) {
	if ( !checkAge(age) ) {
		return;
	}

	console.log( "Showing you the movei" );
	// ...
}
```

- In the code above, if `checkAge(age)` returns `false`, then `showMovie` won't proceed to the `console.log()`.

###### A function with an empty `return` or without it returns `undefined`
- If a function does not return a value, it is the same as if it returns `undefined`:

```JavaScript title:app.js
function doNothing() { /* empty */ }

console.log( doNothing() === undefined ); // true
```

- An empty `return` is also the same as `return undefined`:

```JavaScript title:app.js
function doNothing() {
	return;
}

console.log( doNothing() === undefined ); // true
```

###### Never add a newline between `return` and the value
- For a long expression in `return`, it might be tempting to put it on a separate line, like this:

```JavaScript title:app.js
return
	(some + long + expression + or + whatever * f(a) + f(b))
```

- That doesn't work, because JavaScript assumes a semicolon after `return`. That works the same as:

```JavaScript title:app.js
return;
	(some + long + expression + or + whatever * f(a) + f(b))
```

- So, it effectively becomes an empty return.
- If we want  the returned expression to wrap across multiple lines, we should start it at the same line as `return`, or at least put the opening parentheses there:

```JavaScript title:app.js
return (
	some + long + expression
	+ or +
	whatever * f(a) * f(b)
);
```