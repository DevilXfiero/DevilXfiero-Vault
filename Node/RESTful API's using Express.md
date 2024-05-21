REST - Representational State Transfer

## Express
```js
const express = require("express");
const app = express();

app.get()
app.post()
app.put()
app.delete()
```

To fix stop and reload on file change

 sudo npm i -g nodemon 
 nodemon app.js

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello World!!!");
});

app.get("/api/courses", (req, res) => {
  res.send([1, 2, 3]);
});

app.listen(3000, () => console.log("Listening on port 3000..."));
```

## Environment Variables

export PORT=3000  -> to set port in env variable 

```js
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Listening on port ${port}...`));
```

localhost:3000/api/2024/1?sortBy=name
Route param = 2024, 1 = Essential or required values 
QueryString param = added after ? sortBy = anything that is optional

```js
app.get("/api/courses/:id", (req, res) => {
  const queryParams = req.query;
  res.send(req.params.id);
});
```

```js
const express = require("express");
const Joi = require("joi");
const app = express();

app.use(express.json()); // adding middelware to get request as json

const courses = [
  { id: 1, name: "course1" },
  { id: 2, name: "course2" },
  { id: 3, name: "course3" },
];
app.get("/", (req, res) => {
  res.send("Hello World!!!");
});

app.get("/api/courses", (req, res) => {
  res.send(courses);
});

app.get("/api/courses/:id", (req, res) => {
  const course = courses.find((c) => c.id === parseInt(req.params.id));
  if (!course)
    res.status(404).send("The coures with the given ID was not found");
  res.send(course);
});

app.post("/api/courses", (req, res) => {
  const { error } = validateCourse(req.body);
  if (error) res.status(400).send(error.message);

  const course = {
    id: courses.length + 1,
    name: req.body.name,
  };
  courses.push(course);
  res.send(course);
});

app.put("/api/courses/:id", (req, res) => {
  const course = courses.find((c) => c.id === parseInt(req.params.id));
  if (!course)
    return res.status(404).send("The course with given ID was not found");
  const { error } = validateCourse(req.body);
  if (error) return res.status(400).send(error.message);

  course.name = req.body.name;
  res.send(course);
});

function validateCourse(course) {
  const schema = Joi.object({
    name: Joi.string().min(3).required(),
  });
  return schema.validate(course);
}

app.delete("/api/courses/:id", (req, res) => {
  const course = courses.find((c) => c.id === parseInt(req.params.id));
  if (!course)
    return res.status(404).send("The course with given ID was not found");

  const index = courses.indexOf(course);
  courses.splice(index, 1);

  res.send(course);
});

const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Listening on port ${port}...`));
```


## Middleware 
Middleware function is a function that takes request object and either return response to client or passes control to another middleware function

Request goes through a pipeline called Request Processing Pipeline.

Request -> json() -> route() -> Response

We can do logging, authentication, authorization etc.

### Custom middleware function

logger.js
```js
function log(req, res, next) {
  console.log("Logging...");
  next(); // to pass control to the next middleware function
}

module.exports = log;
```

index.js
```js
const express = require("express");
const Joi = require("joi");
const logger = require("./logger");
const app = express();


app.use(logger);

app.use(function (req, res, next) {
  console.log("Authenticating...");
  next();
});
```

## Built-in Middleware
```js
app.use(express.json());
app.use(express.static('public'));
```

## Third-party Middleware

npm i helmet
npm i morgan

## Environments
```js
console.log(`NODE_ENV : ${process.env.NODE_ENV}`);
console.log(`app: ${app.get("env")}`);

if (app.get("env") === "development") {
  app.use(morgan("tiny"));
  console.log("Morgan enabled...");
}
```

export NODE_ENV=production 

## Configuration

npm rc 
npm i config

create config folder

development.json
```json
{
  "name": "My Express App - Development",
  "mail": {
    "host": "dev-mail-server"
  }
}
```

production.json
```json
{
  "name": "My Express App - Production",
  "mail": {
    "host": "prod-mail-server"
  }
}
```

index.js
```js
const config = require("config");
// Configuration
console.log("Application Name: " + config.get("name"));
console.log("Mail Server: " + config.get("mail.host"));
```

export NODE_ENV=production 

But don't store secret or password in it

Store them in environment variables

export app_password=1234

Inside config folder create
custom-environment-variables.json
```json
{
  "mail": {
    "password": "app_password"
  }
}
```

index.js
```js
console.log("Mail Password: " + config.get("mail.password"));
```

## Debugging

sudo npm i debug  

```js
const startupDebugger = require("debug")("app:startup");
const dbDebugger = require("debug")("app:db");

if (app.get("env") === "development") {
  app.use(morgan("tiny"));
  startupDebugger("Morgan enabled...");
}
```

export DEBUG=app:startup,app:db  // to see messages from particular debuggers
export DEBUG=app:*

also do
DEBUG=app:db nodemon index.js

## Templating engines

Sometimes you want to return HTML markup language instead of JSON

1.Pug
2.Mustache
3.EJS

npm i pug

```js
app.set("view engine", "pug");
app.set("views", "./views"); // default path where templates are stored

app.get("/", (req, res) => {
  res.render("index", { title: "My Express App", message: "Hello" });
});
```

Create views folder and index.pug file inside it.

index.pug
```pug
html 
  head 
     title= title 
  body
     h1= message  
```

## Database Integration

Install driver then you will get module for simple api to connect and work.

