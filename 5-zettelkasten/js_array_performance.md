### Meta
2024-10-14 12:47
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

Methods `push/pop` run fast, while `shift/unshift` are slow.

Why is it faster to work with the end of an array that with its beginning? Let’s see what happens during the execution:

```JavaScript title:app.js
fruits.shift(); // take 1 element from the start
```

It’s not enough to take and remove the element with the index `0`. Other elements need to be renumbered as well.

The `shift` operation must do 3 things:
1. Remove the element with the index `0`.
2. Move all elements to the left, renumber them from the index `1` to `0`, from `2` to `1`, etc.
3. Update the `length` property.

**The more elements in the array, the more time to move them, more in-memory operations.**

Similar things happen with `unshift`: to add an element to the beginning of the array, we need first to move existing elements to the right, increasing their indexes.

What’s with `push/pop`? They do not need to move anything. To extract an element from the end, `pop` cleans the index and shortens `length`.

The actions for the `pop` operation:

```JavaScript title:app.js
fruits.pop(); // take 1 element from the end
```

**The `pop` method doesn’t need to move anything, because other elements keep their indexes.**

`push` operates similarly.