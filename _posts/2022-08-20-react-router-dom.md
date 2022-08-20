---
layout: single
title:  "[React] React-Router-DOM V5 & V6 (day20)" 
subtitle: "difference between v5 & 6"
createDate: "2022-08-20"
categories: React
tags: react
header:
  teaser: "/assets/images/React.jpeg"
---



![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/ad401ad2-d404-4284-9f51-c1ba0239207a/image.jpeg)

## So What Is React Router ?

> React Router is a fully-featured client and server-side routing library for React, a JavaScript library for building user interfaces. React Router runs anywhere React runs; on the web, on the server with node.js, and on React Native.

here are some of the changes you can make to upgrade an existing project from React Router v5 to v6.

### `Switch` Replaced With `Routes`

In v6, `Switch` in not exported from `react-router-dom`. In the earlier version we could use `Switch` to wrap our routes. Now we use `Routes` to do the same thing instead of `Switch`.

### Changes In The Way We Define Our `Route`

The component that should be rendered on matching a route can not be written as children of the `Route` component, but it takes a prop called `element` where we have to pass a JSX component for that to be rendered.

### The `exact` Prop Is Not Needed Anymore

With version 6, React Router has just become alot more awesome. The now better, path matching algorithm, enables us to match a particular route match without the `exact` prop. Earlier, without `exact`, any URL starting with the concerned keyword would be loaded, as the matching process was done from top to down the route definitions. But now, we do not have to worry about that, as React Router has a better algorithm for loading the best route for a particular URL, the order of defining does not really matters now.

#### In v5

```jsx
import { Switch, Route } from "react-router-dom";
.
.
.
<Switch>
    <Route path="/">
        <Home/>
    </Route>
    <Route exact path="/cryptocurrencies">
        <Cryptocurrencies/>
    </Route>
    <Route exact path="/crypto/:coinId">
        <CryptoDetails/>
    </Route>
    <Route exact path="/exchanges">
        <Exchanges />
    </Route>
</Switch>
```

#### In v6

```jsx
import { Routes, Route } from "react-router-dom";
.
.
.
<Routes>
   <Route path="/" element={<Home />} />
   <Route path="/crypto/:coinId" element={<CryptoDetails />} />
   <Route path="/cryptocurrencies" element={<Cryptocurrencies />} />

   <Route path="/exchanges" element={<Exchanges />} />
</Routes>
```

### No Need To Install `react-router-config` Seperately

`react-router-config` allowed us to define our routes as javascript objects, instead of React elements, and all it's functionalities have to moved in the core react router v6.

```jsx
//V5
import { renderRoutes } from "react-router-config";

const routes = [
  {
    path: "/",
    exact: true,
    component: Home
  },
  {
    path: "/cryptocurrencies",
    exact: true,
    component: Cryptocurrencies
  },
  {
    path: "/exchanges",
    exact: true,
    component: Exchanges
  }
];

export default function App() {
   return (
     <div>
       <Router>{renderRoutes(routes)}</Router>
     </div>
   );
}




//V6
function App() {
  let element = useRoutes([
    // These are the same as the props you provide to <Route>
    { path: "/", element: <Home /> },
    { path: "/cryptocurrencies", element: <Cryptocurrencies />,
      // Nested routes use a children property
      children: [
        { path: ":coinId", element: <CryptoDetails /> },
      ] 
    },
    {
      path: "/exchanges",
      element: <Exchanges />
    },
  ]);

  // The returned element will render the entire element
  // hierarchy with all the appropriate context it needs
  return element;
}
```



### `useHistory` Is Now `useNavigate`

React Router v6 now has the navigate api, which most of the times would mean replacing `useHistory` to `useNavigate`.

```jsx
//V5
import { useHistory } from "react-router-dom";

function News() {
  let history = useHistory();
  function handleClick() {
    history.push("/home");
  }
  return (
    <div>
      <button onClick={()=>{
           history.push("/home");
      }}>Home</button>
    </div>
  );
}


//V6
import { useNavigate } from "react-router-dom";

function News() {
  let navigate = useNavigate();

  return (
    <div>
      <button onClick={()=>{
          navigate("/home");
      }}>go home</button>
    </div>
  );
}
```

Some more common features of `useHistory` were `go`, `goBack` and `goForward`. These can also be achieved by navigate api too, we just need to mention the number of steps we want to move forward or backward ('+' for forward and '-' for backward). So we can code these features we can consider this.

```jsx
//V5
import { useHistory } from "react-router-dom";

function Exchanges() {
  const { go, goBack, goForward } = useHistory();

  return (
    <>
      <button onClick={() => go(-2)}>
        2 steps back
      </button>
      <button onClick={goBack}>1 step back</button>
      <button onClick={goForward}>1 step forward</button>
      <button onClick={() => go(2)}>
        2 steps forward
      </button>
    </>
  );
}


//V6
import { useNavigate } from "react-router-dom";

function Exchanges() {
  const navigate = useNavigate();

  return (
    <>
      <button onClick={() => navigate(-2)}>
        2 steps back
      </button>
      <button onClick={() => navigate(-1)}>1 step back</button>
      <button onClick={() => navigate(1)}>
        1 step forward
      </button>
      <button onClick={() => navigate(2)}>
        2 steps forward
      </button>
    </>
  );
}
```

### `activeStyle` and `activeClassName` Props Removed From `<NavLink />`

In the previous version we could set a seperate class or a style object for the time when the `<NavLink/>` would be active. In V6, these two props are removed, instead in case of Nav Links className and style props, work a bit differently. They take a function which in turn gives up some information about the link, for us to better control the styles.

```jsx
//V5
<NavLink
  to="/news"
  style={{ color: 'black' }}
  activeStyle={{ color: 'blue' }}>
  Exchanges
</NavLink>

<NavLink
  to="/news"
  className="nav-link"
  activeClassName="active">
  Exchanges
</NavLink>

//V6
<NavLink
  to="/news"
  style={({isActive}) => { color: isActive ? 'blue' : 'black' }}>
  Exchanges
</NavLink>

<NavLink
  to="/news"
  className={({ isActive }) => "nav-link" + (isActive ? "active" : "")}>
  Exchanges
</NavLink>
```

### Replace `Redirect` with `Navigate`

`Redirect` is no longer exported from `react-router-dom`, instead we use can `Navigate` to achieve the same features.

```jsx
//V5
import { Redirect } from "react-router-dom";

<Route exact path="/latest-news">
    <Redirect to="/news">
</Route>
<Route exact path="/news">
    <News />
</Route>


//V6
import { Navigate } from "react-router-dom";

<Route path="/latest-news" element={<Navigate replace to="/news">} />
<Route path="/news" element={<Home />} />
```



Source from Arunava Modak blog 



https://dev.to/arunavamodak/react-router-v5-vs-v6-dp0