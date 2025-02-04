### Meta
2024-10-23 12:56
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
**State:** #completed 

### Custom “toJSON”
Like `toString` for string conversion, an object may provide method `toJSON` for to-JSON conversion. `JSON.stringify` automatically calls it if available.

```JavaScript title:app.js
let room = {
	number: 23,
};

let meetup = {
	title: "Conference",
	date: new Date(Date.UTC(2017, 0, 1)),
	room
};

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "date":"2017-01-01T00:00:00.000Z",  // (1)
    "room": {"number":23}               // (2)
  }
*/
```

Here we can see that `date` `(1)` became a string. That’s because all dates have a built-in `toJSON` method which returns such kin of string.

Now let’s add a custom `toJSON` for our object `room` `(2)`:

```JavaScript title:app.js
let room = {
	number: 23,
	toJSON() {
		return this.number;
	}
};

let meetup = {
	title: "Conference",
	room,
};

alert( JSON.stringify(room) ); // 23

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "room": 23
  }
*/
```