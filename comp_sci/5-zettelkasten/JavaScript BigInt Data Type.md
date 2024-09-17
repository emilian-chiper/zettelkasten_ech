### Meta
- - -
- 2024-09-16 21:50
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript data types]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
const bigInt = 1234567890123456789012345678901234567890n;
```

### What it does
- - -
- Stores values:
	- larger than `(2^53 - 1)` (which is `9007199254740991`), or
	- less than `-(2^53 - 1)`;
- Represents integers of arbitrary length.

### How it does it
---
- By appending `n` to the end of an integer.
