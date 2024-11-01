### Meta
2024-10-23 17:43
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
	**State:** #completed 

### Using reviver
We received a stringified `meetup` object from the server. It looks like this

```JavaScript title:app.js
// title: (meetup title), date: (meetup date)
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';
```

Now we must *deserialize* it, to turn it back into a JavaScript object.

We can use `JSON.parse`:

```JavaScript title:app.js
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str);

alert( meetup.date.getDate() ); // Error!
```

The value of `meetup.date` is a string, not a `Date` object. How could `JSON.parse` know that it should transform that string into a `Date`?

Let’s pass `JSON.parse` the reviving function as the second argument. It returns all values “as is”, but `date` will become a `Date`:

```JavaScript title:app.js
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

alert( meetup.date.getDate() ); // now works!
```

Also works for nested objects:

```JavaScript title:app.js
let schedule = `{
  "meetups": [
    {"title":"Conference","date":"2017-11-30T12:00:00.000Z"},
    {"title":"Birthday","date":"2017-04-18T12:00:00.000Z"}
  ]
}`;

schedule = JSON.parse(schedule, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

alert( schedule.meetups[1].date.getDate() ); // works!
```