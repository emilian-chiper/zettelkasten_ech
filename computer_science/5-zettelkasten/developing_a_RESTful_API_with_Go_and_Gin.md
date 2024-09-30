### Meta
2024-09-29 12:27
**Tags:** [[tutorials]]
**Status:** #pending 

### Create a folder for your code
(1) Open terminal and change to your home directory
```BASH title:example.sh
cd
```

(2) Using the terminal, create a directory for your code called `web-service-gin`

```BASH title:example.sh
mkdir web-service-gin
cd web-service-gin
```

(3) Create a module to manage dependencies

```BASH title:example.sh
go mod init example/web-service-gin
```

This creates a `go.mod` file in which dependencies you add will be listed for tracking.

### Create the data
- To keep things simple, you’ll store data in memory.
- A more typical API would interact with a database.
- Note that storing data in memory means that the set of albums will be lost each time you stop the server, then recreated when you start it.

#### Write the code
(1) Using your text editor, create a file called `main.go` in the `web-services` directory.

(2) Into `main.go`, at the top of the file, specify

```GO title:main.go
package main
```

- This is a package declaration. A standalone program (as opposed to a library) is always in package `main`.

(3) Beneath the package declaration, declare the `album` struct. This is used to store album data in memory.

- Struct tags such as `json:"artist"` specify what a field’s name should be when the struct’s content are serialized into JSON. Without htem, the JSON would use the struct’s capitalized field names – a style not as common in JSON.

```GO title:main.go
// album represents data about a record album.
type album struct {
	ID string `json:"id"`
	Title string `json:"title"`
	Artist string `json:"artist"`
	Price float64 `json:"price"`
}
```

(4) Beneath the struct declaration, write the following slice of album structs containing data you’ll use to start.

```GO title:main.go
// albums slice to seed record album data
var albums = []album {
	{ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
	{ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
	{ID: "3", Title:"Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}
```

### Write a handler to return all items
- When the client makes a request at `GET/albums`, you want to return all the albums as JSON.
- To do this, we need:
	- logic to prepare a response,
	- code to map the request path to logic.
- This is the reverse of how they’ll be executed at runtime, but you’re adding dependencies first, then the code that depends on them.

#### Write the code
(1) Beneath the struct code added in the preceding section,  create a function to create JSON from the slice of album structs, writing the JSON into the response.

```GO title:main.go
// responds with the list of all albums as JSON
func getAlbums(c *gin.Context) {
	c.IndentedJSON(http.StatusOK, albums)
}
```

##### What happens
- `getAlbums` takes a `gin.Context` parameter. You can give this function any name – neither Gin nor Go require a particular function name format.
- `gin.Context` is the most important part of Gin. It requires request details, validates and serializes JSON, and more. Despite the similar name, this is different from Go’s built-in `context` package.
- Call `Context,IndentedJSON` to serialize the struct into JSON and add it to the response.
- The function’s first argument is the status code you want to send to the client. Here, `SatusOK` from the `net/http` package indicates `200 OK`.
- You can replace `Context.IndentedJSON` with a call to `Context.JSON` to send more compact JSON. In practice, the indented form is much easier to work with when debugging and the size difference is usually small.

(2) Near the top of `main.go`, just beneath the `albums` slice declaration, assing the handler function to an endpoint path.
- This sets up an association in which `getAlbums` handles requests to the `/albums` endpoint path.

```GO title:main.go
func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)

	router.Run("localhost:8080")
}
```

##### What happens
- We initialize a Gin router using `Default`.
- Use the `GET` function to associate the `GET HTTP` method and `/albums` path with a handler function.
- Note that you’re passing the  *name* of the `getAlbums` function. This is different from passing the *result* of the function, which you would do by passing `getAlbums()` (note the parenthesis).
- Use the `Run` function to attach the router to an `http.Server` and start the server.

(3) Near the top of `main.go`, just beneath the package declaration, import the required packages.

```GO title:main.go
package main

import {
	"net/http"

	"github.com/gin/gonic/gin"
}
```

(4) Save `main.go`.

#### Run the code
(1) Begin tracking the `Gin` module as a dependency.
- At the command line, use `go get` to add the `github.com/gin-gonic/gin` module as a dependency for your module.
- Use a  dot`.` argument to mean “get the dependencies for code in the current directory”.

```BASH title:example.sh
go get .
```

(2) From the command line in the directory containing `main.go`,  run the code.

```BASH title:example.sh
go run .
```

(3) From a new command line window, use `curl` to make a request to your running web service.

```BASH example.sh
curl http://localhost:8080/albums
```

- The command should display the data you seeded the service with.

```JSON title:albums.json
[
	{
		"id": "1",
		"title": "Blue Train",
		"artist": "John Coltrane",
		"price": 56.99
	},
	{
		"id": "2",
		"title": "Jeru",
		"artist": "Gerry Mulligan",
		"price": 17.99
	},
	{
		"id": "3",
		"title": "Sarah Vaughan and Clifford Brown",
		"artist": "Sarah Vaughan",
		"price": 39.99
	}
]
```


### Write a handler to add a new item
- When the client makes a `POST` request at `/albums`, you want to add the album described in the request body to the existing albums’ data.

