### Meta
2024-10-16 10:20
**Tags:**
**Status:** #pending 

### What is the PERN Stack?
A set of technologies to build web or mobile apps. It is comprised of four key components: PostgreSQL, Express, React, and Node.js. When the components are combined, you can build a full stack app with CRUD operations.

#### PostgreSQL
PostgreSQL is an open-source object-relational **database** management system (ORDBMS) that supports both SQL (relational) and JSON (non-relational) querying. It’s ACID -compliant and table-based, with complete constraints, triggers and roles. These features are what allow for the creation of relationships between data. This, in turn, leads to benefits such as extensibility, scalability, reliability, performance, and robustness.

#### Express
Express is a popular and free JavaScript web framework designed for use with Node.js. Its purpose is to build web applications, especially **APIs**, quickly and easily. It provides a set of  features for the routing, middleware and handling of HTTP requests and responses. In the PERN Stack, this component handles the application **back-end**.

#### React
React is a JavaScript library for building **user interfaces**. In this stack, this component is responsible for the **front-end**.

#### Node.js
Node.js is a **JavaScript runtime** for developing server-side and networking applications, such as web servers.

### How to Implement the PERN Stack

#### Prerequisites
First, ensure the right tools are present on your system:
- Container machine, such as [[docker|Docker]]
- [[node.js|Node.js]]
- Code editor, such as VSCode
- npx (deprecated, use npm exec instead)
- (Optional) pgAdmin
- (Optional) Postman or Insomnia
- (Optional) nodemon

#### Step 1: Project Structure
##### Build a new folder for the project
This main directory should contain two sub-directories: `/server` and `/client`, each containing only the files related to the server (API) and the client (UI), respectively. This will help keep your project clean and organized.

##### Initialize the project
**Server:** Initialize the project using `npm init` in the server folder to create a Node.js project. Next, install the required dependencies for this basic PERN Stack example using `npm`:
- express, to use Express web framework in the project,
- pg, to use PostgreSQL in the project,
- dotenv, to securely store and manage environment variables in the project, while separating them form code.

**Client:** Initialize the project using `npx create-react-app` (vite) in the client directory. After that, we must install the required dependencies, this time for the front-end:
- axios: to enable making HTTP requests from the front-end.

#### Step 2: Database
##### Set up PostgreSQL
To simplify this example, we need a PostgreSQL container instead of configuring it manually. To do so, we need to use a Docker PosgreSQL image:

```BASH title:script.sh
docker run --name <container_name> -e POSTGRES_USER=<postgres_user> -e POSTGRES_PASSWORD=<postgres_password> -p 5432:5432 -d postgres 
```

##### Create the database and populate it
- Create a SQL script that runs and populates the database, for example:

```SQL title:init.sql
--- Create a table for the database
CREATE TABLE public.products
(
    product_id SERIAL NOT NULL,
    name character varying(50) NOT NULL,
    price real NOT NULL,
    description text NOT NULL,
    PRIMARY KEY (product_id)
);

-- Seed data for products table
INSERT INTO public.products (product_id, name, price, description) VALUES (1,  'Product 1', 9.00, 'Product 1 description.');
INSERT INTO public.products (product_id, name, price, description) VALUES (2,  'Product 2', 7.19, 'Product 2 description.');
INSERT INTO public.products (product_id, name, price, description) VALUES (3, 'Product 3', 9.29, 'Product 3 description.');
INSERT INTO public.products (product_id, name, price, description) VALUES (4,  'Product 4', 6.45, 'Product 4 description.');
```

After that, copy the SQL script to the inside of the container and execute it:

```BASH title:script.sh
docker cp ./<path_to_file>/init.sql <container_name>:/tmp/init.sql

docker exec -ti <container_name> /bin/bash -c "psql -U <postgres_user> -d <postgres_database> -f /tmp/init.sql"
```

Alternatively, if you want, you can do it by:
- Establishing a bash session with `docker exect -ti <container_id> bash` and then use `psql`;
- Using pgAdmin.

