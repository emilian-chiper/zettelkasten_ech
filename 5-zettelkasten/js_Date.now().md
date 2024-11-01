### Meta
2024-10-23 09:43
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_date_and_time]]
**State:** #completed 

### Date.now()
If we only want to measure time, we don’t need the `Date` object.

There’s a special method `Date.now()` that returns the current timestamp.

It is semantically equivalent to `new Date().getTime()`, but it doesn’t create an immediate `Date` object. It is thus faster and doesn’t apply pressure on garbage collection.

It’s used mostly for convenience or when performance matters, e.g. games.

So this is probably better:
```JavaScript title:app.js
let start = Date.now(); // ms count from 1 Jan 1970

// do the job
for (let i = 0; i < 100000; i++) {
	let doSomething = i * i * i;
}

let end = Date.now(); // done

alert( `The loop took ${end - start} ms` ); // subtract numbers, not dates
```