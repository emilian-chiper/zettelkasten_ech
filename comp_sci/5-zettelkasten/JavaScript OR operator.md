### Meta
- 2024-09-17 12:10
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript logical operators]]
- Status: #completed 

### What it looks like
```JavaScript file:app.js
result = a || b;
```

### What it does
- In classical programming, the logical OR is meant to manipulate Boolean values only.
- If any of its arguments are `true`, it `returns` true, otherwise it returns `false`.

### How it does it
- There are four possible logical combinations:

```JavaScript file:app.js
console.log( true || true ); // true
console.log( false || true ); // true
console.log( true || false ); // true
console.log( false || false ); // false
```

- If an operator is not a Boolean, it's converted to a Boolean for the evaluation.

```JavaScript file:app.js
if (1 || 0) {
	console.log( 'truthy!' );
}
```

- Most of the time, OR `||` is issued in an `if` statement to test if *any* of the given conditions is `true`. For example:

```JavaScript file:app.js
let hour = 9;

if (hour < 10 || hour > 18) {
	console.log( 'The office is closed.' );
}
```

- We can pass more than two conditions:

```JavaScript file:app.js
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
	console.log( 'The office is closed.' );
}
```

#### OR `||` finds the first `truthy` value
- The extended algorithm works as follows.
- Given multiple OR'ed values:

```JavaScript file:app.js
result = value1 || value2 || value3;
```

- The OR `||` operator does the following:
	- Evaluates operands from left to right.
	- For each operand, converts it to Boolean. If the result is `true`, stops and returns the original value of the operand.
	- If all operands have been evaluated to `false`, returns the last operand.
- A value is returned in its original form, without the conversion.
- In other words, a chain of OR `||` statements returns the first truthy value or the last one if no truthy value is found.
- For instance:

```JavaScript file:app.js
console.log( 1 || 0 ); // 1 (1 is truthy)

console.log( null || 0  || 1 ); // 1 (1 is the first truthy value)

console.log( undefined || null || 0 ); // 0 (all falsy, returns last value)
```

#### Usage
1) **Getting the first truthy value from a list of variables or expressions**
```JavaScript file:app.js
let firstName = '',
	lastName = '',
	nickName = 'SuperCoder';

console.log(
	firstName || lastName || nickname || "Anonymous" );
); // 'SuperCoder' (first truthy value encountered)
```

2) **Short-circuit evaluation**
```JavaScript file:app.js
true || console.log("not printed");
false || console.log("printed");
```

- OR `||` processes its arguments until the first `truthy` value is reached, and then the value is returned immediately, without even touching the other argument.
- In the first line, the OR `||` operator stops the evaluation immediately upon seeing `true`, so the `console.log()` isn't run.