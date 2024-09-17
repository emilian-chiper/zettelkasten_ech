### Meta
- - -
- 2024-09-16 21:39
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript data types]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let num = 123;
```

### What it does
- - -
- Represents both `integer` (whole) and `floating point` (decimal) numbers.
- Support basic arithmetic operations.

### Special numeric values
---
- `Infinity`
	- Represents the mathematical infinity.
	- Can be obtained as a result of division by zero.
	- Can also be referenced directly.

```JavaScript file:app.js
console.log(1 / 0); // Infinity
console.log( Infinity ); // Infinity
```

- `NaN`
	- Represents a computational error.
	- Results after an incorrect or undefined mathematical operation.
	- Is sticky. Any further mathematical operation with `Nan` returns `NaN`.

```JavaScript file:app.js
console.log("not a number" / 2); // NaN
console.log( NaN + 1 ); // NaN
console.log( 3 * NaN ); // NaN
console.log( "not a number" / 2 - 1 ); // NaN
```


