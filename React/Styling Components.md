
## Vanilla CSS

Add css file with same name with as .tsx file and import css
Move both in one folder 
add css

if you want import to not show as /abc/abc where abc is tsx name
you need to add index.tsx and export component from there
so import will change to /abc which is equivalent to /abc/index.tsx
and pick component from there.

if in another stylesheet we have css class with same name it will result in clashes.


## CSS Modules

Is a css file in which all className are scoped locally.

1. Rename abc.css to abc.module.css
2. Import styles from "./ListGroup.module.css";
```tsx
<ul className={[styles.listGroup, styles.container].join(" ")}>
```

- to import multiple classes we use join on arr
- don't use hype list-group instead use camelCasing for classes otherwise we need to define like styles['list-group']

## CSS-In-JS

CSS and JS in same file.

Libraries
- Styled components
- Emotion
- Polished

npm i styled-components

```tsx
import { useState } from "react";
import styles from "./ListGroup.module.css";
import styled from "styled-components";

const List = styled.ul`
  list-style: none;
  padding: 0;
`;

interface ListItemProps {
  active: boolean;
}
const ListItem = styled.li<ListItemProps>`
  padding: 5px 0;
  background: ${(props) => (props.active ? "blue" : "none")};
`;

interface Props {
  items: string[];
  heading: string;
  onSelectItem: (item: string) => void;
}

function ListGroup(
  { items, heading, onSelectItem }: Props 
) {

  const [selectedIndex, setSelectedIndex] = useState(-1);

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No item found</p>}
      <List>
        {items.map((item, index) => (
          <ListItem
            active={index === selectedIndex}
            key={item}
            onClick={() => {
              setSelectedIndex(index);
              onSelectItem(item);
            }}
          >
            {item}
          </ListItem>
        ))}
      </List>
    </>
  );
}

export default ListGroup;
```


## Separation of Concerns

Divide a program into distinct sections where each section handles a specific functionality, rather having everything in one place.

## Inline Styles

```tsx
<ul className="list-group" style={{ backgroundColor: "orange" }}>
```

## Popular UI Libraries

- Bootstrap
- Material UI
- Tailwind CSS
- Daisy UI
- Chakra UI

## Adding Icons

npm i react-icons@4.7.1  

```tsx
import { BsFillCalendarFill } from "react-icons/bs";

function App() {
  return (
    <div>
      <BsFillCalendarFill color="blue" size="40" />
    </div>
  );
}

export default App;
```
