### Meta
- - -
- 2024-09-17 11:02
- Tags: [[javascript]] [[javascript conditionals]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year < 2015) {
	console.log( 'Too early...' );
} else if (year > 2015) {
	console.log( 'Too late' );
} else {
	console.log( 'Exactly!' );
}
```

### What it does
- - -
-  Allows us to test several variants of a condition.

### How it does it
---
- In the code above, JavaScript first checks `year < 2015`.
- If that is `falsy`, it goes to the next condition `year > 2015`.
- If that is also `falsy`, it executes the last `console.log()`.
- There can be multiple `else if` blocks. The final `else` is optional.