### Meta
2024-09-19 21:30
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_object_methods_this]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
}

user.sayHi = function() {
	alert('Hello!');
}

user.sayHi(); // Hello!
```

### What it does
- Performs an action from within the object.

### How it does it
- Above, we used a function expression to create a function and assign it to the property `user.sayHi` of the object.
- Then, we call it as `user.sayHi()`.
- A function that isa property of an object is called a **method**.
- We can use a pre-declared function as a method.

```JavaScript title:app.js
let user = {
	// ...
}

// function declaration
function greet() {
	alert("Hello!");
}

// assign as method
user.sayHi = greet;

user.sayHi(); // Hello!
```
