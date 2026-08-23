# Backend Development 

A Javascript based backend.

A Javascript runtime: Nodejs / Deno / Bun.

In backend generally, either we have to handle data or file or Third Party Apis.

### Folder Structure
```
package.json
.env
Readme.md
git
lint
prettier
-- src
      index.js (db Connects)
      app.js  (config, cookie, urlencoded)
      constants (enums, dbname)
      -- DB
      -- Models
      -- Controllers
      -- Routes
      -- Middlewares
      -- Utils
      -- More (depends)


```
## How to deploy backend code  in production

First we have to download and install the Nodejs LTS version. Then Check the Version of Nodejs to check it is installed or not.

Check Version of Nodejs and NPM:
```
node -v
npm -v
```

There are two important packages we have to use for creating backend using Nodejs:
- Expressjs: Handles the Request and Response handling in backend.
- Mongoose: Handling interaction with the database and have methods for doing operations on database. 

Create the package.json and other installing the express etc:
```
npm init -y
npm install express

```

Create a file index.js and write some code:
```
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

package.json
```
{
  "name": "nodejs-dev",
  "version": "1.0.0",
  "description": "",
  "keywords": [
    "node"
  ],
  "license": "ISC",
  "author": "anshuman mishra",
  "type": "commonjs",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^5.2.1"
  }
}

```

Now we are ready for deploying this:
- Push this code to new Github repository
- Then Open the digital ocean or any cloud provider and select through github the repo and the branch name and add the environment variables and then deploy to the server.

## How to connect frontend and backend in javascript | Fullstack Proxy and Cors
`CORS`: CORS stands Cross Origin Resource Sharing.
It blocks the requests from different origin which may be different ip or port or domain etc.  
It origin same means url and port and every have to be same.

For solving this type of error generally handled by backend developer by whitelisting the url in the server using any package like cors so that the errors are stopped from coming.

But this is not only the single way, there are lot of ways to handle this.

- So the first way is using the npm package of cors to handle this. But it raises issues in production as it is not manadatory that the port will be same on the production also.

- Another method for solving this using frontend is by handling the proxy, so that we can run a proxy on the same url and port where the backend is running. So it gives the simulation to backend server that the request is coming from the same origin. These proxy configuration are given by different bundlers in frontend. So you have to search for it how to configure proxy in frontend to handle that. 
I mention how we handle it in the vite bunder for react application:  
#### If you are using create-react-app, then the method to handle the proxy is:
open the package.json and add this line:
```
"proxy":"http://localhost:4000"
```

#### If We are using Vite Bundler then:
We have to configure this in the vite.config file:
```
import react from "@vitejs/plugin-react";

export default defineConfig({
  server:{
  proxy:{
    '/api':"http://localhost:3000"
  }
  },
  plugins:[react()]
})
```

## Data Modelling for backend with mongoose
We can use different modelling tools for professional modelling first to make a database design. There are multiple data modelling tools available like Moon Modeler, Erase.io etc.

For Practice I am creating the models for handling todos using mongoose Schema:

- So create a `models` frolder in the project.  
- And inside the `models` folder create `todos` folder.  
- And inside the `todos` folder , create these files:

### `user.models.js`
```
import mongoose from 'mongoose';

const userSchema = new mongoose.Schema(
  {
    username: {
      type: String,
      required: true,
      unique: true,
      lowercase: true,
    },
    email: {
      type: String,
      required: true,
      unique: true,
      lowercase: true,
    },
    password: {
      type: String,
      required: true,
    },
  },
  {
    timestamps: true,
  }
);

export const User = mongoose.model('User', userSchema);

```

### `sub_todo.models.js`
```

```

### `todo.models.js`
```
import mongoose from 'mongoose';

const todoSchema = new mongoose.Schema(
  {
    content: {
      type: String,
      required: true,
    },
    complete: {
      type: Boolean,
      default: false,
    },
    createdBy: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'User',
    },
    subTodos: [
      {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'SubTodo',
      },
    ],
  },
  { timestamps: true }
);

export const Todo = mongoose.model('Todo', todoSchema);

```










