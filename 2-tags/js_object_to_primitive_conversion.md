### Meta
2024-09-20 12:04
**Tags:** [[javascript]] [[javascript_object_basics]]
**State:** #completed  

### Conversion rules
1) There's no conversion to Boolean
	- All objects are `true` in a Boolean context.
	- There exist only numeric and string conversions.
2) The numeric conversion happens when we **subtract** objects or apply **mathematical functions**.
	- `Date` objects can be subtracted, and the result of `date1 - date2` is the time difference between the two dates.
3) String conversion usually happens when we **output** an object with `alert(obj)` and in similar contexts.

### Hints
- How does JavaScript decide which conversion to apply?
- There are three variants of type conversion, that happen in various situations.
- They are called **"hints"**.

#### "string"
- For an object-to-string conversion, when we're doing an operation on an object that expects a string, such as `alert`.

```JavaScript title:app.js
// output
alert(obj);

// using object as a property key
anotherObj[obj] = 123;
```

#### "number"
- For an object-to-number conversion.

```JavaScript title:app.js
// explicit conversion
let num = Number(obj);

// maths (except binary plus)
let n = +obj; // unary plus
let delta = date1 - date2;

// less/greater comparison
let greater = user1 > user2;
```

#### "default"
- Occurs in rare cases when the operator is unsure what type to expect.
- For instance, binary `+` can work with both strings (concatenation) and numbers (addition).
- If a  binary plus gets an object as an argument, it uses the `"default"` hint to convert it.
- If an object is compared using `==` with a string, number, or symbol, it's also unclear which conversion should be done, so `"default"` is used.

```JavaScript title:app.js
// binary plus uses the "default" hint
let total = obj1 + obj2;

// obj == number uses teh "default" hint
if (user == 1) { ... };
```

- The `>` and `<` comparison operators can work with both strings and numbers. Still, they use the `"number"` hint, not `"default"`.

- In practice, things are a bit simple.
- All built-in objects except for `Date` implement `"default"` conversion the same way as `"number"`.

**To do the conversion, JavaScript tries to find and call three object methods:**
1) Call `obj[Symbol.toPrimitive](hint)` - the method with the symbolic key `Symbol.toPrimitive` (system symbol), if such method exists,
2) Otherwise, if hint is `"string"`
	- try calling `obj.toString()` or `obj.valueOf()`, whatever exists.
3) Otherwise, if hit is `"number"` or `"default"`
	1) try calling `obj.valueOf()` or `obj.toString`, whatever exists.

### Symbol.toPrimitive
- Used to name the conversion method.

```JavaScript title:app.js
obj[Symbol.toPrimitive] = function(hint) {
	// here goes the code to convert this object to a primitive
	// it must return a primitive value
	// hint = one of "string", "number", "default"
}
```

- If the method exists, it's used for all hints, and no more methods are needed.
- Here, the `user` object implements it.

```JavaScript title:app.js
let user = {
	name = 'Jon',
	money = 1000,

	[Symbol.toPrimitive](hint) {
		alert(`hint: ${hint}`);
		return hint === "string" ? `{name: "${this.name}"}` : this.money;
	}
};

// conversion demo
alert(user); // hint: string -> {name: 'Jon'}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

- Thus, `user` becomes a self-descriptive string or a money amount, depending on the conversion.
- The single method `user[Symbol.toPrimitive]` handles all conversion cases.

### toString/valueOf
- If there's no `Symbol.toPrimitive` then JavaScript tries to find methods `toString` and `valueOf`:
	- For the `"string"` hint:
		- call `to String`, and
			- if it doesn't exist or if it returns an object instead of a primitive value, then
		- call `valueOf`.
	- For other hints:
		- call `valueOf`, and
			- if it doesn't exist or if it returns an object instead of a primitive value, then
		- call `toString`.
- `toString` and `valueOf` are not symbols, but rather "regular" string-named methods.
- They provide an alternative "old-style" way to implement to conversion.
- These methods must return a primitive value. If they return an object, they are ignored.
- By default, a plain object has the following methods:
	- `toString`, which returns a string `[object Object]`,
	- `valueOf`, which returns the object itself.

```JavaScript title:app.js
let user = {name: 'Jon'};

alert(user); // [object Object]
alert(user.valueOf() === user); // true
```

- The methods can be used to customize the conversion.
- For instance, here `user` does the same as above using a combination of `toString` and `valueOf` instead of `Symbol.toPrimtive`:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	money: 1000,

	// for hint="string"
	toString() {
		return `{name: "${this.name}"}`;
	}

	// for hint="number" or "default"
	valueOf() {
		return this.money;
	}
};

alert(user); // toString -> {name: 'Jon'}
alert(+user); // valueOf -> 1000
alert(user + 500); // valueOf -> 1500
```

- The behavior is the same as the previous implementation, using `Symbol.toPrimitive`.

- Often, we want a single "catch-all" place to handle all primitive conversions. In this case, we can implement `toString` only.

```JavaScript title:app.js
let user = {
	name: 'Jon',

	toString() {
		return this.name;
	}
};

alert(user); // Jon
alert(user + 500); // Jon500
```

- In the absence of `Symbol.toPrimitive` and `valueOf`, `toString` will handle all primitive conversions.

#### A conversion can return any primitive value
- Primitive-conversion methods don't necessarily return the "hinted" primitive.
- There's no control whether `toString` returns exactly a string, or whether `Symbol.toPrimitive` returns a number for the hint `"number"`.
- **Mandatory:** these methods must return a *primitive*, NOT an object.

### Further conversions
- If we pass an object as an argument, there are two stages of calculations:
	1) The object is converted to a primitive (by the rules above).
	2) If necessary for further calculations, the resulting primitive is also converted.

```JavaScript title:app.js
let obj = {
	toString() {
		return "2";
	}
};

alert(obj * 2); // 4
```

- The multiplication `obj * 2` first converts the object to primitive (string `"2"`).
- Then, `"2" * 2` becomes `2 * 2`.

- Binary `+` will concatenate string in the same situation, as it gladly accepts a string:

```JavaScript title:app.js
let obj = {
	toString() {
		return "2";
	}
};

alert(obj + 2); // "22"
```