### Meta
2024-09-19 17:32
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {};

alert( user.noSuchProperty === undefined ); // true

```

### What it does
- Compared to many other languages, a notable feature or objects in JavaScript is that it's possible to access any property.
- There will be no error if the property doesn't exists.

### How it does it
- To test whether the property exists, there a special operator called `"in"`.

```JavaScript title:app.js
"key" in object
```

- For instance:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
};

alert( "age" in user ); // true
alert( "blabla" in user ); // false
```

- On the left side of `in` there must be a *property key*. That is usually a *quoted string*.
- If we omit the quotes, that means a variable should contain the actual name to be tested:

```JavaScript title:app.js
let user = {
	age: 30,
}

let key = "age";
alert( key in user); // true

```

#### Why does the `in` operator exists?
- Isn't it enough to compare against `undefined`?
- Most of the time, the comparison with `undefined` works fine, but there's an edge case when it fails.
- It's when an object property exists, but stores undefined.

```JavaScript title:app.js
let obj = {
	test: undefined,
}

alert( obj.test ); // undefined

alert("test" in obj); // true
```

- In the code above, the property `obj.test` technically exists, so the `in` operator works right.
- This happens rarely, as `undefined` should not be explicitly assigned.
- We mostly use `null` for 'unknown' or 'empty' values.
