### Meta
2024-09-19 16:57
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	"likes birds": true,
}

console.log(user["likes birds"]); // true
```

### What it does
- Allows us to access multiword properties.

### How it does it
- For multiword properties, the dot accessor doesn't work:

```JavaScript title:app.js
user.likes birds = true; // produces an error
```

- JavaScript thinks that we address `user.likes`, and then gives a syntax errors when it comes across unexpected `birds`.
- The dot requires the key to be a valid identifier, which implies that:
	- it contains no spaces,
	- doesn't start with a digit, and
	- doesn't include special characters(`$` and `_` are allowed).
- The square bracket notation works with any string.

```JavaScript title:app.js
let user = {};

// set
user["likes birds"] = true;

// get
console.log(user["likes birds"]); // true

// delete
delete user["likes birds"];
```

- Note that the string inside the brackets is properly quoted (any type of quotes will do).
- Square brackets also provide a way to obtain the property name as the result of any expression.

```JavaScript title:app.js
let key = "likes birds";

// same as user["likes birds"] = true;
user[key] = true;
```

- Here, the `key` variable may be calculated at run-time or depend on the user input. Then, we use it to access the property, which allows for great flexibility.

```JavaScript title:app.js
let user = {
	name: "John",
	age: 30,
};

let key = prompt("What do you want to know about the user?", "name");

// access by variable
console.log( user[key] ); // Jon (if the user entered "name")
```

- The dot notation cannot be used similarly. Accessing the property returns `undefined`.

#### Computed properties
- We can use square brackets in an object literal when creating an object.
- That's called *computed properties*.

```JavaScript title:app.js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
	[fruit]: 5,
};

alert( bag.apple ); // 5 if fruit="apple"
```

- The meaning of a computed property is simple: `[fruit]` means that the property name should be taken from `fruit`.
- So, if a user enters "apple", `bag` will become `{ apple: 5, }`.
- We can use more complex expressions inside square brackets:

```JavaScript title:app.js
let fruit = "apple";
let bag = {
	[fruit + 'Computers']: 5, // bag.appleComputers = 5
}
```

#### Usage
- When property names are knows and simple, the dot is used.
- If we need something more complex, we switch to square bracket notation.