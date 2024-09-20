### Meta
2024-09-20 11:34
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_symbol_type]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
}

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // access the data using the symbol as key
```

### What it does
- Allows us to create "hidden" properties of an object, that no other part of code can accidentally access or overwrite.

### How it does it
- What's the benefit of using `Symbol("id")` over a string `"id"`?
- As `user` objects belong to another codebase, it's unsafe to add fields to them, since we might affect pre-defined behavior in that other codebase.
- Symbols cannot be accessed accidentally.
- The third-party code won't be aware of newly defined symbols, so it's safe to add symbols to the `user` objects.
- Imagine that another script wants to have its own identifier inside `user`, for its own purposes.
- Then that script can create its own `Symbol("id")`, like so:

```JavaScript title:app.js
// ...
let id = Symbol("id");

user[id] = "Their id value";
```

- There will be no conflict between our and their identifiers, because symbols are always different, even if they have the same name.
- If we used a string `"id"` instead of a symbol for the same purpose, then there *would* be a conflict.

```JavaScript title:app.js
let user = { name: "John" };

// Our script uses "id" property
user.id = "Our id value";

// ... Another script also wants "id" for its purposes
user.id = "Their id value"

// Thus, the script is overwritten!
```

#### Symbols in an object literal
- If we want to use a symbol inside an object literal `{...}`, we need square brackets around it.

```JavaScript title:app.js
let id = Symbol("id");

let user = {
	name: 'Jon',
	[id]: 123,
}
```

#### Symbols are skipped by for...in

```JavaScript title:app.js
let id = Symbol("id");
let user = {
	name: 'Jon',
	age: 30,
	[id]: 123
};

for (let key in user) alert(key); // Jon, 30

// The direct acces by the symbol works
alert("Direct: " + user[id] ); // Direct: 123
```

- [Object.keys(user)]([[js_Object.keys()]]) also ignores them, which is part of the general "hiding symbolic properties" principle.
- If another script or library loops over our object, it won't unexpectedly access a symbolic property.
- In contrast, [Object.assign()]([[js_Object.assign()]]) copies both string and symbol properties.

```JavaScript title:app.js
let id = Symbol("id");
let user = {
	[id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123
```