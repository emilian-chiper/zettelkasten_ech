### Meta
2024-10-22 21:07
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_destructuring_assignment]]
**State:** #completed 

### Smart function parameters
There are times when a function has many parameters, most of which are optional. That’s especially true for user interfaces. Imagine a function that creates a menu. It may have a width, a height, a title, an item list, etc.

Here’s a bad way to write it:

```JavaScript title:app.js
function showMenu(title = "Untitled", width = 200, height = 100, items = []) {
	// ...
}
```

The problem is remembering the order of arguments. Another issue is how to call a function when most parameters are ok by default.

Like this?

```JavaScript title:app.js
// undefined where default values are fine
showMenu("My Menu", undefined, undefined, ["Item1", "Item2"])
```

That’s ugly, and becomes unreadable when we deal with more parameters.

Instead, we can pass parameters as an object, and the function immediately destructures them into variables:

```JavaScript title:app.js
// we pass object to function
let options = {
	title: "My menu",
	items: ["Item1", "Item2"]
};

// ... and it immediately expands it to variables
function showMenu({title = "Untitled", width = 200, height = 100, items = []}) {
	// title, items -- taken from options
	// width, height -- defaults used
	alert(`${title} ${width} ${height}`); // My menu 200 100
	alert( items ); // Item1, Item2
};

showMenu(options);
```

We can also use more complex destructuring with nested objects and colon mappings:

```JavaScript title:app.js
let options = {
	title: "My menu",
	items: ["Item1", "Item2"],
};

function showMenu({
	title = "Untitled",
	width: w = 100,
	height: h = 200,
	items: [item1, item2],
}) {
	alert( `${title} ${w} ${h}` );
	alert( item1 );
	alert( item2 );
};

showMenu(options);
```

The full syntax is the same as for a destructuring assignment:

```JavaScript title:app.js
function({
	incomingProperty: varName = defaultValue
	...
})
```

Then, for an object of parameters, there will be a variable `varName` for the property `incomingProperty`, with `defaultValue` by default.

Please not that such destructuring assumes that `showMenu()` does have an argument. If we want all values by default, then we should specify an empty object:

```JavaScript title:app.js
showMenu({}); // ok, all values are default

showMenu(); // this would produce an error
```

We can fix this by making `{}` the default value for the whole object of parameters:

```JavaScript title:app.js
function showMenu({ title = "Menu", width = 100, height = 200 } = {}) {
	alert( `${title} ${width} ${height} ` );
};

showMenu(); // Menu 100 200
```

In the code above, the whole arguments object is `{}` by default, so there’s always something to destructure.