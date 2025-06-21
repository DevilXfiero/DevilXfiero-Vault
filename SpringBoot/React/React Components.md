Two ways 

JS Class or function

Function based are popular - PascalCasing

Message.tsx
```tsx
function Message() {
  // JSX: JavaScript XML
  const name = "DevilX";
  if (name) return <h1>Hello {name}</h1>; // {} inside braces we can write any js expression
  return <h1>Hello World</h1>;
}

export default Message;
```

App.tsx
```tsx
import Message from "./Message";

function App() {
  return (
    <div>
      <Message />
     </div>
  );
}

export default App;
```

hmr - hot module replacement used to by vite to reload updated changes.


# [[Building Components]]

# [[Styling Components]]

# [[Managing Components]]


