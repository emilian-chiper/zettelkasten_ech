### Meta
2024-09-18 10:10
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
for (let i = 0; i < 10; i++) {

	// if true, skip the remaining part of the body
	if (i % 2 === 0) continue;

	console.log(i); // 1 3 5 7 9
}
```

### What it does
- Is a 'lighter' version of `break`.
- It doesn't stop the whole loop.
- It stops the current iteration and forces the loop to start a new one (if the condition allows).

#### Decrease nesting
```JavaScript title:decrease_nesting.js
for (let i = 0; i < 10; i++) {
	if (i % 2) {
		console.log(i);
	}
}
```
- This does the same as the example above, with extra nesting.

#### Warning
- See [[js_no_conditional_break_continue]]
- 