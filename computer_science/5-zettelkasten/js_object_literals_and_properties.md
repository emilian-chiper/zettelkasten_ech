### Meta
2024-09-19 11:45
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
};

```

### What it does
- Stores properties in the form of `key: value` pairs.

### How it does it
- A property has a `key` ("name" or "identifier") before the colon `:` and a `value` to the right of it.
- In the `user` object above, there are two properties:
	- The first property has a key of `name` and a value of `'Jon'`.
	- The second one has a key of `age` and a value of `30`.

### Accessing properties - the  dot notation
- Property values are accessible using the dot notation.

```JavaScript title:app.js
console.log( user.name ); // Jon
console.log( user.age ); // 30
```

### Adding properties
- A property value can be of any type. Let's a Boolean:

```JavaScript title:app.js
user.isAdmin = true;
```

### Removing properties
- To remove a property, we can use the `delete` operator.

```JavaScript title:app.js
delete user.age;
```

### Multiword property names
- Multiword property names can be used, but they must be quoted:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	"like birds": true
};
```

### Last property
- The last property in the list may end with a comma.
- This is called a 'trailing' or 'hanging' comma.
- It makes it easier to add/remove/move around properties, because all line become alike.

```JavaScript title:app.js
let user = {
	name: 'Bilbo',
	age: 30,
}
```