### Meta
2024-09-18 10:15
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What
- Syntax constructs that are not expressions cannot be used with the ternary operator `?`.
- In particular, directives such as `break` and `continue` are **NOT ALLOWED**.

#### Example
- If we take this code:

```JavaScript title:app.js
if (i > 5) {
	console.log(i);
} else {
	continue;
}
```

... and rewrite it using the conditional operator:

```JavaScript title:app.js
(i > 5) ? console.log(i) : continue;
```

... the result will be a [`SyntaxError`]([[js_syntax_error]]).

### How it does it
Examples
