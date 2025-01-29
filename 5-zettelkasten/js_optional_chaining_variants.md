### Meta
2024-09-20 09:05
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_optional_chaining]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let userAdmin = {
	admin() {
		alert("I am admin");
	}
};

let userGuest = {};

userAdmin.admin?.(); // I am admin

userGuest.admin?.(); // no such method

```

### What it does
- `?.` is not an operator, but a special syntax construct, that also works with functions and square brackets.

### How it does it
- In the example above, if the `admin` function exists, then it runs. Otherwise, `?.` stops the evaluation without errors.
- The `?.[]` syntax also works.

```JavaScript title:app.js
let key = 'firstName';

let user1 = {
	firstName: 'Jon',
};

let user2 = null;

alert( user1?.[key] ); // Jon
alert( user2?.[key] ); // undefined
```

- Also, we can use `?.` with delete:

```JavaScript title:app.js
delete user?.name; // delete user.name if user exists
```


#### We can use `?.` for safe reading and deleting, but not writing
- The optional chaining `?.` construct has no use on the left side of an assignment.

```JavaScript title:app.js
let user = null;

user?.name = 'Jon'; // error
```