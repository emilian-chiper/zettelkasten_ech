### Meta
2024-09-19 22:20
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_constructor_operator_new]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
function User(name) {
	this.name = name;
	this.isAdmin = false;
}

let user = newUser('Jack');

alert(user.name); // Jack
alert(user.isAdmin); // false
```

### What it does
- Implement reusable object creation code.

### How it does it
- Conventions:
	1) Capitalized names.
	2) Executed only with the `new` operator.
- When a function is executed with `new`, it performs the following:
	- A new empty object is created and assigned to `this`.
	- The function body executes. Usually, it modifies `this`, adds new properties to it.
	- The value of `this` is returned.
- Something like this:

```JavaScript title:app.js
function User(name) {
	// this = {}; (implicitly)

	// add properties to this
	this.name = name;
	this.isAdmin = false;

	// return this; (implicitly)
}
```

- So, `let user = new User("Jack")` gives the same result as:

```JavaScript title:app.js
let user = {
	name: "Jack",
	isAdmin: false,
}
```

- Now if we want to create other users, we can call `new User("Ann")`,  `new User("Alice")` and so on.
- Again, any function (except arrow functions) can be used as a constructor.
- It can be run with `new` as long as it follows the 'capital letter first' convention.

#### new function() {...}
- If we have many lines of code all about creation of a single complex object, we can wrap them in an **immediately called constructor function**, like this:

```JavaScript title:app.js
// create function and immediately call it
let user = new function() {
	this.name = 'John';
	this.isAdmin = fase;

	// ... other code for user creation
	// maybe complex logic and statements
	// local variables etc.
}
```

- This constructor can't be called again, because it is not save anywhere, but created and immediately called.
- This trick aims to encapsulate the code that constructs the single object, without future reuse.