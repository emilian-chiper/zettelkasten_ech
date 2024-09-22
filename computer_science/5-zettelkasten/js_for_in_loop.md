### Meta
2024-09-19 17:54
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
for (key in object) {
	// ...
}
```

### What it does
- Iterates over all keys of an object.

### How it does it
- Let's output all properties of `user`:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	isAdmin: true,
}

for (let key in user) {
	// keys
	alert( key ); // name, age, isAdmin
	// values for the keys
	alert( user[key] ); // Jon, 30, true
}
```

- All `for` constructs allow us to declare the looping variable inside the loop, like `let key` here.
- We can use other names instead of `key`, like `for (let prop in obj)`.

#### Ordered like an object
- If we loop over an object, do we get all properties in the same order they were added?
- They are ordered in a special fashion:
	- **integer** properties are **sorted**,
	- others appear in **creation order**.

```JavaScript title:app.js
let codes = {
	"49": "Germany",
	"41": "Switzerland",
	"44": "Great Britain",
	// ...
	"1": "USA",
};

for (let code in codes) {
	alert(code); // 1, 41, 44, 49
}

```

##### Integer properties
- An **integer property** is a string that can be converted to-and-from an integer without a change.
- So, `"49"` is an integer property key, because when it's transformed to an integer number and back, it's still the same. `"+49"` and `"1.2"` are not:

```JavaScript title:app.js
// Number(...) explicitly converts to a number
// Math.trun is a built-in function that removes the decimal part

alert( String(Math.trunc(Number("49"))) ); // "49", same, integer property
alert( String(Math.trunc(Number("+49"))) ); // "49", not same, "+49" => not integer property
alert( String(Math.trunc(Number("1.2"))) ); // "1", not same "1.2" => not integer property

```

- On the other hand, if the keys are non-integer, then they are listed in the creation order. For instance:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	surname: 'Smith',
};
user.age = 25;

// non-integer properties are listed in the creation order
for (let prop in user) {
	alert( prop ); // name, surname, age
}

```

- To fix the issue with the phone codes, me make them non-integer.

```JavaScript title:app.js
let codes = {
	"+49": "Germany",
	"+41": "Switzerland",
	"+44": "Great Britain",
	// ...
	"+1": "USA",
};

for (let code in codes) {
	alert( +code ); // 49, 41, 44, 1
}
```