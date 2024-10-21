### Meta
2024-10-20 21:42
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### Most methods support “thisArg”
Almost all array methods that call functions – like `find`, `filter`, `map`, with a notable exception for `sort`, accept an optional additional parameter `thisArg`.

That parameter is rarely used. Here’s the full syntax of these methods:

```JavaScript title:app.js
arr.find(func, thisArg);
arr.filter(func, thisArg);
arr.map(func, thisArg);
// ...
// thisArg is the optional last argument
```

The value of `thisArg` parameter becomes `this` for `func`.

For example, here we use a method of `army` object as a filter, and `thisArg` passes the context:

```JavaScript title:app.js
let army = {
	minAge: 18,
	maxAge: 27,
	canJoin(user) {
		return user.age >= this.minAge && user.age < this.maxAge;
	}
};

let users = [
	{age: 16},
	{age: 20},
	{age: 23},
	{age: 30}
];

// find users, for whom army.canJoin returns true
let soldiers = users.filter(army.canJoin, army);

alert(soldiers.length); // 2
alert(soldiers[0].age); // 20
alert(soldiers[1].age); // 23
```

If in the examples above we used `users.filter(army.canJoin)`, then `army.canJoin` would be called as a standalone function, with `this=undefined`, thus leading to an instant error.

A call to `users.filter(army.canJoin, army)` can be replaced with `users.filter(user => army.canJoin(user))`, that does the same. The latter is used more often, as it’s a bit easier to understand for most people.