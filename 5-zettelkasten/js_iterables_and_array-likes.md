### Meta
2024-10-20 22:37
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

Two official terms look similar, but are very different. Please make sure you understand them well to avoid the confusion.
- *Iterables* are objects that implement the `Symbol.iterator` method.
- *Array-likes* are objects that have indexes and `length`, so they look like arrays.

When we use JavaScript for practical tasks in a browser or any other environment, we may meet objects that are iterables or array-likes, or both.

For instance, strings are both iterable (`for..of` works on them) and array-like (they have numeric indexes and `length`).

But an iterable may not be array-like. And vice-versa, an array-like may not be iterable.

Here’s an object that is array-like, but not iterable:

```JavaScript title:app.js
let arrayLike = {
	0: "Hello",
	1: "World",
	length: 2
};

// Error (no Symbol.iterator)
for (let item of arrayLike) {}
```

Both iterables and array-likes are usually *not arrays*, they don’t have `push`, `pop`, etc. That’s rather inconvenient if we have such an object and want to work with it as with an array. For example, we would like to work with `range` using array methods.