### Meta
- - -
- 2024-09-17 08:44
- Tags: [[javascript]] [[javascript fundamentals]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
console.log( 2 > 1 ); // true
console.log( 2 == 1 ); // false
console.log( 2 != 1 ); // true
```

### Supported Operators
- - -
- The following operators are supported:
	- Greater than `>`
	- Lesser than `<`
	- Greater than or equal `>=`
	- Less than or equal `<=`
	- Equality `==`
	- Inequality `!=`
	- Strict equality `===`
	- Strict inequality `!==`

### How they work
---
- All comparison operators return a Boolean value:
	- `true`
	- `false`
- A comparison result can be assigned to a variable:

```JavaScript file:app.js
let result = 5 > 4; // assign the identifier 'result' to the value of 'true' stored in memory
console.log( result ); // true
```

### String comparison
- - -
- To see if a string is greater than another, JavaScript uses the **dictionary** or **lexicographical** order.
- That is, strings are compared letter-by-letter.

```JavaScript file:app.js
console.log( 'Z' > 'A' ); // true
console.log( 'Glow' > 'Glee' ); // true
console.log( 'Bee' > 'Be' ); // true
```

#### Comparison algorithm
1) Compare the first character of both strings.
2) If the first character from the first string is greater (or lesser) than the other string's, then the first string is greater (or lesser) than the second. We're done.
3) Otherwise, if both strings' first characters are the same, compare the second characters the same way.
4) Repeat until the end of either string.
5) If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.

#### Not a real dictionary, but Unicode order
- The comparison algorithm given above is roughly equivalent to the one used in dictionaries or phone books, but it's not exactly the same.
- Case matters:
	- `"A"` is lesser than the lowercase `"a"`. Why?
		- `"a"` has a greater index in the internal encoding table JavaScript uses (Unicode).

### Comparison of different types
- - -
- When comparing values of different types, JavaScript converts the values to numbers.

```JavaScript file:app.js
console.log( '2' > 1 ); // true, '2' becomes 2
console.log( '01' == 1 ); // true, '01' becomes 1
```

- For Boolean values, `true` becomes `1` and `false` becomes `0`.

```JavaScript file:app.js
console.log( true == 1 ); // true
console.log( false == 0 ); // true
```

#### An Unexpected Consequence
- It is possible that at the same time:
	- Two values are equal.
	- One of them is `true` as a Boolean and the other one is `false` as a Boolean.

```JavaScript file:app.js
let a = 0;
console.log( Boolean(a) ); // false

let b = "0";
console.log( Boolean(b) ); // true

alert( a == b); // true (only possible with "loose" equality)
```

### Strict Equality
- - -
- A regular equality check `==` cannot differentiate `0` from `false`.

```JavaScript file:app.js
console.log( 0 == false ); // true
```

- The same thing happens with an empty string:

```JavaScript file:app.js
console.log( '' == false); // true
```

- This happens because operands of different types are converted to numbers by the equality operator `==`.
- An empty string, just like `false`, becomes zero.
- **A strict equality operator `===` checks the equality without type conversion.**
- In other words, if `a` and `b` are of different types, then `a === b` immediately returns `false` without an attempt to convert them.

```JavaScript file:app.js
console.log( 0 === false ); // false
```

### Comparison with `null` and `undefined`
---
- There is a non-intuitive behavior when `null` and `undefined` are compared to other values.
- **For a strict equality check `===`**
	- These values are different, because each is a different type.

```JavaScript file:app.js
console.log( null === undefined ); // false
```

- **For a non-strict check `==`**
	- They equal each other but not any other value.

```JavaScript file:app.js
console.log( null == undefined ); // true

```

- **For mathematics and other comparisons `< > <= >=`**
	- `null`/`undefined` are converted to numbers:
		- `null` becomes `0`
		- `undefined` becomes `NaN`.

#### Strange result: `null` vs `0`
```JavaScript file:app.js
console.log( null > 0 ); // false
console.log( null == 0 ); // false
console.log( null >= 0 ); // true
```

- **Rationale:**
	- Comparisons convert `null` to a number, treating it as `0`, thus
	- `null >= 0` is `true`, and
	- `null > 0` is `false`.

#### An incomparable `undefined`
- The value `undefined` should NOT be compared to other values.

```JavaScript file:app.js
console.log( undefined > 0 ); // false
console.log( undefined < 0 ); // false
console.log( undefined == 0 ); // false
```

- **Rationale**:
	- Comparisons `(1)` and `(2)` return `false` because `undefined` gets converted to `NaN` and `NaN` is a special numeric value which returns `false` for all comparisons.
	- The equality check `(3)` returns `false` because `undefined` only equals `null`, `undefined`, and **no other value**.

#### Rules of thumb
- Treat comparisons with `undefined`/`null` except the strict equality `===` with exceptional care.
- Do NOT use comparisons `>= > < <=` with a variable which might be `null`/`undefined`, unless you really know what you're doing. If a variable can have these values, check for them separately.