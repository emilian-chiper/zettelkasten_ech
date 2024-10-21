### Meta
2024-10-21 21:08
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_weakmap_and_weakset]]
**State:** #pending 

### WeakMap
The first difference between `Map` and `WeakMap` is that keys must be objects, not primitive values:

```JavaScript title:app.js
let weakMap = new WeakMap();

let obj = {};

weakMap.set(obj, "ok"); // works fine (object key)

// can't use a string as the key
weakMap.set("test", "Whoops"); // Error, because "test" is not an object
```

If we use an object as the key, and there are no other references to that object, it will be removed from memory (and from the map) automatically.

```JavaScript title:app.js
let john = { name: "John" };

let weakMap = new WeakMap();
weakMap.set(john, "...");

john = null; // overwrite the reference

// john is removed from memory
```

If `john` only exists as the key of `WeakMap` – it will be automatically deleted from the map (and memory).

`WeakMap` doesn’t support iteration and methods `keys()`, `values()`, `entries()`, so there’s no way to get all keys or values from it.

`WeakMap` has only the following methods:
- `weakMap.set(key, value)`
- `weakMap.get(key)`
- `weakMap.delete(key)`
- `weakMap.has(key)`

**Why such limitation?**
If an object has lost all other references (like `john` in the code above), then it is to be garbage-collected automatically. But technically it’s not exactly specified *when the cleanup happens*.

The JavaScript engine decides that. It may choose to perform the memory cleanup immediately or to wait and do the cleaning later when more deletions happen. So, technically, the current element count of a `WeakMap` is not known. The engine may have cleaned it up or not, or did it partially. For that reason, methods that access all keys/values are not supported.

#### Use case: additional data
The main area of application of `WeakMap` is *additional data storage*.

If we’re working on an object that “belongs” to another code, maybe even a third-party library, and would like to store some data associated with it, that should only exist while the object is alive – then `WeakMap` is exactly what’s needed.

We put the data to a `WeakMap`, using the object as the key, and when the object is garbage collected, that data will automatically disappear as well.

```JavaScript title:app.js
weaMap.set(john, "secret documents");
// if john dies, secret documents will be destroyed automatically
```

For instance, we have code that keeps a visit count for users. The information is stored in a map: a user object in the key and the visit count is the value. When a user leaves (its object gets garbage collected), we don’t want to store their visit count anymore.

Here’s an example of a counting function with `Map`:

```JavaScript title:app.js
// 📁 visitsCount.js
let visitCountMap = new Map(); // map: user => visits count

// increase the visits count
function countUser(user) {
	let count = visitsCountMap.get(user) || 0;
	visitsCountMap.set(user, count + 1);
}
```