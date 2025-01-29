### Meta
2024-09-20 17:28
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_methods_of_primitives]]
**State:** #completed  

### The primitive conundrum
- The paradox faced by the creator of JavaScript:
	- There are many things one would want to do with primitives, like a string or number. It would be great to access them using methods.
	- Primitives must be as fast and lightweight as possible.
- The solution:
	1) Primitives are still primitive. A single value is desired.
	2) The language allows access to methods and properties of strings, numbers, Booleans and symbols.
	3) In order for that to work, a special "object wrapper" that provides the extra functionality is created, and then is destroyed.

### Implementation
- The "object wrappers" are different for each primitive type: `String`, `Number`, `Boolean`, `Symbol`, `BigInt`. Thus, they provide different sets of methods.
- For instance, there exists a string method [str.toUpperCase()]([[String.prototype.toUpperCase()]]) that returns a capitalized a capitalized `string`.

```JavaScript title:app.js
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
```

- Behind the scenes:
	- The string `str` is a primitive. In the moment of accessing its property, a special object is created that knows the value of the strings, and has useful methods, like `toUpperCase()`.
	- That method runs and returns a new string (shown by `alert`).
	- The special object is destroyed, leaving the primitive `str` alone.
- Thus, primitives can provide methods, but they still remain lightweight.
- A number has methods of its own, such as [toFixed(n)]([[Number.prototype.toFixed()]]) rounds the number to the given precision:

```JavaScript title:app.js
let n = 1.23456;

alert( n.toFixed(2) ); // 1.23
```

#### Constructors `String`/`Number`/`Boolean` are for internal use only
- Some languages like Java 🤮 allow us to explicitly create "wrapper objects" for primitives using a syntax like `new Number(1)` or `new Boolean(false)`.
- In JavaScript, that's also possible for historical reasons, but highly **NOT RECOMMENDED**.

```JavaScript title:app.js
alert( typeof 0 ); // "number"

alert( typeof new Number(0) ); // "object"
```

- Objects are always `truthy` in `if`,  so here the alert will trigger:

```JavaScript title:app.js
let zero = new Number(0);

if (zero) {
	alert( "zero is truthy!?!" );
}
```

- On the other hand, using the same functions `String`/`Number`/`Boolean` without `new` is totally fine and useful.
- They convert a value to the corresponding type: to a string, a number, or a Boolean (primitive).

```JavaScript title:app.js
let num = Number("123");
```


#### null/undefined have no methods
- `null` and `undefined` have no corresponding "wrapper objects" and provide no methods.
- An attempt to access a property of such a value would give an error.