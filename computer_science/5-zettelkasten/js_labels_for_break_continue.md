### Meta
2024-09-18 10:19
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_loops]]
**State:** #completed  

### Problem
- Sometimes we need to break out from multiple nested loops at once.
- In the code below, we loop over `i` and `j`, prompting for the coordinates `(i, j)` from `(0, 0)` to `(2, 2)`.
- We need a way to stop the process if the user cancels the input.
- The ordinary `break` after `input` would only break the inner loop.


```JavaScript title:app.js
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // what if we want to exit from here to Done (below)?
  }
}

console.log('Done!');
```

### Solution
- A ***label*** is an identifier with a colon before a loop:

```JavaScript title:app.js
labelName: for (...) {
	...
}
```

- The `break <labelName>` statement breaks out of the label.

```JavaScript title:app.js
outer: for (let i = 0; i < 3; i++) {

	for (let j = 0; j < 3; j++) {

		let input = prompt(`Value at coords (${i}, ${j})`, '');

		// if an empty string or canceled, the break out of both loops
		if (!input) break outer;

		// do something else with the value ...
	}
}

alert('Done!');
```

- In the code above, `break outer` looks upwards for the label named `outer` and breaks out of the loop.
- The control goes straight from line `8` to line `14`.
- The label can also be moved to a separate line.

#### Warning
- Labels **DO NOT** allow us to jump into an arbitrary place in the code.
- This is impossible:

```JavaScript title:app.js
break label;

label: for (...)
```

- A `break` directive must be inside a code block.
- Any labelled code block will do:

```JavaScript title:app.js
label: {
	// ...
	break label; // works
	// ...
}
```

- Most of the time `break` is used inside loops.
- A `continue` is only possible from inside a loop.