#### Step 3: Building the API
The API starting point is `index.js`, the file you need to create in the server folder. This file will define all the routes and import express. Additionally, it also has the necessary configurations set so that Node.js server runs on the desired port and starts listening for incoming requests.

##### Create the API
Change the file `index.js` to create the API:

```JavaScript title:app.js
equire("dotenv").config({ path: __dirname + "/.env" });
const express = require('express');

const app = express();

const PORT = process.env.PORT || 9000;

//Here you can add your routes
//Here's an example
app.get("/", (req, res) => {
    res.send("Hello World!");
  });

app.listen(PORT, () => {
    console.log(`Server listening on the port  ${PORT}`);
})
```

##### Run the API
Now, if you run `node index.js` or `npx nodemon index.js` in terminal, the following message will show up on your console:
```BASH title:scripth.sh
Server listening to port 9000
```

##### Test the API
To test if the API is working use Postman to make the request. In this case, a simple GET request to `http://localhost:9000/` should return the string “Hello World!”.

**Note**
This is just the basis of the PERN Stack. Normally, a web app requires numerous requests that can make projects a little bit confusing. To organize larger projects, there are optional files that we can use:
- Rotues: forward the requests to the appropriate controller functions, to handle them;
- Controllers: contain functions to handle specific routes and determine the appropriate response to send back to the user;
- Services: contain functions to handle possible errors;
- Database files: contain functions to perform CRUD operations in a database.

#### Step 4: Configure PostgreSQL connection
##### Create a connection between the database and the API
We need to create a file, `db.config.js`, a configuration file which we connect to PostgreSQL with the help of a connection string.

Below we’re using `pg` to create a connection pool, which is a cache of database connections maintained for efficient reuse in future database requests.

```JavaScript title:db.config.js
require("dotenv").config();
const { Pool } = require("pg");

const database = process.env.PGDATABASE;

const connectionString = `postgresql://${process.env.PGUSER}:${process.env.PGPASSWORD}@${process.env.PGHOST}:${process.env.PGPORT}/${database}`;

const pool = new Pool({
	connectionString: connectionString,
});

module.exports = {
	query: (text, params) => pool.query(text, params),
	end: () => pool.end(),
};
```

To check if the connection is working, let’s create a route for the products, in this case, on `index.js`.

```JavaScript title:index.js
require("dotenv").config({ path: __dirname + "/.env" });
const express = require('express');
const pool = require(__dirname + "/config/db.config.js");

const app = express();

const PORT = process.env.PORT || 9000;

//Functions
const getProducts =  (req, res) => {
  pool.query('SELECT * FROM products', (error, products) => {
    if (error) {
      throw error
    }
    res.status(200).json(products.rows)
  })
}

//Here you can add your routes
//Here's an example
app.get("/", (req, res) => {
    res.send("Hello World!");
  });

app.get('/products', getProducts)

app.listen(PORT, () => {
    console.log(`Server listening on the port  ${PORT}`);
})
```

#### Step 5: Externalize Environment Variables
The request above won’t work because we’re using the `dotenv` library, which loads variables from a `.env` file, which we haven’t yet set up, into `process.env`.

##### Create a .env file
To do so, create a `.env` file inside `/server` and put the value of the variables there.

```YAML title:.env
#DATABASE_INFO
PGDATABASE=pern_example
PGUSER=pern_example
PGPASSWORD=12345678
PGHOST=localhost
PGPORT=5423

#SERVER_INFO
PORT=9000
```

Now, make a GET request to `http://localhost:9000/products` and make sure the server is running.

#### Step 6: Make API calls from UI
To deliver responses to client requests, our UI needs to get data from the API by making API calls. We have two options for this:
- Axios,
- Fetch.

##### Change client package.json
To let the client-side use the server-side for requests, add the code line `"proxy": "http://localhost:9000"` to the client `package.json` file.

