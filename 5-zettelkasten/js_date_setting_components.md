### Meta
2024-10-23 09:20
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_date_and_time]]
**State:** #completed 

### Setting date components
The following methods allow to set date/time components:
- `setFullYear(year, [month], [date])`
- `setMonth(month, [date])`
- `setDate(date)`
- `setHours(hour, [min], [sec], [ms])`
- `setMinutes(min, [sec], [ms]`
- `setSeconds(sec, [ms])`
- `setMilliseconds(ms)`
- `setTime(milliseconds)` (sets the whole date by milliseconds since 01.01.1970 UTC)

Every one of them except `setTime()` has a UTC-variant, such as `setUTCHours()`.

Some methods can set multiple components at once, for example `setHours`. The components that aren’t mentioned aren’t modified. For instance:
```JavaScript title:app.js
let today = new Date();

today.setHours(0);
alert(today); // still today, but the hours changed to 0

today.setHours(0, 0, 0, 0);
alert(today); // still today, now 00:00:00 sharp
```