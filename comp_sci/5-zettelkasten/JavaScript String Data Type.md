### Meta
- - -
- 2024-09-16 22:06
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript data types]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;
```

### What it does
- - -
-  Represents a sequence of characters.

### How it does it
---
- A string in JavaScript must be surrounded by quotes.
- In JavaScript, there are double quotes, single quote, and backticks, as shown above.
- JavaScript doesn't differentiate between double and single quotes, or "simple" quotes.
- Backticks are "extended functionality" quotes, allowing us to embed variables and expressions into a string by wrapping them in `${...}`.
- **Note:** The `char` type does NOT exist in JavaScript. A string may consist of zero or multiple characters.
