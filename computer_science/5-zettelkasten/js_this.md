### Meta
2024-09-19 21:40
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_object_methods_this]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	sayHi() {
		console.log(`Hello, ${this.name}!`);
	},
};

user.sayHi(); // Hello, Jon!
```

### What it does
- To access the object, a method can use the **this** keyword.
- The value of `this` is the object "before dot", the one used to call the method.

### How it does it
- While technically possible to use the object's name (i.e. `user`) over `this`, such code is unreliable.
- If we decide to copy `user` to another variable, e.g. `admin = user`, and overwrite `user` with something else, then it will access the wrong object.

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	sayHi() {
		alert( user.name );
	},
};

let admin = user;
user = null; // overwrite to make things obvious

admin.sayHi(); // TypeError: Cannot read property 'name' of null
```

- If we had used `this.name` over `user.name` inside the `alert`, then the code would work.

### `this` is not bound
- In JavaScript, `this` behaves unlike most other programming languages.
- It can be used in any function, even if it's not a method of an object.

```JavaScript title:app.js
function sayHi() {
	alert( this.name );
}
```

- The value of `this` is evaluated during the run-time, depending on the *context*.
- For instance, here the same function is assigned to two different objects and has different 'this' in the calls:

```JavaScript title:app.js
let user = { name: 'Jon' };
let admin = { name: 'Amdin' };

function sayHi() {
	alert( this.name );
}

// Use the same function in two objects
user.f = sayHi;
admin.f = sayHi;

user.f(); // Jon (this == user)
admin.f(); // Admin (this == admin)

admin['f'](); // Admin
```

- The rule is simple: if `obj.f()` is called, then `this` is `obj` during the call of `f`. So either `user` or `admin` in the example above.

### Calling without an object
- We can call the function without an object at all:

```JavaScript title:app.js
function sayHi() {
	alert(this);
}

sayHi(); // undefined
```

- In this case, `this` is `undefined` in strict mode.
- In non-strict mode, the value of `this` in such case will be the *global object* (`window` in a browser). This is a historical behavior that `'use strict'` fixes.
- Usually such a call is a programming error. If there's `this` inside a function, it expects to be called in an object context.

### Arrow functions have no `this`
- If we reference `this` from an arrow functions, it's taken from the outer context.
- For instance, here `arrow()` uses `this` from the outer `user.sayHi()` method:

```JavaScript title:app.js
let user = {
	firstName: 'Ilya',
	sayHi() {
		let arrow = () => alert(this.firstName);
		arrow();
	},
};

user.sayHi(); // Ilya
```

- That's a special feature of arrow functions.
- It's useful when we actually do not want to have a separate `this`, but would rather take it form the outer context.