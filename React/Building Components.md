Bootstrap - modern css library for styling css of applications.

Install bootstrap
1. npm i bootstrap@5.2.3 in terminal.
2. import "bootstrap/dist/css/bootstrap.css" in main.tsx 


## Creating a ListGroup Component

```tsx
function ListGroup() {
  return (
    <ul className="list-group">
      <li className="list-group-item">An item</li>
      <li className="list-group-item">A second item</li>
      <li className="list-group-item">A third item</li>
      <li className="list-group-item">A fourth item</li>
      <li className="list-group-item">And a fifth one</li>
    </ul>
  );
}

export default ListGroup;
  
```

## Fragments

Multiple tags we can put them all in div but we're adding extra element better use fragment.
```tsx
function ListGroup() {
  return (
    <> // fragment short way so that we don't need to import
    <h1>ListGroup</h1>
    <ul className="list-group">
      <li className="list-group-item">An item</li>
      <li className="list-group-item">A second item</li>
      <li className="list-group-item">A third item</li>
      <li className="list-group-item">A fourth item</li>
      <li className="list-group-item">And a fifth one</li>
    </ul>
    </>
  );
}

export default ListGroup;
```

## Rendering Lists
```tsx
function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo"];
  return (
    <>
      <h1>List</h1>
      <ul className="list-group">
        {items.map((item) => (
          <li key={item}>{item}</li> //  item should have unique key preferred id so if we add or remove items dynamically react knows what part of the page should be updated
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```


## Conditional Rendering

In JS
true && 1 -> 1
true && 'DevilX' -> 'DevilX'
false && 'DevilX' -> false 

```tsx
function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo"];

  return (
    <>
      <h1>List</h1>
      {items.length === 0 ? <p> No item found </p> : null} // can put message inside const or function with paramters for clean code.
      {items.length === 0 && <p>No item found</p>} // better technique developers use
      <ul className="list-group">
        {items.map((item) => (
          <li key={item}>{item}</li> 
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```


## Handling Events

```tsx
{items.map((item, index) => (
          <li
            className="list-group-item"
            key={item}
            onClick={() => console.log(item, index)}
          >
            {item}
          </li>
        ))}

```

```tsx
import { MouseEvent } from "react";

function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo"];
  // Event Handler
  const handleClick = (event: MouseEvent) => console.log(event)

  return (
    <>
      <h1>List</h1>
      {items.length === 0 && <p>No item found</p>}
      <ul className="list-group">
        {items.map((item, index) => (
          <li
            className="list-group-item"
            key={item}
            onClick={handleClick}
          >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```


## Managing State

Each component has its own state
```tsx
import { useState } from "react";

function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo"];

  // let selectedIndex = 0; // no item selected
  // Event Handler

  // need to useState Hook because react doesn't knows about state change of    variable
  const [selectedIndex, setSelectedIndex] = useState(-1);

  return (
    <>
      <h1>List</h1>
      {items.length === 0 && <p>No item found</p>}
      <ul className="list-group">
        {items.map((item, index) => (
          <li
            className={
              selectedIndex === index
                ? "list-group-item active"
                : "list-group-item"
            }
            key={item}
            onClick={() => {
              setSelectedIndex(index);
            }}
          >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```


## Passing data via Props

ListGroup.tsx
```tsx
import { useState } from "react";

interface Props {
  items: string[];
  heading: string;
}

function ListGroup({ items, heading }: Props /* can also do by props: Props*/) {
  // need to useState Hook because react doesn't knows about state change of variable
  const [selectedIndex, setSelectedIndex] = useState(-1);

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No item found</p>}
      <ul className="list-group">
        {items.map((item, index) => (
          <li
            className={
              selectedIndex === index
                ? "list-group-item active"
                : "list-group-item"
            }
            key={item}
            onClick={() => {
              setSelectedIndex(index);
            }}
          >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```

App.tsx
```tsx
import ListGroup from "./components/ListGroup";

function App() {
  const items = ["New York", "San Francisco", "Tokyo"];

  return (
    <div>
      <ListGroup items={items} heading="Cities" />
    </div>
  );
}

export default App;
```

## Passing functions via Props

ListGroup.tsx

```tsx
import { useState } from "react";

interface Props {
  items: string[];
  heading: string;
  onSelectItem: (item: string) => void;
}

function ListGroup(
  { items, heading, onSelectItem }: Props /* can also do by props: Props*/
) {
  // need to useState Hook because react doesn't knows about state change of variable
  const [selectedIndex, setSelectedIndex] = useState(-1);

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No item found</p>}
      <ul className="list-group">
        {items.map((item, index) => (
          <li
            className={
              selectedIndex === index
                ? "list-group-item active"
                : "list-group-item"
            }
            key={item}
            onClick={() => {
              setSelectedIndex(index);
              onSelectItem(item);
            }}
          >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```

App.tsx

```tsx
import ListGroup from "./components/ListGroup";

function App() {
  let items = ["New York", "San Francisco", "Tokyo"];
  const handleSelectItem = (item: string) => {
    console.log(item);
  };
  return (
    <div>
      <ListGroup
        items={items}
        heading="Cities"
        onSelectItem={handleSelectItem}
      />
    </div>
  );
}

export default App;
```

State Vs Props

| Props | State |
| ---- | ---- |
| Input passed to a component | Data managed by a components |
| Similar to function args | Similar to local variables |
| Immutable  | Mutable  |
| Cause a re-render | Cause a re-render |

## Passing children
Alert.tsx
```tsx
import { ReactNode } from "react";

interface Props {
  children: ReactNode;
}

const Alert = ({ children }: Props) => {
  return <div className="alert alert-primary">{children}</div>;
};

export default Alert;

```

App.tsx
```tsx
import Alert from "./components/Alert";

function App() {
  return (
    <div>
      <Alert>Hello World</Alert> // we can paas any html code by adding children
      component in Props with ReactNode Type
    </div>
  );
}

export default App;
```

## Button Exercise

Button.tsx
```tsx
interface Props {
  children: string;
  color?: "primary" | "secondary"; // to make optional and set default and make use of or to only set property with provided values
  onClick: () => void;
}

const Button = ({ children, onClick, color = "primary" }: Props) => {
  return (
    <button className={"btn btn-" + color} onClick={onClick}>
      {children}
    </button>
  );
};

export default Button;

```

App.tsx
```tsx
import Button from "./components/Button";

function App() {
  const clicked = () => {
    console.log("Clicked");
  };
  return (
    <div>
      <Button color="secondary" onClick={clicked}>
        My Button
      </Button>
    </div>
  );
}

export default App;
```