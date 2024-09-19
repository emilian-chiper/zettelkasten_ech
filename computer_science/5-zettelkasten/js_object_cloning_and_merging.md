### Meta
2024-09-19 18:47
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_object_references_and_copying]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
};

let clone = {} // the new empty object

// the copying process
for (let key in user) {
	clone[key] = user[key];
}

// now clone isa fully independent object with the same content
clone.name = 'Pete';

alert( user.name ); // Jon
alert( clone.name ); // Pete
```

### What it does
- Clones the content of an object into an empty object.

### How it does it
- Uses a `for ... in` loop to clone the content of the `user` object into the `clone` object.

### Object.assign()

```JavaScript title:app.js
Object.assign(dest, ...sources)
```

- Arguments:
	- `dest` is a target object (i.e. destination).
	- Further arguments list source objects.

```JavaScript title:app.js
let user = { name: 'Jon' };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copies all properties from the permissions objects into user
Object.assign(user, permissions1, permissions2);

alert(user.name); // Jon
alert(user.canView); // true
alert(user.canEdit); // true
```

- If the copied property name already exists, it gets overwritten:

```JavaScript title:app.js
let user = { name: 'Jon' };

Object.assign(user, { name: 'Pete' });

alert(user.name); // Pete
```

- We can also use `Object.assign` to perform a simple object cloning:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
};

let clone = Object.assign({}, user);

alert(clone.name); // Jon
alert(clone.age); // 30
```

- Here it copies all properties of `user` into the empty object and returns it.