#### Write the code
(1) Add code to add albums data to the list albums.
- Somewhere after the import statements, write:

```GO title:main.go
// adds an album from JSON received in the request body
funct postAlbums(c *gin.Context) {
	var newAlbum album

	// Call BindJSON to bind the received JSON to
	// newAlbum.
	if err := c.BindJSON(&newAlbum); err != nil {
		return
	}

	// Add the new album to the slice.
	albums = append(albums, newAlbum)
	c.IndentedJSON(http.StatusCreated, newAlbum)
}
```
- In this code, you:
	- Use `Context.BindJSON` to bind the request body to `newAlbum`.
	- Append the `album` struct initialized from the JSON to the `albums` slice.
	- Add a 201 status code to the response, along with JSON representing the album you added.

(2) Change your `main` function so that it includes the `router.POST` function, as follows:

```Go title:main.go
func main () {
	router := gin.Default()
	router.GET("/albums", getAlbums)
	router.POST("/albums", postAlbums)

	router.Run("localhost:8080")
}
```
- In this code, you:
	- Associate the `POST` method at the `/albums` path with the `postAlbums` function.
	- With `Gin`, you can associate a handler with a HTTP method-and-path combination. Thus, you can separately route requests sent to a single path based on the method the client is using.

#### Run the code
(1) If the server is still running from the last section, stop it.
(2) From the command line in the directory containing `main.go`, run

```BASH title:example.sh
go run .
```

(3) From a different command line window, use `curl` to make a request to your running web service.

```BASH title:example.sh
curl http://localhost:8080/albums \
  --include \
  --header: "Content-Type: application/json" \
  --request: "POST" \
  --data '{"id": "4","title": "The Modern Sound of Betty Carter","artist": "Betty Carter","price": 49.99}'
```
- The command should display headers and JSON for the added album.

```JSON title:response.json
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Date: Wed, 02 Jun 2021 00:34:12 GMT
Content-Length: 116

{
    "id": "4",
    "title": "The Modern Sound of Betty Carter",
    "artist": "Betty Carter",
    "price": 49.99
}

```

(4) As in the previous section, use `curl` to retrieve the full list of albums, to confirm that the new album was added:

```BASH title:example.sh
curl http://localhost:8080/albums \
    --header "Content-Type: application/json" \
    --request "GET"
```
- The command should display the album list.

```JSON title:response.json
[
	{
		"id": "1",
		"title": "Blue Train",
		"artist": "John Coltrane",
		"price": 56.99
	},
	{
		"id": "2",
		"title": "Jeru",
		"artist": "Gerry Mulligan",
		"price": 17.99
	},
	{
		"id": "3",
		"title": "Sarah Vaughan and Clifford Brown",
		"artist": "Sarah Vaughan",
		"price": 39.99
	},
	{
		"id": "4",
		"title": "The Modern Sound of Betty Carter",
		"artist": "Betty Carter",
		"price": 49.99
	}
]
```

### Write a handler to return a specific item
- When the client makes a request to `GET` `/albums/[id]`, you want to return the album whose ID matches the `id` path parameter.

#### Write the code
(1) Beneath the `postAlbums` function, create logic to retrieve album ID

```GO title:main.go
// locates the album whose ID value matches the id
// paraameter sent by the client, then returns that album as a response.
func getAlbumByID(c *gin.context) {
	id := c.Param("id")

	// Loop over the list of albums, looking for
	// an album whose ID value matches the parameter.
	for _, a := range albums {
		if a.ID == id {
			c.IndentedJSON(http.StatusOK, a)
			return
		}
	}
	c.IndentedJSON(http.StatusNotFound, gin.H{"message": "album not found"})
}
```
- In this code, you:
	- Use `Context.Param` to retrieve the `id` path parameter from the URL. When you map this handler to a path, you’ll include a placeholder for the parameter in the path.
	- Loop over the `album` structs in the slice, looking for one whose ID field value matches the `id` parameter value. If it’s found, you serialize that `album` struct to JSON and return it as a response with a `200 OK` HTTP code.
	- Return a HTTP `404 error` with `http.StatusNotFound` if the album isn’t found.

(2) Finally, change your `main` so that it includes a new call to `router.GET`, where the path is now `/albums/:id`.

```GO title:main.go
func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)
	router.GET("/albums/:id", getAlbumByID)
	router.POST("/albums", postAlbums)

	router.Run("localhost:8080")
}
```

- In this code, you associate the `/albums/:id` path with the `getAlbumByID` function. In Gin, the colon preceding an item in the path signifies that the item is a path parameter.

#### Run the code
(1) If the server is still running from the last section, stop it.
(2) From the command line in the directory containing `main.go`, run the code to start the server.

```BASH title:example.sh
go run .
```

(3) From a different command line window, use `curl` to make a request to your running web service.

```BASH title:example.sh
curl http://localhost:8080/albums/2
```

- The command should display JSON for the album whose ID you used. If the album wasn’t found, you’ll get JSON with an error message.

```JSON response.json
{
	"id": "2",
	"title": "Jeru",
	"artist": "Gerry Mulligan",
	"price": 17.99
}
```