# http-and-web-standard Model

## Understanding how Http, DNS and TCP/IP work

### What is a Server and How Does it Work on a Higher Level?
The server is responsible for validating credentials, interacting with the database, and deciding how to respond to each request.

Each server response includes an HTTP status code, which tells the client what happened. These status codes let the client know whether a request succeeded or failed and why.

For example:

200 means that everything was OK.

404 means that the resource was not found on the server.

500 means that there was an internal server error.

503 means that the server is temporarily unavailable.

And so on…

Each status code has its own unique meaning.

If the data is updated dynamically or the application needs some sort of communication with a database, servers are very likely key components of the communication process.

These are some of the main types of servers:

Web servers deliver web content, such as HTML pages, images, and CSS files, to browsers.

Application servers handle business logic, process user input, and coordinate responses.

Database servers run database management systems and store, retrieve, and manage data.

Mail servers send, receive, and store email messages.

File servers manage access to files and allow them to be stored and shared across a network.

Proxy servers act as intermediaries between clients and other servers, often used for caching, security, or traffic control.

Servers are the backbone of the powerful online platforms we use every day. They make it possible to run complex logic, store and process large amounts of data, and support millions of users at the same time. 

### What is DNS and How Does it Work at a High Level?
