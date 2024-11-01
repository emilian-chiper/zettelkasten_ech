### Meta
2024-10-22 12:06
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_destructuring_assignment]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let arr = ["John", "Smith"];

let [firstName, surname] = arr;

alert(firstName); // John
alert(surname); // Smith
```

### What it does
The **destructuring assignment** is a special syntax that allows us to “unpack” arrays or objects into variables.

### Array destructuring
It looks great when combined with `split` or other array-returning methods:

```JavaScript title:app.js
let [firstName, surname] = "John Smith".split(' ');

alert(firstName); // John
alert(surname); // Smith
```

#### Particularities
**⚠️ “Destructuring” does not mean “destructive”**
It’s called “destructuring assignment” because it “destructures” by copying items into variables. The array itself isn’t mutated. It’s a shorter way to write:

```JavaScript title:app.js
// let [firstName, surname] = arr;
let firstName = arr[0];
let surname = arr[1];
```


**⚠️ Ignore elements using commas**
Unwanted elements of the array can be ignored with commas:

```JavaScript title:app.js
// second element ins't needed
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert( title ); // Consul
```

In the code above, the second element of the array is skipped by using a comma, the third is assigned to `title`, and the rest is ignored (as there are no variables for them).

**⚠️ Works with any iterable on the right side**

```JavaScript title:app.js
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```

That works, because internally a destructuring assignment works by iterating over the right value. It’s a kind of syntax sugar calling `for..of` over the value to the right hand side of `=` and assigning the values.

**⚠️ Assign to anything at the left-side**
We can use any “assignables” on the left side.

For instance, an object property:

```JavaScript title:app.js
let user = {};
[user.name, user.surname] = "John Smith".split(' ');

alert(user.name); // John
alert(user.surname); // Smith
```

**⚠️ Looping with .entries()**
In the previous chapter, we saw the `Object.entries(obj)` method.

We can use it with destructuring to loop over the keys-and-values of an object:

```JavaScript title:app.js
let user = {
	name: "John",
	age: 30
};

// loop over the keys-and-values
for (let [key, value] of Object.entries(user)) {
	alert(`${key}:${value}`); // name: John, then age: 30
}
```

The similar code for a `Map` is simple, as it’s iterable:

```JavaScript title:app.js
let user = new Map();
user.set("name", "John");
user.set("age", "30");

// Map iterates as [key, value] pairs, very convenient for destructuring
for (let [key, value] of user) {
	alert(`${key}:${value}`); // name: John, age: 30
}
```

**⚠️ Swap variables trick**
There’s a well-know trick for swapping values of two variables using a destructuring assignment:

```JavaScript title:app.js
let guest = "Jane";
let admin = "Pete";

[gues, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane
```

Here we create a temporary array of two variables and immediately destructure it in swapped order. We can swap more than two variables that way.

#### The rest operator
Usually, if the array is longer than the list on the left hand side, the “extra” items are omitted.

For example, here only two items are take, while the rest are ignored:

```JavaScript title:app.js
let [name1, name2] = ['Julius', 'Caesar', 'Consul', 'of the Roman Republic'];

alert(name1); // Julius
alert(name2); // Caesar
// Further items were not assigned
```

If we’d like to also gather the omitted items, we can add one more parameter that gets “the rest” using `...`:

```JavaScript title:app.js
let [name1, name2, ...titles] = ['Julius', 'Caesar', 'Consul', 'of the Roman Republic'];

alert( titles ); // ['Consul', 'of the Roman Republic']
```

#### Default values
If the array is shorter than the list of variables on the left, there will be no errors. Absent values are considered undefined:

```JavaScript title:app.js
let [firstName, surname] = [];

alert(firstName); // undefined
alert(surname); // undefined
```

If we want a “default” value to replace the missing one, we can provide it using `=`:

```JavaScript title:app.js
// default values
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

alert(name); // Julius (from array)
alert(surname); // Anonymous (default used)
```

Default values can be more complex expressions or even function calls. They are evaluated only if the value is not provided.

For instance, here we use the `prompt` function for two defaults:

```JavaScript title:app.js
// runs only prompt for surname
let [name = prompt('name?'), surname = prompt('surname?')] = ["Julius"];

alert(name); // Julius (from array)
alert(surname); // whatever prompt gets
```

**Note:** the `prompt` will only run for the missing value (`surname`).