### Meta
2024-09-18 09:59
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let sum = 0;

while (true) {
	let value = +prompt("Enter a number", '');
	
	if (!value) break; // (*)

	sum += value;
}
alert( 'Sum: ' + sum );
```

### What it does
- The `break` directive is at line `6` if the user enters an empty line or cancels or cancels the input.
- It stops the loop immediately, passing control to the first line after the loop. Namely, `alert`.
- The combination "infinite loop + `break` as needed" is great for situations when a loop's condition must be checked not in the beginning or end of the loop, but in the middle or even in several places of its body.