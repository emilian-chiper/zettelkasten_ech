### Meta
2024-10-21 20:29
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_weakmap_and_weakset]]
**State:** #completed 

### WeakMap and WeakSet
The JavaScript engine keeps a value in memory while it is “reachable” and can potentially be used. For instance:

```JavaScript title:app.js
let jon = { name: "Jon" };

// the object can be accessed, john is the reference for it

// overwrite the reference
jon = null;

// the object will be removed from memory
```

Usually, properties of an object or elements of an array or another data structure are considered reachable and kept in memory while the data structure is in memory.

For instance, if we put an object into an array, then while the array is alive, the object will be alive as well, even if there are no other references to it.

```JavaScript title:app.js
let jon = { name: "Jon" };

let arr = [ jon ];

jon = null; // overwrite the reference

// the object previously referenced by jon is stored inside the array
// therefore it won't be garbage-collected
// we can access it as arr[0]
```

Similar to that, if we use an object as the key in a regular `Map`, then while the `Map` exists, that object exists as well. It occupies memory and may not be garbage collected.

```JavaScript title:app.js
let jon = { name: "Jon" };

let map = new Map();
map.set(jon, "...");

jon = null; // overwrite the reference

// jon is stored inside the map
// we can access it by using map.keys()
```

`WeakMap` is fundamentally different in this aspect. It doesn’t prevent garbage-collection of keys objects.

The most notable limitation of `WeakMap` and `WeakSet` is the absence of iterations, and the inability to get the current content. That may appear inconvenient, but doesn’t prevent these data structures from doing their main job – “additional” storage of data for objects which are stored/managed at another place.