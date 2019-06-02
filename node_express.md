# Node.js

## Setup and basics

- `npm init` to start a project
  - `npm install <module>` to add that dependency
  - `npm install` to add all dependencies listed in `package.json` to the local project
- run `node <filename>` to run file

## Modules

### Exports (CommonJS)

- `module.exports` used to expose an object as a module/
  - `module.exports` and `exports` are basically the same; `exports` is a plain JS var that happens to be set to `module.exports`
  - `./` is necessary in `require` if it's a local module
- Consider the following code in `myModule.js`:
  ```
  var func1 = function() { ... };
  var num = 56;
  exports.f1 = func1;
  exports.n = num;
  ```
- This "exposes" `func1` and `num`, such that in the calling code you can use

  ```
  var m = require('./myModule);
  m.f1();
  var newNum = m.n + 1;
  ...
  ```

### `path`

- Work with file/directory paths, e.g. `join`, `format`, `parse`

### `os`

- Used to access operating system-specific stuff like `cpus`, `arch`, `totalmem`

### `fs` (File system)

- Utility for working with files, including `mkdir`, `rename`, `read`, and `write`
- Most of these are asynchronous (use callbacks) (although there are also synchronous versions)

### `events`

- **Emitters** emit named events that cause **listeners** to be called
- Objects that are instances of `EventEmitter` class have a `eventEmitter.on(eventName, listener)` function, where `listener` is the callback function
- When the EventEmitter object emits an event using `emitter.emit(eventName[, ...args])`, all of the functions attached to that specific event (i.e. that have `.on(eventName`) are called synchronously

### `http`

- **client-server model**: browser (client) submits HTTP request message to server, which provides resources, returning a response to the client
  - browser is an example of a **user agent**
- `http.createServer([options][, requestListener])` where `options` includes `IncomingMessage` (req in the example) and `ServerResponse` (res) and returns a new instance of `http.Server`
- `server.listen(5000)` starts the HTTP server on port 5000 and listens for connections. Can also have a callback
- See more: [**HTTP messages**](#HTTP-request-methods)

## Loading HTML

- Much easier with frameworks like Express
- `request.end([data[, encoding]][, callback])` finishes sending the request, flushes data to the stream
  - can put HTML code straight into here
- You can only access the webpage when the server is running
- **nodemon** is a tool that allows you to restart Node.js apps automatically after filesystem changes
  - If you update something, you normally have to close and manually restart the process to see the update. With nodemon, you don't have to
  - Can use `npm i -D nodemon` to install as a dev dependency
  - Check `package.json` for the nodemon dependency and script, then use `npm run dev` in this case to start
- This only works for local hosting--can use something like Heroku to deploy the app online

# Server-side concepts

## RESTful APIs

- **REST: Representational State Transfer** is a software architecture style for web services
- Usually use **HTTP**
- Flexible design allowing data return in XML, JSON, YAML, etc.
- Constraints of RESTful APIs:
  - _Client-server_: client and server should be separate; changing one doesn't affect the other
  - _Stateless_: each call can be made independently; there is no data stored on the server or in sessions
  - _Cacheable_: caching done on client side when needed, for efficiency
  - <mark>_Uniform interface_: API layer should be independent of the server?</mark>
  - _Layered system_: different layers with specific responsabilities working together
  - _Code on demand_: (optional)

# Express

## Basics

- **Express** is a backend web framework for Node.js (not comparable to client-side frameworks like React, Angular, Vue)
- Makes building Node webapps much simpler
- Backend apps (rendering pages) as well as API stuff (returning JSON)
- **Middleware functions** have access to both **request** and **response** objects
  - Can execute any code, make changes to these objects, end response cycle, and call next middleware in the stack

## Static directory

- Set a **static directory** to avoid all the `get`, `res`, `req` BS
  - `express().use(express.static(DIRECTORY))`

## Routing

### HTTP request methods

- Client sends **requests** to the server; server sends **responses**
- Request messages include **request methods**
- **GET**: retrieve data
- **HEAD**: like GET, but no response body
- **POST**: adding stuff to the server (e.g. adding an item to a database, data submitted from a webform)

<mark>MORE</mark>

### Express routing

- **Routing**: how an app responds to a client request to a certain endpoint
- Structure: `app.method(path, handler)`
  - `app` is an instance of `express()`
  - `method` is an **HTTP request method**
  - `path` is a path on the server
  - `handler` is the function executed when route is matched
- Example:
  ```
  app.get('/', (req, res) => {
      res.send("lmao okay");
  })
  ```

#### Route paths

- Route paths can have regex matchers, e.g. `'/ab*cd'` matches `abccd`, `abOKOKcd`, etc.

#### Route parameters

- Named URL segments that capture values specified at their position in the URL, which then populate the `req.params` object

<mark><h1>Stuck on routing, Express JS crash course </h1></mark>
