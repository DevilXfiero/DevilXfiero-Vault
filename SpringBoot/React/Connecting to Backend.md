
## Understand the Effect Hook

### Side Effect

- Store data in local storage.
- Call the server to fetch/save data.
- Manually modify the DOM.

 useEffect(() => {})
 To execute a piece of code **after** a component is rendered.
 call at top of the component not inside for loops.
```tsx
import { useRef, useEffect } from "react";

function App() {
  const ref = useRef<HTMLInputElement>(null);
  // afterRender
  useEffect(() => {
    // Side effect
    if (ref.current) ref.current.focus();
  });

  useEffect(() => {
    document.title = "My App";
  }); // multiple useEffect run in order after each render.
  return (
    <div>
      <input ref={ref} type="text" className="form-control" />
    </div>
  );
}
export default App;
```

## Effect Dependencies

If we do a change in render using use state it will render again and useEffect  will run again after render this will cause infinite loop so we need to tell to useEffect only when first time component render.

ProductList.tsx
```tsx
import React, { useEffect, useState } from "react";

const ProductList = ({ category }: { category: string }) => {
  const [products, setProducts] = useState<string[]>([]);

  useEffect(() => {
    console.log("Fetching products in ", category);
    setProducts(["Clothing", "Household"]);
  }, [category]); // second param array of dependencies if any value changes react will rerun effect but empty[] array means not dependent so it will run only once.

  return <div>ProductList</div>;
};

export default ProductList;
```

App.tsx
```tsx
import { useRef, useEffect, useState } from "react";
import ProductList from "./components/ProductList";

function App() {
  const [category, setCategory] = useState("");

  return (
    <div>
      <select
        className="form-select"
        onChange={(event) => setCategory(event.target.value)}
      >
        <option value=""></option>
        <option value="Clothing">Clothing</option>
        <option value="Household">Household</option>
      </select>
      <ProductList category={category} />
    </div>
  );
}
export default App;
```

## Effect Clean Up

```tsx
import { useEffect } from "react";

const connect = () => console.log("Connecting");
const disconnect = () => console.log("Disconnecting");
function App() {
  useEffect(() => {
    connect();
    return () => disconnect(); // function if we want do cleanup that will stop or do whatever effect is doing.
  });

  return <div></div>;
}
export default App;
```

## Fetching data 

 backend - jsonplaceholder.typicode.com 

Sending HTTP Requests
- fetch()
- axios (library)

npm i axios@1.3.4  

Calling to server will not happen immediately it will take some till so axios.get('url') function return **Promise**.

Promise - An object that holds the eventual result or failure of asynchronous operation.

```tsx
import axios from "axios";
import { useEffect, useState } from "react";

interface User {
  id: number;
  name: string;
}
function App() {
  const [users, setUsers] = useState<User[]>([]);

  useEffect(() => {
    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users")
      .then((response) => setUsers(response.data));
  }, []);

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
export default App;
```


## Understanding HTTP Requests

HTTP - Hypertext Transfer Protocol
Protocol for transferring data over the Internet.

## Handling Errors

```tsx
import axios from "axios";
import { useEffect, useState } from "react";

interface User {
  id: number;
  name: string;
}
function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");

  useEffect(() => {
    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/xusers")
      .then((response) => setUsers(response.data))
      .catch((err) => setError(err.message));
  }, []);

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
}
export default App;
```

## Working with Async and Await

```tsx
import axios, { AxiosError } from "axios";
import { useEffect, useState } from "react";

interface User {
  id: number;
  name: string;
}
function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const res = await axios.get<User[]>(
          "https://jsonplaceholder.typicode.com/users"
        );
        setUsers(res.data);
      } catch (err) {
        setError((err as AxiosError).message);
      }
    };
    fetchUsers();
  }, []);

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
}
default ;

```

## Cancelling  a Fetch Request

```tsx
useEffect(() => {
    const controller = new AbortController();
    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users", {
        signal: controller.signal,
      })
      .then((response) => setUsers(response.data))
      .catch((err) => {
        if (err instanceof CanceledError) return;
        setError(err.message);
      });

    return () => controller.abort();
  }, []);
```


