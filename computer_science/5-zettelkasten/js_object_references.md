### Meta
2024-09-19 18:16
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_object_references_and_copying]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = { name: "John" };

let admin = user; // copy the reference

```

### What it does
- Copies the reference to another object.

### How it does it
- Compared to primitives, objects are stored and copied **by reference**, whereas primitives are always copied 'as a whole value'.
- Here, we put a copy of `message` into `phrase`:

```JavaScript title:app.js
let message = "Hello!";
let phrase = message;
```

- **A variable assigned to an object stores not the object itself, but it's "address in memory" -- in other words "a reference" to it.**

```JavaScript title:app.js
let user = {
	name: 'Jon',
};
```

- The object is stored somewhere in memory, while the `user` variable has (is) a 'reference' to it.
- When we perform actions with the object, e.g. take a property `user.name`, the JavaScript engine look at what's at that address and performs the operation on the actual object.
- **When an object variable is copied, the reference is copied, but the object itself is not duplicated.**

```JavaScript title:app.js
let user = {
	name: 'Jon',
};

let admin = user; // copy the reference

admin.name = 'Pete';

console.log(user.name); // 'Pete'
```