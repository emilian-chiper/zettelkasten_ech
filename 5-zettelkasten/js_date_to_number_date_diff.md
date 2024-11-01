### Meta
2024-10-23 09:39
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_date_and_time]]
	**State:** #completed 

### Date to number, date diff
When a `Date` object is converted to number, it becomes the timestamp, same as `date.getTime()`:

```JavaScript title:app.js
let date = new Date();
alert(+date); // the number of milliseconds, same as date.getTime()
```

The important side effect: dates can be subtracted, the result is their difference in ms.

That can be used for time measurements:

```JavaScript title:app.js
let start = new Date(); // start measuring time

// do the job
for (let i = 0; 1 < 100000; i++) {
	let doSomething = i * i * i;
}

let end = new Date(); // end measuring time

alert( `The loop took ${end - start} ms`);
```