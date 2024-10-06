### Meta
2024-09-18 08:14
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
while (condition) {
	// code
	// so-called "loop body"
}
```

### What it does
- While the `condition` is truthy, the `code` from the loop body is executed.
### How it does it
 - The loop below outputs `i` while `i < 3`:

```JavaScript title:app.js
let i = 0;
while (i < 3) { // prints 0, then 1, then 2
	console.log( i );
	i++;
}
```

- A single execution of the loop body is called an ***iteration***. The loop above makes 3 iterations.
- If `i++` were absent, the loop repeat ad infinitum. In practice, the browser provides ways to stop such loops, and in server-side JavaScript the process can be killed.
- Any expression or variable can be a loop condition, not just comparisons -- the condition is evaluated and converted to a Boolean by `while`.
- For instance, a shorter way to write `while (i != 0)` is `while (i)`.
- **Note:** Curly braces are not required for a single line body.

```JavaScript title:app.js
let i = 3;
while (i) console.log(i--);
```
