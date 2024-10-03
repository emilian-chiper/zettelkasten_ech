### Meta
2024-10-03 21:34
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

### Basic routing
***Routing*** refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

Each route can have one or more handler functions, which are executed when the route is matched.

#### Route definition
Route definition takes the following structure

```JavaScript title:app.js
app.METHOD(PATH, HANDLER)
```

Where:
- `app` is an instance of `express`,
- `METHOD` is an [HTTP request method], in lowercase,
- `PATH` is a path on the server,
- `HADNLER` is the function executed when the route is matched.

#### Defining simple routes
Respond with `Hello World!` on the homepage:
```JavaScript title:app.js
app.get('/', (req, res) => {
	res.send('Hello World!')
})
```

Respond to POST request on the root route (` / `), the application's home page:

```JavaScript title:app.js
app.post('/', (req, res) => {
	res.send('Got a POST request');
})
```

Respond to a PUT request to the `/user` route:

```JavaScript title:app.js
res.put('/user', (req, res) => {
	res.send('Got a PUT request at /user');
})
```

Respond to a DELETE request to the `/user` route:

```JavaScript title:app.js
app.delete('/user', (req, res) => {
	res.send('Go a DELETE request at /user')
})
```