##### Modify client App.js file
```JavaScript title:App.js
import './App.css';
import axios from 'axios';
import React, {useState, useEffect} from 'react';
import 'bootstrap/dist/css/bootstrap.min.css'


function App() {

  const [data, setData] = useState([]);

  useEffect(() => {
    axios
    .get('/products')
    .then(res => res.data)
    .then(data => setData(data));
  }, []);

  return (
    <div className='container my-5' style={{ display: 'flex', justifyContent: 'center', alignItems: 'center'}}>
      <table className='table table-striped'>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Price</th>
            <th>Description</th>
          </tr>
        </thead>
          <tbody>
            { data.map(item => (
              <tr key={item.product_id}>
                <td>{item.product_id}</td>
                <td>{item.name}</td>
                <td>{item.price}</td>
                <td>{item.description}</td>
              </tr>
            ))}
          </tbody>
        </table> 
      </div>
  )};

export default App;
```

This file imports axios, so we can communicate with server-side from client-side. Then, it also imports **useState** and **useEffect**:
- **useState**: a React hook that allows declaring a state variable and its setter function to update the state;
- **useEffect:** a React hook that allows declaring an effect that should run after every render, in this case, or when certain values change.

To make the response data more visually appealing, style it.

##### Run the client-side
To run the client-side, run `npm start` in terminal.

#### Step 7: Building UI
You can organize your project using:
- Components: reusable code for creating UI,
- Pages: different routes or sections of the app, responsible for rendering the content from a specific route,
- Contexts: way to pass data through the component tree,
- Services: API requests.

### Dockerizing the Application
Finally, create images for both front-end and back-end.

#### Step 1: Create Dockerfiles
Create a `Dockerfile` in each directory, `/server` and `/client`. These files will be used to build both Docker images, which can be then run as Docker containers.

##### Dockerfile for server-side
```YAML title:Dockerfile

FROM node:19-alpine

WORKDIR /home/node/app

COPY . .

RUN chown -R node:node .

USER node

RUN npm install

EXPOSE 9000

CMD [ "node", "index.js" ]
```

##### Dockerfile for client-side
```YAML title:Dockerfile

FROM node:19-alpine

WORKDIR /home/node/app

COPY . .

RUN chown -R node:node .

USER node

RUN npm install

EXPOSE 3000

CMD [ "npm", "start" ]
```

#### Step 2: Create .dockerignore files
Next, for cleaner installation of Node packages, let’s create a `.dockerignore` fire in both `/server` and `/client` folders. In this case, this file will ignore the `node_modules` directory from being copied to the containers, since we already run `npm install` on `Dockerfile`.

```YAML title:.dockerignore
node_modules
```

#### Step 3: Build the docker images
You now have the required files, but you need to **build the images** by running the following command on the `/server` and `/client` subdirectories:

```BASH title:script.sh
docker build -t server:latest .

docker build -t client:latest .
```

#### Step 4: Create containers
Run the images to create containers:

```BASH title:script.sh
docker run --name <container_name> -p 9000:9000 -d server

docker run --name <container_name> -p 3000:3000 -d client
```

Now that  you have all the containers needed for the PERN stack to work, you’ll notice nothing is working because the connections between the containers are broken.

To fix this, we could inspect the container’s IP addresses with `docker inspect <container-name>` and change the `.env` file (`PG_HOST`) from the server-side and `package.json` (`proxy`) from the client-side with the respective values. However, there’s a cleaner way to do it:

#### Step 5: Create docker bridge network
```BASH title:script.sh
docker network create <network_name>
```

#### Step 6: Connect the containers
Connect the three containers to the network by running the following command for each one:

```BASH title:script.sh
docker network connect <network_name> <container_name>
```

#### Step 7: Last configurations
Change the `.env` file (server-side) and `package.json` (client-side) with the name of the containers to connect. Finally, rebuild and rerun the containers:

```YAML title:.env
#DATABASE_INFO
PGDATABASE=pern_example
PGUSER=pern_example
PGPASSWORD=12345678
PGHOST=some_postgres #change here!!!
PGPORT=5432

#SERVER_INFO
PORT=9000
```

```JSON title:package.json
{
  "name": "client",
  "version": "0.1.0",
  "private": true,
  "proxy": "http://server-side:9000"
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "axios": "^1.2.4",
    "bootstrap": "^5.2.3",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```