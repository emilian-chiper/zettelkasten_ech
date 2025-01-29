### Meta
2024-09-17 23:12
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_logical_operators]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
result = !value;
```

### What it does
- The operator accepts a single argument and does the following:
	- Converts the operand to Boolean type: `true` / `false`.
	- Returns the inverse value.

### How it does it
```JavaScript title:app.js
console.log( !true ); // false
console.log( !0 ); // true
```

- A double NOT `!!` is sometimes used for converting a value to Boolean type.

```JavaScript title:app.js
console.log( !!"not-empty string" ); // true
console.log( !!null ); // false
```

- In this double negation, the first `!` converts the value and returns the invers, and the second `!` inverses it again.
- The precedence of NOT `!` is highest amongst all logical operators. Thus, it always executes before either `&&` or `||`.