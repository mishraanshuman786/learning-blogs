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

## How to connect frontend and backend in javascript






