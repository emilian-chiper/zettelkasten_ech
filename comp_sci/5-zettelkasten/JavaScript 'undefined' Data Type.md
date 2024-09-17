### Meta
- - -
- 2024-09-16 22:25
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript data types]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let age;

console.log(age); // "undefined"
```

### What it does
- - -
- Is its own type, like `null`.
- Means 'value not assigned'.
- Can be explicitly assigned to a variable, but is **NOT** recommended. Instead:
	- use `null` to assign an 'empty' or 'unknown' value to a variable, and
	- reserve `undefined` as a default initial value.

### How it does it
---
- Like so
