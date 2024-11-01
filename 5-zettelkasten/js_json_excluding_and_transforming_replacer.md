### Meta
2024-10-23 12:22
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
**State:** #completed 

### Excluding and transforming: replacer
The full syntax of `JSON.stringify` is:

```JavaScript title:app.js
let json = JSON.stringify(value[, replacer, space]);
```

`value`
A value to encode.

`replacer`
Array of properties to encode or a mapping function `function(key, value)`.

`space`
Amount of space to use for formatting.

Most of the time, `JSON.stringify` is used with the first argument only. If we need to fine-tune the replacement process, like to filter our circular references, we can use the second argument.

If we pass an array of properties to it, only these properties will be encoded. For instance:

```JavaScript title:app.js
let room = {
	number: 23,
};

let meetup = {
	title: "Conference",
	participants: [{name: "John"}, {name: "Alice"}].
	place: room // meetup references room
};

room.occupiedBy = meetup; // room references meetup

alert( JSON.stringify(meetup, ['title', 'participants']) );
// {"title":"Conference","participansts":[{},{}]}
```

Here we’re probably too strict. The property list is applied to the whole object structure. So the object in `participants` are empty, because `name` is not in the list.

Let’s include in the list every property except `room.occupiedBy` that would cause the circular reference:

```JavaScript title:app.js
let room = {
	number: 23,
};

let meet = {
	title: "Conference",
	participants: [{name: "John"}, {name: "Alice"}],
	place: room,
};

room.occupiedBy = meetup; // room reference meetup

alert( JSON.stringify(meetup, ['title', 'participants', 'place', 'name', 'numer']) );
/*
{
	"title":"Conference",
	"participants":[{"name":"John"},{"name":"Alice"}],
	"place":{"name":23},
}
*/
```

Now everything except `occupiedBy` is serialized. But the list of properties is quite long.

Fortunately, we can use a function instead of an array as the `replacer`.

The function will be called for every `(key, value)` pair and should return the “replaced” value, which will be used instead of the original one. Or `undefined` if the value is to be skipped.

In our case, we can return `value` “as if” for everything except `occupieadBy`, the code below return `undefined`:

```JavaScript title:app.js
let room = {
	number: 23,
};

let meetup = {
	title: "Conference",
	participants: [{name: "John"}, {name: "Alice"}],
	place: room, // meetup refence room
};

room.occupiedBy = meetup; // room references meetup

alert( JSON.stringify(meetup, function replacer(key, value) {
	alert(`${key}: ${value}`);
	return (key == 'occupiedBy') ? undefined : value;
}));

/* key:value pairs that come to replacer:
:             [object Object]
title:        Conference
participants: [object Object],[object Object]
0:            [object Object]
name:         John
1:            [object Object]
name:         Alice
place:        [object Object]
number:       23
occupiedBy: [object Object]
*/
```

Note that `replacer` gets every key/value pair including nested objects and array items. It is applied recursively. The value of `this` inside `replacer` is the object that contains the current property.

The first call is special. It is made using a special “wrapper object”: `{"": meetup}`. In other words, the first `(key, value)` pair has an empty key, and the value is the target object as a whole. That’s why the first line is `":[object Object]"` in the example above.

The idea is to provide as much power for `replacer` as possible: it has a chance to analyze and replace/skip even the whole object if necessary.