### Meta
2024-09-19 22:45
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_constructor_operator_new]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function User(name) {
	this.name = name;

	this.sayHi = function() {
		alert("My name is: " + this.name);
	};
}

let john = new User("John");

john.sayHi(); // My name is: John
```

### What it does
- Defines methods that all new instances of the constructor can use.

### How it does it
- Bad practice.
