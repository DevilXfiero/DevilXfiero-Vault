- Caching
- Automatic retry
- Automatic refresh
- Paginated queries
- Infinite queries

What is React Query?
 A powerful library for managing data fetching and caching in React applications.

Redux - A popular state management library for JS applications.

| Redux | React Query |
| ---- | ---- |
| Difficult to learn | A lot simpler |
| So much boilerplate code | More lightweight |
Do not use Redux for caching.


 npm i @tanstack/react-query@4.28 

main.tsx
```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import "bootstrap/dist/css/bootstrap.css";
import "./index.css";
import { QueryClient ,QueryClientProvider } from "@tanstack/react-query";}


const queryClient = new QueryClient();
ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
    <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

## Fetching Data And Handling Errors

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

interface Todo {
  id: number;
  title: string;
  userId: number;
  completed: boolean;
}

const TodoList = () => {
  const fetchTodos = () =>
    axios
      .get<Todo[]>("https://xjsonplaceholder.typicode.com/todos")
      .then((res) => res.data);

  const { data: todos, error } = useQuery<Todo[], Error>({
    queryKey: ["todos"], // caching key
    queryFn: fetchTodos, // function to fetch data from backend
  }); // need to provide data and error type

  if (error) return <p>{error.message}</p>;

  return (
    <ul className="list-group">
      {todos?.map((todo) => (
        <li key={todo.id} className="list-group-item">
          {todo.title}
        </li>
      ))}
    </ul>
  );
};

export default TodoList;
```

Showing Loading Indicator
```ts
const {
    data: todos,
    error,
    isLoading,
} = useQuery<Todo[], Error>({
    queryKey: ["todos"], // caching key
    queryFn: fetchTodos, // function to fetch data from backend
});

if (isLoading) return <p>Loading...</p>;
```

## React query devtools

- npm i @tanstack/react-query-devtools@4.28  
```js
import { ReactQueryDevtools } from "@tanstack/react-query-devtools"; // in main.tsx add component
```

## Customizing react query settings

Auto refresh stale data on 3 conditions:
 - When a network is reconnected
 - When a component is mounted 
 - When the window is refocused


```tsx
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 3,
      cacheTime: 300_000, // 5 min if query has no obserever meaning no component is using query.
      staleTime: 10 * 1000, // how much time data consider fresh
      refetchOnWindowFocus: false, // default true
    },
  },
});

```


## Parametrized queries


usePost.ts
```ts
import { useQuery } from '@tanstack/react-query';
import axios from 'axios'
import React from 'react'


interface Post {
    id: number;
    title: string;
    body: string;
    userId: number;
}
  
const usePosts = (userId: number | undefined) => {
  const fetchPosts = () => axios
      .get<Post[]>('https://jsonplaceholder.typicode.com/posts', {
        params: {
            userId
        }
      })
      .then((res) => res.data)
  

  return useQuery<Post[], Error>({
    queryKey: userId ? ["users", userId, 'posts']: ['posts'],
    queryFn: fetchPosts,
    staleTime: 1*60*1000,
  });
}

export default usePosts
```

PostList.tsx
```tsx
import { useState } from "react";
import usePosts from "./hooks/usePosts";

const PostList = () => {
  const [userId, setUserId] = useState<number>();
  const { data: posts, error, isLoading } = usePosts(userId);

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>{error.message}</p>;

  return (
    <>
      <select
        onChange={(event) => setUserId(parseInt(event.target.value))}
        value={userId}
        className="form-select mb-3"
      >
        <option value=""></option>
        <option value="1">User 1</option>
        <option value="2">User 2</option>
        <option value="3">User 3</option>
      </select>
      <ul className="list-group">
        {posts?.map((post) => (
          <li key={post.id} className="list-group-item">
            {post.title}
          </li>
        ))}
      </ul>
    </>
  );
};

export default PostList;
```


## Paginated Queries

usePosts.ts
```ts
import { useQuery } from '@tanstack/react-query';
import axios from 'axios'


interface Post {
    id: number;
    title: string;
    body: string;
    userId: number;
}

interface PostQuery {
    page: number; 
    pageSize: number;
}
  
const usePosts = (query: PostQuery) => {
  const fetchPosts = () => axios
      .get<Post[]>('https://jsonplaceholder.typicode.com/posts', {
        params: {
            _start: (query.page - 1)*query.pageSize,
            _limit: query.pageSize
        }
      })
      .then((res) => res.data)
  

  return useQuery<Post[], Error>({
    queryKey: ['posts', query],
    queryFn: fetchPosts,
    staleTime: 1*60*1000,
    keepPreviousData: true, // fix loading and moving up for next page as previous data will be shown until new data being loaded.
  });
}

export default usePosts
```

PostList.tsx
```tsx
import { useState } from "react";
import usePosts from "./hooks/usePosts";

const PostList = () => {
  const pageSize = 10;
  const [page, setPage] = useState(1);
  const { data: posts, error, isLoading } = usePosts({ page, pageSize });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>{error.message}</p>;

  return (
    <>
      <ul className="list-group">
        {posts?.map((post) => (
          <li key={post.id} className="list-group-item">
            {post.title}
          </li>
        ))}
      </ul>
      <button
        disabled={page === 1}
        onClick={() => setPage(page - 1)}
        className="btn btn-primary my-3 "
      >
        Previous
      </button>
      <button
        onClick={() => setPage(page + 1)}
        className="btn btn-primary my-3 ms-1"
      >
        Next
      </button>
    </>
  );
};

export default PostList;
```


