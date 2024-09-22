### Meta
2024-09-18 09:44
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
for (begin; condition; step) {
	// ... loop body ...
}
```

### What it does
- Loops over an iterable.

### How it does it
```JavaScript title:app.js
for (let i = 0; i < 3; i++) { // 0, then 1, then 2
	console.log(i);
}
```

| **part**  |                  |                                                                        |
| --------- | ---------------- | ---------------------------------------------------------------------- |
| begin     | `let i = 0`      | Executes once upon entering the loop.                                  |
| condition | `i < 3`          | Checked before every every loop iteration. If `false`, the loop stops. |
| body      | `console.log(i)` | Runs again again while the condition is `truthy`.                      |
| step      | `i++`            | Executes after the body on each iteration.                             |
- The general loop algorithm works like this:
```
Run begin
-> (if condition -> run body and run step)
-> (if condition -> run body and run step)
-> (if condition -> run body and run step)
-> ...
```

- That is, `begin` executes once, then it iterates: after each `condition` test, `body` and `step` are executed.

#### Inline variable declaration
- Here, the `counter` variable `i` is declared right in the loop. This is called an "inline" variable declaration. Such variables are visible only inside the loop.
```JavaScript title:app.js
for (let i = 0; i < 3; i++) {
	console.log(i); // 0 1 2
}
console.log(i); // error, no such variable
```

Instead of defining a variable, we can use an existing one:
```JavaScript title:app.js
let i = 0;

for (i = 0; i < 3; i++) {
	console.log(i); // 0 1 2
}
console.log(i); // 3
```

#### Skipping parts
- Any part of `for` can be skipped.

```JavaScript title:skip_begin.js
let i = 0;

for (; i < 3; i++) { // no need for begin
	console.log(i); // 0 1 2
}
console.log(i);
```

```JavaScript title:skip_step.js
let i = 0;

for (; i < 3;) { 
	console.log(i++); // 0 1 2
}
```
- This makes the loop identical to `while (i < 3)`.

```JavaScript title:infinite_for.js
for (;;) {
	// repeats without limits.
}
```