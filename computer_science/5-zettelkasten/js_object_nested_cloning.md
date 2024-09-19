### Meta
2024-09-19 20:58
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	sizes: {
		height: 182,
		width: 50,
	}
};

console.log( user.sizes.height ); // 182

let clone = Object.assign({}, user);

console.log( user.sizes === clone.sizes); // true

// user and clone share sizes
user.sizes.width = 60;
console.log(clone.sizes.width); // 60
```

### What it does
- Clones properties in nested objects.

### How it does it
-  It's not enough to copy `clone.sizes = user.sizes`, because `user.sizes` is an object, and will be copied by reference, so `clone` and `user` will share the same sizes.
- To fix that and make `user` and `clone` truly separate objects, we should use a cloning loop that examines each value of `user[key]` and, if it's an object, then replicate its structure as well.
- That is called *deep cloning* or *structured cloning*.

### structuredClone
- The call `structuredClone(object)` clones the object with all the nested properties.

```JavaScript title:app.js
let user = {
	name: 'Jon',
	sizes: {
		height: 182,
		width: 50,
	}
};

let clone = structuredClone(user);

console.log( user.sizes === clone.sizes ); // false, different objects

// user and clone are totally unrelated now
user.sizes.width = 60; // change a property from one place
console.log(clone.sizes.width); // 50, not related
```

- The `structuredClone` method can clone most data types, such as objects, arrays, primitive values.
- It also supports circular references, when an object property references the object itself (directly or via a chain or references).

```JavaScript title:app.js
let user = {};

// circular reference
user.me = user;

let clone = structutredClone(user);
alert(clone.me === clone); // true
```

- `clone.me` references the `clone`, not the `user`!
- Thus, the circular reference was cloned correctly as well.

- There are cases when `structuredClone` fails, such as when an object has a function property:

```JavaScript title:app.js
structuredClone({
	f: function() {}
});
```

- Function properties aren't supported.
- To handle such complex cases we may need to use a combination of cloning methods, write custom code, or use existing implementations such as `_.cloneDeep(obj)` from the `lodash` JavaScript library.