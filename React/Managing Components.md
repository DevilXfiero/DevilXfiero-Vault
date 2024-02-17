## State Hook

React updates state asynchronously.
```tsx
function App() {
  const [isVisible, setVisibility] = useState(false);
  const handleClick = () => {
    setVisibility(true);
    console.log(isVisible); // false
    
  };
  return (
    <div>
      <button onClick={handleClick}>Show </button>
    </div>
  );
}

export default App;
```

State is stored outside of components.
Use hooks at the top level of your component.

## Choosing the State Structure

- Avoid redundant state variables.
- Group related variables inside an object.
- Avoid deeply nested structures.
```tsx
const [firstName, setFirstName] = useState("");
const [lastName, setLastName] = useState("");
const fullName = firstName + " " + lastName;

const [person, setPerson] = useState({
    firstName: "",
    lastName: "",
}); 
const [isLoading, setLoading] = useState(false);
```

## Pure Function

Given the same input, always returns the same result.
To keep components pure keep changes out of the render phase.

## Understanding the Strict Mode

Strict mode enabled renders each component twice first used for reporting or detecting issues.
In production strict mode checks are not included and component renders only once.

## Updating Objects

```tsx
const [drink, setDrink] = useState({
    title: "Americano",
    price: 5,
  });

  const handleClick = () => {
    // drink.price  = 6; don't give existing state object it will not update need new state object
    const newDrink = {
      ...drink,
      price: 6,
    };
    setDrink(newDrink);
  };

```


## Updating Nested Objects

```tsx
const [customer, setCustomer] = useState({
    name: "DevilX",
    address: {
      city: "Ghaziabad",
      zipCode: 20231,
    },
  });

  const handleClick = () => {
    setCustomer({
      ...customer,
      address: { ...customer.address, zipCode: 23213 },
    }); // spread opertor is shallow when we used creating new Customer object it will return existing address object in memory
    //  both refrence same address so we have to create new address object.
  };
```

## Updating Arrays
```tsx
const [tags, setTags] = useState(["happy", "cheerful"]);
const handleClick = () => {
  // Add
  setTags([...tags, "exciting"]);

  // Remove
  setTags(tags.filter((tag) => tag != "happy"));

  // Update
  setTags(tags.map((tag) => (tag === "happy" ? "happiness" : tag)));
  };
```

## Updating Array of Objects
```tsx
const [bugs, setBugs] = useState([
    { id: 1, title: "Bug1", fixed: false },
    { id: 2, title: "Bug 2", fixed: false },
  ]);
const handleClick = () => {
  setBugs(bugs.map((bug) => (bug.id === 1 ? { ...bug, fixed: true } : bug)));
};
```

## Simplifying Update Logic with Immer

npm i immer@9.0.19

```tsx
import { useState } from "react";
import produce from "immer";

function App() {
  const [bugs, setBugs] = useState([
    { id: 1, title: "Bug1", fixed: false },
    { id: 2, title: "Bug 2", fixed: false },
  ]);
  const handleClick = () => {
    // setBugs(bugs.map((bug) => (bug.id === 1 ? { ...bug, fixed: true } : bug)));
    setBugs(
      produce((draft) => {
        const bug = draft.find((bug) => bug.id === 1);
        if (bug) bug.fixed = true;
      })
    ); // draft is proxy object that records changes we're gonna apply.
  };

  return (
    <div>
      {bugs.map((bug) => (
        <p key={bug.id}>
          {bug.title} {bug.fixed ? "Fixed" : "New"}
        </p>
      ))}
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App;
```

## Sharing State between Components

To share the state we have to lift the state up to the closest component.

- Component that hold the state is the one responsible for updating it.

NavBar.tsx
```tsx
import React from "react";

interface Props {
  cartItemsCount: number;
}

const NavBar = ({ cartItemsCount }: Props) => {
  return <div>NavBar: {cartItemsCount}</div>;
};

export default NavBar;

```

Cart.tsx
```tsx
import React from "react";

interface Props {
  cartItems: string[];
  onClear: () => void;
}
const Cart = ({ cartItems, onClear }: Props) => {
  return (
    <>
      <div>
        <ul>
          {cartItems.map((item) => (
            <li key={item}>{item}</li>
          ))}
        </ul>
        <button onClick={onClear}> Clear</button>
      </div>
    </>
  );
};

export default Cart;
```

App.tsx
```tsx
import { useState } from "react";

import Cart from "./components/Cart";
import NavBar from "./components/NavBar";

function App() {
  const [cartItems, setCartItems] = useState(["Product1", "Product2"]);

  return (
    <div>
      <NavBar cartItemsCount={cartItems.length}></NavBar>
      <Cart cartItems={cartItems} onClear={() => setCartItems([])}></Cart>
    </div>
  );
}

export default App;
```

