### Meta
2024-10-03 21:51
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

### PostgreSQL Database Integration
**Module:** `pg-promise`
**Installation**
`$ nmp install pg-promise`

**Example**
```JavaScript title:app.js
const pgp = require('pg-promise')(/* options */)
const dp = pgp('postgress://username:password@host:port/database')

db.one('SELECT $1 AS value', 123)
  .then((data) => {
    console.log('DATA:', data.value)
  })
  .catch((error) => {
    console.log('ERROR:', error)
  })
```