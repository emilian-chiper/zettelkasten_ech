### Meta
2024-10-23 08:53
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_date_and_time]]
**State:** #completed 

### Access date components
There are methods to access the year, month and so on from the `Date` object:
- `getFullYear()` – get the year (4 digits).
- `getMonth()` – get the month, from 0 to 11.
- `getDate()` – get the day of the month, form 1 to 31.
- `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()` – get the corresponding time components.
- `getDay()` – get the day of the week, from `0` (Sunday) to `6` (Saturday). The first day is always Sunday. In some countries, that’s not so, but can’t be changed.

**All methods above return the components relative to the local time zone.**

There are also their UTC-counterparts, that return day, month, year and so on for the time zone UTC+0: `getUTCFullYear()`, `getUTCMonth()`, `getUTCDay()`. Just insert the `"UTC"` right after `"get"`.

If your local time zone is shifted relative to UTC, then the code below shows different hours:
```JavaScript title:app.js
// current date
let date = new Date();

// the hour in your current time zone
alert( date.getHours() );

// the hour in UTC+0 time zone (London time without daylight savings)
alert( date.getUTCHours() );
```

Besides the given months, there are two special ones that do not have a UTC-variant:
- `getTime()` – returns the timestamp for the date, a number of milliseconds passed from the January 1st of 1970 UTC+0.
- `getTimezoneOffset()` – returns the difference between UTC and the local time zone, in minutes:
```JavaScript title:app.js
// if you are in timezone UTC-1, outputs 60
// if you are in timezone UTC+30, outputs -180
alert( new Date().getTimezoneOffset() );
```