### Meta
2024-09-19 22:38
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_constructor_operator_new]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function BigUser() {
	this.name = "John";
	return { name: "Godzilla" }; // <-- return this object
}

alert( new BigUser().name ); // Godzilla
```

### What it does
- `return` with an object returns an object, in all other cases `this` is returned.

### How it does it
- Usually, constructors do not have a `return` statement.
- Their task is to write all necessary stuff into `this`, and it automatically becomes the result.
- If there is a `return` statement, the rules are simple:
	- If `return` is called with an object, then the object is returned instead of `this`.
	- If `return` is called with a primitive, it's ignored.
- Here's an example with an empty return:

```JavaScript title:app.js
function SmallUser() {
	this.name = "John";

	return; // <--returns this
}

alert( new SmallUser().name ); // John
```

#### Omitting parentheses
- We can omit parentheses after `new`:

```JavaScript title:app.js
let user = new User;
// same as
let user = new User();
```

- This is NOT a good practice.