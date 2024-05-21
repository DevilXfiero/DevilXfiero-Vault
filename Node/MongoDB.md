npm i mongoose

```js
const mongoose = require("mongoose");

mongoose
  .connect("mongodb://localhost/playground")
  .then(() => console.log("Connected to MongoDB..."))
  .catch((err) => console.error("Could not connect to MongoDB", err));
```

## Schemas

We have concept of schema in mongoose not mongoDB
We use schema to define the shape of documents within a collection in mongoDB

Collection - Table
Documents -Rows

Each document is a container for key value pairs

Schema Types
1. String
2. Number
3. Date
4. Buffer - used for storing binary data
5. Boolean
6. ObjectID - assigning unique identifiers
7. Array

```js
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean,
});
```

## Model
Compile Schema into Model to get Class the create an object of the Class and this object maps to a document in mongoDb database.

## Saving a document

```js
const mongoose = require("mongoose");

mongoose
  .connect("mongodb://localhost/playground")
  .then(() => console.log("Connected to MongoDB..."))
  .catch((err) => console.error("Could not connect to MongoDB", err));

const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean,
});

const Course = mongoose.model("Course", courseSchema); // collection name and schema

async function createCourse() {
  const course = new Course({
    name: "Node.js Course",
    author: "DevilXfiero",
    tags: ["node", "backend"],
    isPublished: true,
  });

  const result = await course.save();
  console.log(result);
}

createCourse();
```

## Querying Documents

```js
async function getCourses() {
  const courses = await Course.find({
    author: "DevilXfiero",
    isPublished: true,
  })
    .limit(10)
    .sort({ name: 1 }) // 1 for asc and -1 for desc
    .select({ name: 1, tags: 1 }); // to get only name and tag property
  console.log(courses);
}

getCourses();
```

## Comparison Query Operators

1. eq (equal)
2. ne (not equal)
3. gt (greater than)
4. gte (greater than or equal to)
5. lt (less than)
6. lte (less than or equal to)
7. in 
8. nin (not in)

```js
 const courses = await Course
    .find({ price: { $gt: 10, $lte: 20 } }) // replace value by an object for comparision
    .find({ price: { $in: [10, 15, 20] } })
    .limit(10)
    .sort({ name: 1 }) // 1 for asc and -1 for desc
    .select({ name: 1, tags: 1 }); // to get only name and tag property
  console.log(courses);
```

## Logical Query Operators

OR and AND
```js
const courses = await Course.find()
    .or([{ author: "Mosh" }, { isPublished: true }])
    .and([])
    .limit(10)
    .sort({ name: 1 }) // 1 for asc and -1 for desc
    .count(); // to get number of documents
  console.log(courses);
```

## Regular Expression

```js
const courses = await Course
    // Starts with DevilX
    .find({ author: /^DevilX/ })

    // Ends with Fiero
    .find({ author: /Fiero$/i }) // i for case insensitive

    // Contains DevilX
    .find({ author: /.*DevilX.*/i })

    .limit(10)
    .sort({ name: 1 }) // 1 for asc and -1 for desc
    .select({ name: 1, tags: 1 });
```

## Pagination

```js
async function getCourses() {
  const pageNumber = 2;
  const pageSize = 10;
  const courses = await Course.find({
    author: "DevilXfiero",
    isPublished: true,
  })
    .skip((pageNumber - 1) * pageSize)
    .limit(pageSize)
    .sort({ name: 1 }) // 1 for asc and -1 for desc
    .select({ name: 1, tags: 1 }); // to get only name and tag property
  console.log(courses);
```


## Validation

Only meaningful at mongoose level not at db level.

```js
const courseSchema = new mongoose.Schema({
  name: { type: String, required: true },
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean,
});

await course.validate(); // to manually validate or it will check while saving
```

##  Built-in-Validators

```js
const courseSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    minlength: 5,
    maxlength: 255,
    //match: /pattern/
  },
  category: {
    type: String,
    required: true,
    enum: ["web", "mobile", "network"],
  },
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean,
  price: {
    type: Number,
    required: function () {
      return this.isPublished;
    }, // required if is published
    min: 10,
    max: 200,
  },
});
```
## Custom Validators

```js
tags: {
    type: Array,
    validate: {
      validator: function (v) {
        return v && v.length > 0;
      },
      message: "A course should have atlease one tag.",
    },
  }
```


isAsync: true
and make validator async function

```js
for (field in ex.errors) {
      console.log(ex.errors[field].message);
    }
```


## SchemaType Options

```js
category: {
    type: String,
    required: true,
    enum: ["web", "mobile", "network"],
    lowercase: true, // convert to lowercase
    // uppercase: true,
    trim: true,
 },
 price: {
    type: Number,
    required: function () {
      return this.isPublished;
    }, // required if is published
    min: 10,
    max: 200,
    get: (v) => Math.round(v),
    set: (v) => Math.round(v),
  }
```

