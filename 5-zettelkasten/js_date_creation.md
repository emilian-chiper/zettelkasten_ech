### Meta
2024-10-23 08:34
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_date_and_time]]
**State:** #completed 

### Creation
To create a new `Date` object, call `new Date()` with one of the following arguments:

`new Date()`
Without arguments – create a `Date` object for the current date and time:

```JavaScript title:app.js
let now = new Date();
alert( now ); // shows current date/time
```

`new Date(milliseconds)`
Create a `date` object with the time equal to number of milliseconds (1/1000 of a second) passed after the Jan 1st of 1970 UTC+0.

```JavaScript title:app.js
// 0 means 01.01.1970 UTC+0
let Jan01_1970 = new Date(0);
alert( Jan01_1970 );

// now add 24 hours, get 02.01.1970 UTC+0
let Jan02_1970 = new Date(24 * 3600 * 1000);
alert( Jan02_1970 );
```

An integer number representing the number in milliseconds that has passed since the beginning of 1970 is called a *timestamp*.

It’s a lightweight numeric representation of a date. We can always create a date from a timestamp using `new Date(timestamp)` and convert the existing `Date` object to a timestamp using the `date.getTime()` method.

Dates before 01.01.1970 have negative timestamps, e.g.:
```JavaScript title:app.js
// 31 Dec 1969
let Dec31_1969 = new Date(-24 * 3600 * 1000);
alert( Dec31_1969 );
```

`new Date(datestring)`
If there is a single argument, and it’s a string, it is parsed automatically (same as `Date.parse`).

```JavaScript title:app.js
let date = new Date("2017-01-26");
alert(date);
```

`new Date(year, month, date, hours, minutes, seconds, ms)`
Create the date with the given components in the local time zone. Only the first two arguments are obligatory.
- The `year` should have 4 digits. For compatibility, 2 digits are also accepted and considered `19xx`, e.g. `98` is the same as `1998` here. Use 4 digits.
- The `month` count starts with `0` (Jan), up to `11` (Dec).
- The `date` parameter is actually the day of month. If absent, `1` is assumed.
- If `hours/minutes/seconds/ms` is absent, they are assumed to be equal `0`.

For instance:

```JavaScript title:app.js
new Date(2011, 0, 1, 0, 0, 0, 0); // 1 Jan 2011, 00:00:00
new Date(2011, 0, 1); // the same, hours etc are 0 by default
```

The maximal precision is 1 ms (1/1000 sec):
```JavaScript title:app.js
let Date = new Date(2011, 0, 1, 2, 3, 4, 567);
alert( date ); // 1.01.2011, 02:03:04.567
```