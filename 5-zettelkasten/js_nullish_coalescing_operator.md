### Meta
2024-09-18 07:39
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let result = a ?? b;
```

### What it does
- Returns the first argument if it's not `null` or `undefined`.

### How it does it
- Let us say that a value is `defned` when it is neither `null` nor `undefined`.
- The result of `a ?? b` is:
	- if `a` is `defined`, then `a`,
	- otherwise, `b`.
- This can be rewritten as:
```JavaScript title:app.js
let result = (a !== null && a !== undefined) ? a : b;
```

#### Use cases
- The common use case for `??` is to provide a default value. For example:
```JavaScript title:app.js
let user;

console.log(user ?? "Anonymous"); // "Anonymous"

user = "John";

console.log(user ?? "Anonymous"); // "John"
```

- We can also use a sequence of `??` to select the first value from a list that isn't `null` or `undefined`.
```JavaScript title:app.js
let firstName = null;
let lastName = null;
let nickName = "Big Chungus";

// Shows the first defined value
console.log(
	firstName ??
	lastName ??
	nickname ??
	"Anonymous"
); // Big Chungus
```

#### Comparison with ||
- The OR `||` operator can be used in the same way as `??`.
- In the code above, they produce the same result.
- The differences are:
	- `||` returns the first `truthy` value, while
	- `??` returns the first `defined` value.
- In other words, `||` doesn't distinguish between `false`, `0`, an empty string `""` and `null` or `undefined`. They are all `falsey` values. If any of these is the first argument of `||`, we'll get the second argument as the result.
- In practice, we may want to use the default value only when the variable is `null` or `undefined`. For example:

```JavaScript title:app.js
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

#### Precedence
- Both `??` and `||` have the same `level 3` precedence in the [Operator Precedence Table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#table).
- This means they are evaluated before `=` and `?`, but after most mathematical operators. Thus, parentheses may be required:

```JavaScript title:app.js
let height = null;
let width = null;

// important: use parentheses
let area = (height ?? 100) * (width ?? 50);

alert(area); // 500

// without parentheses
are = height ?? 100 * width ?? 50;

alert(area); // 50
```

#### Using `??` with `&&` or `||`
- It is **FORBIDDEN**, unless the precedence is explicitly specified with parentheses.

```JavaScript title:app.js
let x = 1 && 2 ?? 3;
alert(x); // SyntaxError

x = (1 && 2) ?? 3;
alert(x); // 2
```