Asynchronous does not mean concurrent or multithreaded.

```js
console.log("Before");
setTimeout(() => {
  console.log("Reading a user from a database...");
}, 2000); // asynchronous or non blocking function
console.log("After");
```

## Async Patterns

Patterns to deal with result for asynchronous functions
1. Callbacks
2. Promises
3. Async/await - syntactical sugar over promises

## Callbacks

```js
console.log("Before");
getUser(1, (user) => {
  getRepositories(user.username, (repos) => {
    console.log("Repos", repos);
  });
});
console.log("After");

// callback is a function we're going to call when result of async function is ready
function getUser(id, callback) {
  setTimeout(() => {
    console.log("Reading a user from a database...");
    callback({ id: id, gitHubUsername: "DevilXfiero" });
  }, 2000);
}

function getRepositories(username, callback) {
  setTimeout(() => {
    console.log("Calling the github API...");
    callback(["repo1", "repo2", "repo3"]);
  }, 2000);
}
```

## Callback Hell

we have too much nested structure for relations like user->repo->commits called Callback Hell.

## Named Functions to Rescue

```js
console.log("Before");
getUser(1, getRepositories);
console.log("After");

function getRepositories(user) {
  getRepositories(user.username, getCommits);
}
function getCommits(repos) {
  getCommits(repo, displayCommits);
}
function displayCommits(commits) {
  console.log(commits);
}

// callback is a function we're going to call when result of async function is ready
function getUser(id, callback) {
  setTimeout(() => {
    console.log("Reading a user from a database...");
    callback({ id: id, gitHubUsername: "DevilXfiero" });
  }, 2000);
}

function getRepositories(username, callback) {
  setTimeout(() => {
    console.log("Calling the github API...");
    callback(["repo1", "repo2", "repo3"]);
  }, 2000);
}
```

## Promise

Object that holds the eventual result of an async operation.

Create Promise object - Pending state
Result ready - Fulfilled state
Error - Rejected state

```js
const p = new Promise((resolve, reject) => {
  // Kick off some async work
  // ...
  setTimeout(() => {
    resolve(1); // pending => resolved, fullfilled
    reject(new Error("message")); // pending => rejected
  }, 2000);
  // send result to consumer of this object
});

p.then((res) => console.log("Result", res)).catch((err) =>
  console.log("Error", err.message)
);
```


```js
console.log("Before");

getUser(1)
  .then((user) => getRepositories(user.gitHubUsername))
  .then((repos) => getCommits(repos[0]))
  .then((commits) => console.log(commits))
  .catch((err) => console.log("Error", err.message));

console.log("After");

function getUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Reading a user from a database...");
      resolve({ id: id, gitHubUsername: "DevilXfiero" });
    }, 2000);
  });
}

function getRepositories(username) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Calling GitHub API...");
      resolve(["repo1", "repo2", "repo3"]);
    }, 2000);
  });
}

function getCommits(repo) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Calling GitHub API...");
      resolve(["commit"]);
    }, 2000);
  });
}
```

## Creating settled Promises
```js
const p = Promise.resolve({ id: 1 });
p.then((result) => console.log(result));
```

## Running Promises in Parallel

```js
const p1 = new Promise((resolved) => {
  setTimeout(() => {
    console.log("Async operation 1...");
    resolved(1);
  }, 2000);
});

const p2 = new Promise((resolved) => {
  setTimeout(() => {
    console.log("Async operation 2...");
    resolved(2);
  }, 2000);
});

Promise.all([p1, p2])
  .then((res) => console.log(res))
  .catch((err) => console.log("Error", err.message)); // if any of the promise got rejected final promise considered rejected

Promise.race([p1, p2])
  .then((res) => console.log(res))
  .catch((err) => console.log("Error", err.message)); // something as soon as one promise completed
```

## Async / Await

helps you write async code like sync code
```js
async function displayCommits() {
  try {
    const user = await getUser(1);
    const repos = await getRepositories(user.gitHubUsername);
    const commits = await getCommits(repos[0]);
    console.log(commits);
  } catch (err) {
    console.log("Error", err.message);
  }
}
displayCommits();

function getUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Reading a user from a database...");
      resolve({ id: id, gitHubUsername: "DevilXfiero" });
    }, 2000);
  });
}

function getRepositories(username) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Calling GitHub API...");
      //   reject(new Error("Could not get the repos"));
      resolve(["repo1", "repo2", "repo3"]);
    }, 2000);
  });
}

function getCommits(repo) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log("Calling GitHub API...");
      resolve(["commit"]);
    }, 2000);
  });
}
```

