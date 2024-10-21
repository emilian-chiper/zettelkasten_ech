### Meta
2024-10-20 22:33
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_iterables]]
**State:** #completed 

This code creates a string iterator and gets values from it “manually”:

```JavaScript title:app.js
let str = "Hello";

// does the same as
// for (let char of str) alert(char);

let iterator = str[Symbol.iterator]();

while (true) {
	let result = iterator.next();
	if (result.done) break;
	alert(result.value); // outputs characters one by one
}
```

That is rarely needed, but gives us more control over the process than `for..of`. For instance, we can split the iteration process: iterate a bit, then stop, do something else, and then resume later.