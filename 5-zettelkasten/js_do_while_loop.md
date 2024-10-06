### Meta
2024-09-18 09:34
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
do {
	// loop body
} while (condition);
```

### What it does
- Loops through an iterable.

### How it does it
- The loop will first execute the body, then check the condition, and, while it's `truthy`, execute it again and again.

```JavaScript title:app.js
let i = 0;
do {
	console.log( i );
	i++;
} while (i < 3);
```

#### Use case
- Only when you want the body of the loop to execute **at least once**, regardless of the condition being truthy.
- Usually, the other form (`while(...) {...}`) is preferred.