### Meta
2024-09-17 22:43
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### Terms: "unary", "binary", "operand"
**Operand**
	- A term of the mathematical expression, basically what operators are applied to.
	- In `5 * 2` the operands are `5` and `2`.
	- Sometimes called "arguments" instead of "operands".
- **Unary operators**
	- Have a single operand.
	- For example, the unary negation `-` reverses the sign of a number:

```JavaScript title:app.js
let x = 1;

x = -x;
console.log( x ); // -1, unary negation was applied
```

- **Binary operators**
	- Have two operands.
	- The same `-` exists in binary form as well:

```JavaScript title:app.js
let x = 1,
	y = 3;
console.log( y - x ); // 2, binary minus substracts values
```

### Mathematical operations
-  The following mathematical operations are supported:
	- Addition `+`,
	- Subtraction `-`,
	- Multiplication `*`,
	- Division `/`,
	- Remainder `%`,
	- Exponentiation `**`.
- The first four are straightforward.

#### Remainder `%`
- The result of `a % b` is the remainder of the integer division `a` by `b`.

```JavaScript title:app.js
console.log( 5 % 2 ); // 1, the remainder of 5 divided by 2
console.log( 8 % 3 ); // 2, the remainder of 8 divided by 3
console.log( 8 % 4); // 0, the remainder of 8 divided by 4
```

#### Exponentiation `**`
- The exponentiation operator `a ** b` raises `a` to the power of `b`.

```JavaScript title:app.js
console.log( 2 ** 4); // 16
```

- The exponentiation operator is defined for non-integer numbers as well.

```JavaScript title:app.js
console.log( 4 ** (1/2) ); // 2
console.log( 8 ** (1/3)); // 2
```

### String Concatenation with Binary +
```JavaScript title:app.js
let s = "my" + "string";
console.log(s); // mystring
```

### Numeric Conversion, Unary +
- If applied to a single value, doesn't do anything to numbers.
- If the operand is not a number, the unary plus converts it into a number.
- It does the same thing as `Number(...)`, but is shorter.

```JavaScript title:app.js
// No effect on numbers
let x = 1;
console.log( +x ); // 1

let y = -2;
console.log( +y ); // -2

// Converts non-numbers
console.log( +true ); // 1
console.log( +""); // 0
```

- The need to convert strings to numbers arises very often. For example, if we're getting values from HTML form fields, they are usually string. What if we want to sum them?
- The binary plus would produce concatenation.

```JavaScript title:app.js
let apples = "2";
let oranges = "3";

console.log( apples + oranges ); // "23"
```

- If we want to treat them as numbers, we must first convert them.

```JavaScript title:app.js
let apples = "2";
let oranges = "3";

// Both values converted to numbers before the binary plus
console.log( +apples + +oranges); // 5
```

### Operator Precedence
- See: [Operator Precedence Table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#table)

