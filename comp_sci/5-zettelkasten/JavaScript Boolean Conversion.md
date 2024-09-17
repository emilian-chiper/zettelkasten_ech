### Meta
- - -
- 2024-09-17 10:52
- Tags: [[javascript]] [[javascript conditionals]]
- Status: #pending

### What it looks like
- - -
```JavaScript file:app.js
if (0) { // 0 is falsy
	...
}

if (1) { // 1 is truthy
	...
}
```

### What it does
- - -
- The `if (...)` statement evaluates the expression in its parentheses and converts the result to a boolean.
- Per the [[JavaScript Type Conversion#Conversion rules]]:
	- A number `0`, an empty string `""`, `null`, `undefined`, and `NaN` all become `false`, for which they are called **falsy** values.
	- Other values become `true`, so they are called **truthy**.
- Thus,
	- the code at `line 1` would never execute, and
	- the code at `line 4` will always execute.
- We can also pass a pre-evaluated Boolean value to `if`, like so:

```JavaScript file:app.js
let cond = (year == 2015);

if (cond) {
	...
}
```

### How it does it
---
- Like so
