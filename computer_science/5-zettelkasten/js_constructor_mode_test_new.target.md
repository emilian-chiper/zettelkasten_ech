### Meta
2024-09-19 22:30
**Tags:** [[javascript]] [[javascript_object_basics]] [[js_constructor_mode_test_new.target]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function User() {
	alert(new.target);
}

// without 'new'
User(); // undefined

// with 'new'
new User(); // function User { ... }
```

### What it does
- Inside a function, we can check if it was called with `new` or without it, using a special property called `target.new`.
- It is `undefined` for regular calls and equals the function if called with `new`.
- This can help to figure out if it was called in 'constructor mode' (with `new`) or in 'regular mode'.
- We can also make both `new` and regular calls to do the same, like so:

```JavaScript title:app.js
function User(name) {
	if (!new.target) {
		return new User(name);
	}

	this.name = name;
}

let john = User('John'); // redirects call to new User
alert(john.name); // John
```

- This approach is sometimes used in libraries to make the syntax more flexible, so that people may call the function with or without `new`, and it still works.
- Omitting `new` makes it a bit less obvious what's going on, so it's best to avoid this in most cases.
- With `new` we know that the new object is being created.

### How it does it
Examples
