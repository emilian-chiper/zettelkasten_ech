### Meta
2024-09-19 17:14
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function makeUser(name, age) {
	return {
		name,
		age,
		// ... other properties
	};
}

let user = makeUser("John", 30);
console.log(user.name); // John
```

### What it does
- Uses existing variables and values for property names.

### How it does it
- in the example above, properties have the same names as variables.
- The use-case of making a property from a variable is common, that there's a special *property value shorthand* to make it shorter.
- This is the long-form version.

```JavaScript title:app.js
function makeUser(name, age) {
	return {
		name: name,
		age: age,
		// ... other properties
	};
}

let user = makeUser("John", 30);
console.log(user.name); // John
```

- We can use both normal properties and shorthand properties in the same object.

```JavaScript title:app.js
let user = {
	name, // same as name:name
	age: 30,
}
```