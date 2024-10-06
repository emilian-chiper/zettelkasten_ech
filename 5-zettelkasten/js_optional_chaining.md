### Meta
2024-09-20 08:52
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_optional_chaining]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {};

alert( user?.address?.street); // undefined (no error)
```

### What it does
- Stops the evaluation if the value before `?.` is `undefined` or `null` and returns undefined.

### How it does it
- In other words, `value?.prop`:
	- works as `value.prop`, if `value` exists,
	- otherwise (when `value` is either `undefined` or `null`) it returns `undefined`.
- Here's an example with `document.querySelector()`:

```JavaScript title:app.js
let html = document.querySelector('.elem')?.innerHTML; // will be undefined if there's no element
```

- Reading the address with `user?.address` works even if `user` doesn't exist:

```JavaScript title:app.js
let user = null;

alert( user?.address ); // undefined
alert( user?.address.street ); // undefined
```

- **Note:** `?.` makes optional the value **before** it, but not any further.

#### Don't overuse optional chaining
- We should use `?.` only when it's ok that something doesn't exist.
- For example, if `user` must exist, but `address` is optional, then we should write `user.address?.stree`, **NOT** `user?.address?.street`.

#### The value before `?.` must be declared
- If there's no variable `user` at all, then `user?.anything` triggers an error.