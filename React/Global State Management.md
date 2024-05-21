- Reducers
- Context 
- Providers
- Zustand

Not covering redux.

## Consolidating State Logic with Reducer

### Reducers

A function that allows us to centralize state updates in a component.

counterReducer.ts
```ts
interface Action {
  type: "INCREMENT" | "RESET";
}
const counterReducer = (state: number, action: Action): number => {
  if (action.type === "INCREMENT") return state + 1;
  if (action.type === "RESET") return 0;
  return state;
};

export default counterReducer;
```


Counter.tsx
```tsx
import { useReducer } from "react";
import counterReducer from "./reducers/counterReducer";

const Counter = () => {
  //   const [value, setValue] = useState(0);
  const [value, dispatch] = useReducer(counterReducer, 0);
  return (
    <div>
      Counter ({value})
      <button
        onClick={() => dispatch({ type: "INCREMENT" })}
        className="btn btn-primary mx-1"
      >
        Increment
      </button>
      <button
        onClick={() => dispatch({ type: "RESET" })}
        className="btn btn-primary mx-1"
      >
        Reset
      </button>
    </div>
  );
};

export default Counter;
```


taskReducer.ts
```ts
interface Task {
  id: number;
  title: string;
}

interface AddTask {
  type: "ADD";
  task: Task;
}

interface DeleteTask {
  type: "DELETE";
  taskId: number;
}

type TaskAction = AddTask | DeleteTask;

const tasksReducer = (tasks: Task[], action: TaskAction): Task[] => {
  switch (action.type) {
    case "ADD":
      return [action.task, ...tasks];
    case "DELETE":
      return tasks.filter((t) => t.id !== action.taskId);
  }
};

export default tasksReducer;
```


## Sharing State using React Context

Sharing state - Lift the state up to the closes parent and pass it down as props to child components. 

Problem - we have to pass state through multiple components to reach child as our component tree grow bigger and complex. (Prop drilling)

### React Context

Allows sharing data without passing it down through many components in the middle.


1. Lift state up to the closest parent
 App.tsx
```tsx
import { useReducer } from "react";
import HomePage from "./state-management/HomePage";
import NavBar from "./state-management/NavBar";
import TaskContext from "./state-management/contexts/tasksContext";
import tasksReducer from "./state-management/reducers/taskReducer";

function App() {
  const [tasks, dispatch] = useReducer(tasksReducer, []);
  return (
    <TaskContext.Provider value={{ tasks, dispatch }}>
      <NavBar />
      <HomePage />
    </TaskContext.Provider>
  );
}
export default App;

```

 2. Create at context
tasksContext.ts
```ts
import { Dispatch } from "react";
import { Task, TaskAction } from "../reducers/taskReducer";
import React from "react";

interface TasksContextType {
  tasks: Task[];
  dispatch: Dispatch<TaskAction>;
}

const TaskContext = React.createContext<TasksContextType>(
  {} as TasksContextType
); // default value use null or pass an empty object using as keyword.

export default TaskContext;
```

3. Use shared state using context hook in component.
TaskList.tsx
```tsx
const { tasks, dispatch } = useContext(TaskContext);
```

AuthProvider.tsx
```tsx
import React, { ReactNode, useReducer } from "react";
import authReducer from "./reducers/authReducer";
import AuthContext from "./contexts/authContext";

interface Props {
  children: ReactNode;
}
const AuthProvider = ({ children }: Props) => {
  const [user, dispatch] = useReducer(authReducer, "");
  return (
    <AuthContext.Provider value={{ user, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
};

export default AuthProvider;
```

Anytime something in context changes all components using context re-render.

- A context should only hold values that are closely related and tend to change together.

Minimizing Renders 
Split up a context into smaller and focused ones, each having a single responsibility.

When to use context
State - Server State, Client (UI) State

Avoid using context for server state. Let react query manage the server state for you.
Client state -> Local state + React Context

State Management Libraries
1. Redux
2. MobX
3. Recoil
4. xState 
5. Zustand

Redux - A widely-used state management library for JS applications.

## Managing Application state with Zustand

npm i zustand@4.3.7 

store.ts
```ts
import { create } from "zustand";

interface CounterStore {
  counter: number;
  increment: () => void;
  reset: () => void;
}

const useCounterStore = create<CounterStore>((set) => ({
  counter: 0,
  increment: () => set((store) => ({ counter: store.counter + 1 })),
  reset: () => set(() => ({ counter: 0 })),
}));

export default useCounterStore;
```

Counter.tsx
```tsx
import { useReducer } from "react";
import counterReducer from "./reducers/counterReducer";
import useCounterStore from "./stores/store";

const Counter = () => {
  //   const [value, setValue] = useState(0);
  const { counter, increment, reset } = useCounterStore();
  return (
    <div>
      Counter ({counter})
      <button onClick={() => increment()} className="btn btn-primary mx-1">
        Increment
      </button>
      <button onClick={() => reset()} className="btn btn-primary mx-1">
        Reset
      </button>
    </div>
  );
};

export default Counter;
```

No need of context just do const {counter} = useCounterStore(); to use counter in any component.

## Preventing unnecessary Renders
```tsx
const counter = useCounterStore((s) => s.counter); // Navbar only dependent on counter property and only re render where counter changes.
```

Inspecting Stores with Zustand DevTools

npm i simple-zustand-devtools@1.1.0 
npm i -D @types/node 

```tsx
import { mountStoreDevtool } from "simple-zustand-devtools";

if (process.env.NODE_ENV === "development")
  mountStoreDevtool("Counter Store", useCounterStore);
```