## Infinite Queries
usePosts.ts
```ts
import { useInfiniteQuery, useQuery } from '@tanstack/react-query';
import axios from 'axios'


interface Post {
    id: number;
    title: string;
    body: string;
    userId: number;
}

interface PostQuery {
    pageSize: number;
}
  
const usePosts = (query: PostQuery) => {
  const fetchPosts = ({pageParam = 1}) => axios
      .get<Post[]>('https://jsonplaceholder.typicode.com/posts', {
        params: {
            _start: (pageParam - 1)*query.pageSize,
            _limit: query.pageSize
        }
      })
      .then((res) => res.data)
  

  return useInfiniteQuery<Post[], Error>({
    queryKey: ['posts', query],
    queryFn: fetchPosts,
    staleTime: 1*60*1000,
    keepPreviousData: true, // fix loading and moving up for next page as previous data will be shown until new data being loaded.
    getNextPageParam: (lastPage, allPages) => {
      return lastPage.length > 0 ? allPages.length + 1 : undefined;
    }
  });
}

export default usePosts
```


PostList.tsx
```tsx
import { useState } from "react";
import usePosts from "./hooks/usePosts";
import React from "react";

const PostList = () => {
  const pageSize = 10;
  const {
    data: posts,
    error,
    isLoading,
    fetchNextPage,
    isFetchingNextPage,
  } = usePosts({ pageSize });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>{error.message}</p>;

  return (
    <>
      <ul className="list-group">
        {posts.pages.map((page, index) => (
          <React.Fragment key={index}>
            {page.map((post) => (
              <li key={post.id}>{post.title}</li>
            ))}
          </React.Fragment>
        ))}
      </ul>
      <button
        className="btn btn-primary my-3 ms-1"
        disabled={isFetchingNextPage}
        onClick={() => fetchNextPage()}
      >
        {isFetchingNextPage ? "Loading..." : "Load More"}
      </button>
    </>
  );
};

export default PostList;
```


## Mutating Data with Handling Errors and isLoading

TodoForm.tsx
```tsx
import { useRef } from "react";
import { Todo } from "./hooks/useTodos";
import { useMutation, useQueryClient } from "@tanstack/react-query";
import axios from "axios";

const TodoForm = () => {
  const queryClient = useQueryClient();
  const addTodo = useMutation<Todo, Error, Todo>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),
    onSuccess: (savedTodo, newTodo) => {
      // APPROACH: Invalidating the cache
      // queryClient.invalidateQueries({
      //     queryKey: ['todos']
      // }) // doesn't work with json placeholder
      // APPROACH 2: Updating the data in cache directly
      queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
        savedTodo,
        ...(todos || []),
      ]);
      if (ref.current) ref.current.value = "";
    },
  });
  const ref = useRef<HTMLInputElement>(null);

  return (
    <>
      {addTodo.error && (
        <div className="alert alert-danger">{addTodo.error.message}</div>
      )}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button disabled={addTodo.isLoading} className="btn btn-primary">
            {addTodo.isLoading ? "Adding..." : "Add"}
          </button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;
```

## Optimistic Updates
```tsx
import { useRef } from "react";
import { Todo } from "./hooks/useTodos";
import { useMutation, useQueryClient } from "@tanstack/react-query";
import axios from "axios";

interface AddTodoContext {
  previousTodos: Todo[];
}
const TodoForm = () => {
  const queryClient = useQueryClient();
  const addTodo = useMutation<Todo, Error, Todo, AddTodoContext>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),

    onMutate: (newTodo: Todo) => {
      const previousTodos = queryClient.getQueryData<Todo[]>(["todos"]) || [];
      queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
        newTodo,
        ...(todos || []),
      ]);
      if (ref.current) ref.current.value = "";
      return { previousTodos };
    },
    onSuccess: (savedTodo, newTodo) => {
      queryClient.setQueryData<Todo[]>(["todos"], (todos) =>
        todos?.map((todo) => (todo === newTodo ? savedTodo : todo))
      );
    },
    onError: (error, newTodo, context) => {
      if (!context) return;
      queryClient.setQueryData<Todo[]>(["todos"], context.previousTodos);
    },
  });
  const ref = useRef<HTMLInputElement>(null);

  return (
    <>
      {addTodo.error && (
        <div className="alert alert-danger">{addTodo.error.message}</div>
      )}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button disabled={addTodo.isLoading} className="btn btn-primary">
            {addTodo.isLoading ? "Adding..." : "Add"}
          </button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;
```



APIClient.ts
```ts
import axios from "axios";

const axiosInstance = axios.create({
    baseURL: 'https://jsonplaceholder.typicode.com'
});


class APIClient<T>{
    endpoint: string;

    constructor(endpoint: string) {
        this.endpoint = endpoint;
    }

    getAll = () => {
        return axiosInstance
        .get<T[]>(this.endpoint)
        .then((res) => res.data);
    }

    post = (data: T) => {
        return axiosInstance
        .post<T>(this.endpoint, data)
        .then((res) => res.data);
    }
}

export default APIClient;
```


todoService.ts
```ts
import APIClient from "./apiClient";

export interface Todo {
    id: number;
    title: string;
    userId: number;
    completed: boolean;
}

export default new APIClient<Todo>('/todos');
```
## Understanding then Application Layers

Components - use hooks to fetch and update data e.g TodoForm, TodoList
Custom Hooks - use HTTP Services to fetch and update data e.g useTodos all logic for managing data in cache
HTTP Services - instances of APIClient dedicated to working with specific objects e.g todoService
APIClient - handles sending http request to backend

Time to ms library
npm i ms@2.1.3 
npm i -D @types/ms

