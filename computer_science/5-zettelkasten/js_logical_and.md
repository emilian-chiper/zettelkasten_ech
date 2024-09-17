### Meta
2024-09-17 23:10
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_logical_operators]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
result = a && b;
```

### What it does
-  In classical programming, AND returns `true` if **both** operands are truthy and `false` otherwise.

### How it does it
- There are four possible logical combinations:

```JavaScript title:app.js
console.log( true && true ); // true
console.log( false && false ); // false
console.log( true && false ); // false
console.log( false && false); // false
```

- An example using `if`:

```JavaScript title:app.js
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
	console.log( 'The time is 12:30' );
}
```

#### OR `||` find the first `truthy` value
- The extended algorithm works as follows.
- Given multiple AND'd values:

```JavaScript title:app.js
result = value1 && value2 && value3;
```

- The AND `&&` operator does the following:
	- Evaluates operands from left to right.
	- For each operand, converts it to a Boolean. If the result is `false`, stops and returns the original value of that operand.
	- If all all operands have been evaluated (i.e. all were `truthy`), returns the last operand.
- In other words, AND returns the first `falsey` value or the last value if none were found.
- Examples:

```JavaScript title:app.js
// if the first operand is truthy,
// AND returns the second operand
console.log( 1 && 0 ); // 0
console.log( 1 && 5 ); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
console.log( null && 5 ); // null
console.log( 0 && "no matter what" ); // 0
```

- We can also pass several values in a row.

```JavaScript title:app.js
console.log( 1 && 2 && null && 3 ); // null
```

- When all values are `truthy`, the last value is returned:

```JavaScript title:app.js
console.log( 1 && 2 && 3 ); // 3
```

- **Note:** The precedence of AND `&&` is higher than OR `||`.
- The code `a && b || c && d` is the same as `(a && b) || (c && d)`.

#### Don't replace `if` with `||` or `&&`
- Sometimes, people use AND `&&` as a shorter way to write `if`. For instance:

```JavaScript title:app.js
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

- The action in the right part of `&&` would execute only if the evaluation reaches it. This is an analogue for:

```JavaScript title:app.js
let x = 1;

if (x > 0) alert( 'Greater than zero!' );
```

- Although the variant with `&&` appears shorter, `if` is more obvious and more readable.
