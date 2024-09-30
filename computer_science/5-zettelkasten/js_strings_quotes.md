### Meta
2024-09-29 22:08
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_strings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let singe = 'single-quoted';
let double = "double-quoted";
let backticks = `backticks`;
```

### What it does
- Single and double quotes are the same.
- Backticks allow us to embed any expression into the string, by wrapping it in `${...}`.


### How it does it

```JavaScript title:app.js
function sum(a, b) {
	return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3
```

- Another advantage of backticks is that they allow a string to span multiple lines.

```JavaScript title:app.js
let guestList = `Guest:
  * John
  * Pete
  * Mary
`;

alert(guestList); // a list of guests, mutiple lines
```