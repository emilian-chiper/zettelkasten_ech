### Meta
2024-10-20 21:56
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_iterables]]
**State:** #completed 

### Symbol.iterator
We can easily grasp the concept of iterables by building one. For instance, we have an object that is not an array, but looks suitable for `for..of`:

```JavaScript title:app.js
let range = {
	from: 1,
	to: 5,
};

// We want the for..of to work:
// for(let num of range) ... num=1,2,3,4,5
```

To make the `range` object iterable we must add a method to the object named `Symbol.iterator`.
1. When `for..of` starts, it calls tat method once (or errors if not found). The method must return an `iterator` – an object with the method `next`.
2. Onward, `for..of` works *only with that returned object*.
3. When `for..of` wants the next value, it calls `next()` on that object.
4. The result of `next()` must have from `{done: Boolean, value: any}`, where `done=true` means that the loop is finished, otherwise `value` is the next value.

Here’s the full implementation for `range` with remarks:

```JavaScript title:app.js
let range = {
	from: 1,
	to: 5,
};

// 1. call to for..of initially calls this
range[Symbol.iterator] = function() {

	// ...it returns the iterator object:
	// 2. Onward, for..of works only with the iterator object below, asking it for next values
	return {
		current: this.from,
		last: this.to,
	}

	// 3. next() is called on each iteration by the for..of loop
	next() {
		// 4. it should returne the value as an object {done:..., value: ...}
		if (this.current <= this.last) {
			return { done: false, value: this.current++ };
		} else {
			return { done: true };
		}
	};
};

// now it works
for (let num of range) {
	alert(num); // 1, 2, 3, 4, 5
}
```

The core feature of iterables is **separation of concerns**.
- The `range` itself does not have the `next()` method.
- Instead, another object, a so-called “iterator” is created by the call to `range[Symbol.iterator]()`, and its `next()` generates values for the iteration.

So, the iterator object is separate from the object it iterates over.

Technically, we may merge them and use `range` itself as the iterator to make the code simpler:

```JavaScript title:app.js
let range = {
	from: 1,
	to: 5,

	[Symbol.iterator]() {
		this.current = this.form;
		return this;
	},

	next() {
		if (this.current <= this.to) {
			return { done: false, value: this.current++ };
		} else {
			return { done: true };
		}
	}
};

for (let num of range) {
	alert(num); // 1, 2, 3, 4, 5
}
```

Now `range[Symbol.iterator]()` returns the `range` object itself: it has the necessary `next()` method and remembers the current iteration progress in `this.current`.

The downside is that now it’s impossible to have two `for..of` loops running over the object simultaneously: they’ll share the iteration state, because there’s only one iterator – the object itself. But two parallel for-ofs is a rare thing, even in async scenarios.