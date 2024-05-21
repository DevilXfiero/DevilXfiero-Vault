```js
// global object and functions
console.log();
setTimeout() // call function after a delay
clearTimeout(); 

setInterval(); // repeteadly call function after a delay
clearInterval();

window // Browsers represents global scope 
global // in Node we have global
var message = ''; // not added to the global object only scoped to the file because of node modular system
```

## Modules

Problem
In global scope same name function override the previous definition in global scope. 

Modules
Small building blocks to define variables and functions such that two variables or functions don't override same name variables and functions defined somewhere in other files.

Every file in node application is consider as module.

```js
console.log(module); // not global
```

Jshint tool to check errors

logger.js
```js
var url = "http://mylogger.io/log";

function log(message) {
  // Send HTTP request
  console.log(message);
}

// module.exports.log = log; // export an object
module.exports = log; // export function directly;
```

```js
const log = require("./logger");
log("message");
```

Node does not execute export code directly it always wraps code inside each module.
```js
function(exports, require, module, __filename, __dirname)
```

require -> Module Wrapper Function
## Path Module
```js
const path = require("path");

var pathObj = path.parse(__filename);
console.log(pathObj);
```

## OS Module
```js
const os = require("os");

var totalMemory = os.totalmem();
var freeMemory = os.freemem();

console.log(`Total Memory: ${totalMemory}`);
console.log(`Free Memory: ${freeMemory}`);
```

## File System Module
```js
const fs = require("fs");

const files = fs.readdirSync("./");
console.log(files);

fs.readdir("./", function (err, files) {
  if (err) console.log("Error", err);
  else console.log("Result", files);
}); // All async methods take function as a last argument and node call this function when operation complete we call this function as Callback
```

## Event

A signal that something has happened

## Events Module

```js
const EventEmitter = require("events"); // capital letter because it is a Class.
const emitter = new EventEmitter();

// Listener - function that is being called when event raised.
// Register a Listner
emitter.on("messageLogged", function () {
  console.log("Listener called");
});

// Raise an event
emitter.emit("messageLogged");
// Making a noise, produce- signalling
```

## Event Arguments
```js
const EventEmitter = require("events"); // capital letter because it is a Class.
const emitter = new EventEmitter();

// Register a Listner
emitter.on("messageLogged", (arg) => {
  // e, eventArg
  console.log("Listener called", arg);
});

// Raise an event
emitter.emit("messageLogged", { id: 1, url: "http://" });
```

If you need to use events within application you need to create a class that extends EventEmitter.

logger.js
```js
const EventEmitter = require("events");

var url = "http://mylogger.io/log";

class Logger extends EventEmitter {
  log(message) {
    // Send HTTP request
    console.log(message);

    // Raise an event
    this.emit("messageLogged", { id: 1, url: "http://" });
  }
}

module.exports = Logger;
```

app.js
```js
const EventEmitter = require("events");

const Logger = require("./logger");
const logger = new Logger();

// Register a Listner
logger.on("messageLogged", (arg) => {
  console.log("Listener called", arg);
});

logger.log("message");
```

## HTTP Module

```js
const http = require("http");

const server = http.createServer((req, res) => {
  if (req.url === "/") {
    res.write("Hello World");
    res.end();
  }
});

server.listen(3000);

console.log("Listening on port 3000...");
```

