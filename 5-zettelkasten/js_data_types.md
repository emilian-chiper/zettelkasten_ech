### Meta
2024-09-17 22:25
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### Number
#### What it looks like
```JavaScript title:app.js
let num = 123;
```
#### What it does
- Represents both `integer` (whole) and `floating point` (decimal) numbers.
- Support basic arithmetic operations.

#### Special numeric values
`Infinity`
	- Represents the mathematical infinity.
	- Can be obtained as a result of division by zero.
	- Can also be referenced directly.

```JavaScript title:app.js
console.log(1 / 0); // Infinity
console.log( Infinity ); // Infinity
```

- `NaN`
	- Represents a computational error.
	- Results after an incorrect or undefined mathematical operation.
	- Is sticky. Any further mathematical operation with `Nan` returns `NaN`.

```JavaScript title:app.js
console.log("not a number" / 2); // NaN
console.log( NaN + 1 ); // NaN
console.log( 3 * NaN ); // NaN
console.log( "not a number" / 2 - 1 ); // NaN
```

### BigInt
#### What it looks like
```JavaScript title:app.js
const bigInt = 1234567890123456789012345678901234567890n;
```

#### What it does
- Stores values:
	- larger than `(2^53 - 1)` (which is `9007199254740991`), or
	- less than `-(2^53 - 1)`;
- Represents integers of arbitrary length.

#### How it does it
- By appending `n` to the end of an integer.

### String
#### What it looks like
```JavaScript title:app.js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;
```

#### What it does
-  Represents a sequence of characters.

#### How it does it
- A string in JavaScript must be surrounded by quotes.
- In JavaScript, there are double quotes, single quote, and backticks, as shown above.
- JavaScript doesn't differentiate between double and single quotes, or "simple" quotes.
- Backticks are "extended functionality" quotes, allowing us to embed variables and expressions into a string by wrapping them in `${...}`.
- **Note:** The `char` type does NOT exist in JavaScript. A string may consist of zero or multiple characters.

### Boolean
#### What it looks like
```JavaScript title:app.js
let nameFieldChecked = true;
let ageFieldChecked = false;

let isGreater = 4 > 1;
console.log(isGreater); // true
```

#### What it does
-  Stores yes/no values:
	- `true` means 'yes, correct', and
	- `false` means 'no, incorrect.'.
- Also come as a result of comparisons.

### null
#### What it looks like
```JavaScript title:app.js
let age = null;
```

#### What it does
-  Is its own type.
- Is **NOT** a 'reference to a non-existing object' or a 'null pointer'.
- Is a special value which represents 'nothing', 'empty', or 'value unknown'.

### undefined
#### What it looks like
```JavaScript title:app.js
let age;

console.log(age); // "undefined"
```

#### What it does
- Is its own type, like `null`.
- Means 'value not assigned'.
- Can be explicitly assigned to a variable, but is **NOT** recommended. Instead:
	- use `null` to assign an 'empty' or 'unknown' value to a variable, and
	- reserve `undefined` as a default initial value.

### Object
#### What it does
-  Is a special type reserved for complex logic.
- All other types are called `primitive` because their values can contain only a single value.
- In contrast, objects are used to store collections of data and more complex entities.