npm i react-router-dom@6.10.0

routes.tsx
```tsx
import { createBrowserRouter } from "react-router-dom";
import HomePage from "./HomePage";
import UserListPage from "./UserListPage";

const router = createBrowserRouter([
  { path: "/", element: <HomePage /> },
  { path: "/users", element: <UserListPage /> },
]);

export default router;
```

main.tsx
```tsx
<RouterProvider router={router} />
```

```tsx
<a href="/users">Users</a> // full page reload
<Link to="/users"> Users</Link> // only change data of the new page.
```

Navigate between pages
```tsx
const navigate = useNavigate();
navigate("/"); // on event completion
```

## Passing params to path
```tsx
const router = createBrowserRouter([
  { path: "/users/:id", element: <UserDetailPage /> },
]);

// to link
<Link to={`/users/${user.id}`}>{user.name}</Link>
```

## Getting params from path
```tsx
// we can use these hooks
const params = useParams();
const [searchParams, setSearchParams] = useSearchParams();
console.log(searchParams.toString());
console.log(searchParams.get("name"));
const location = useLocation();
```

## Nested routes


routes.tsx
```tsx
import { createBrowserRouter } from "react-router-dom";
import HomePage from "./HomePage";
import UserListPage from "./UserListPage";
import ContactPage from "./ContactPage";
import UserDetailPage from "./UserDetailPage";
import Layout from "./Layout";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    children: [
      { index: true, element: <HomePage /> },
      { path: "users", element: <UserListPage /> },
      { path: "users/:id", element: <UserDetailPage /> },
    ],
  },
]);

export default router;
```


Layout.tsx
```tsx
import { Outlet } from "react-router-dom";
import NavBar from "./NavBar";

const Layout = () => {
  return (
    <>
      <NavBar />
      <div id="main">
        <Outlet /> // is a placeholder for a child component
      </div>
    </>
  );
};

export default Layout;
```

## Handling errors

ErrorPage.tsx
```tsx
import { isRouteErrorResponse, useRouteError } from "react-router-dom";

const ErrorPage = () => {
  const error = useRouteError(); // to catch error thrown
  console.log(error);
  return (
    <>
      <h1>Oops...</h1>
      <p>{isRouteErrorResponse(error) ? "Invalid page" : "Unexpected error"}</p>
    </>
  );
};

export default ErrorPage;
```

route.tsx
```tsx
import { createBrowserRouter } from "react-router-dom";
import HomePage from "./HomePage";
import UserListPage from "./UserListPage";
import ContactPage from "./ContactPage";
import UserDetailPage from "./UserDetailPage";
import Layout from "./Layout";
import ErrorPage from "./ErrorPage";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    errorElement: <ErrorPage />,
    children: [
      { index: true, element: <HomePage /> },
      { path: "users", element: <UserListPage /> },
      { path: "users/:id", element: <UserDetailPage /> },
    ],
  },
]);

export default router;
```

## Private routes

routes access to only authenticated users.
## Layout routes

PrivatRoutes.tsx
```tsx
import React from "react";
import { Navigate, Outlet } from "react-router-dom";
import useAuth from "./hooks/useAuth";

const PrivateRoutes = () => {
  const { user } = useAuth();

  if (!user) return <Navigate to="/login" />;
  return <Outlet />;
};

export default PrivateRoutes;
```

routes.tsx
```tsx
import { createBrowserRouter } from "react-router-dom";
import HomePage from "./HomePage";
import UserListPage from "./UserListPage";
import ContactPage from "./ContactPage";
import UserDetailPage from "./UserDetailPage";
import Layout from "./Layout";
import ErrorPage from "./ErrorPage";
import PrivateRoutes from "./PrivateRoutes";
import LoginPage from "./LoginPage";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    errorElement: <ErrorPage />,
    children: [
      { index: true, element: <HomePage /> },
      { path: "login", element: <LoginPage /> },
    ],
  },
  {
    element: <PrivateRoutes />,
    children: [{ path: "users", element: <UserListPage /> }],
  },
]);

export default router;
```