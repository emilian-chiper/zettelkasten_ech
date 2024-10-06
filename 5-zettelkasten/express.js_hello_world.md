### Meta
2024-10-03 21:30
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

### What it looks like

```JavaScript title:app.js
const express = require('express' 4.18.2)
const app = express()
const port = 3000

app.get('/', (req, res) => {
    res.send('Hello World!')
})

app.listen(port, () => {
    console.log(`Example app listending on port ${port})
})
```

### What's going on?
This app starts a server and listens on port 3000 for connections.

The app responds with "Hello World!" for requests to the root URL (`/` ) or *route*.
For every other path, it will respond with a `404 Not Found`.

### Running locally
Create a directory named `myapp`, change to it and run `npm init`.
Install `express` as a dependency.

In the `myapp` directory, create a file named `app.js`, and copy the code from the example above.

Run the app with `node app.js`.
