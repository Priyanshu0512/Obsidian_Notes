
## Some Jargons

### 1. SPA (Single Page Application)

A Single Page Application (SPA) is a type of web application or website that interacts with the user by dynamically rewriting the current page, rather than loading entire new pages from the server.

>**Key Characteristics:**
- Loads a single HTML page initially.
- Subsequent interactions and navigation are handled by dynamically updating the content on the page through JavaScript.
- Utilises AJAX or Fetch API to communicate with the server and fetch data without reloading the entire page.
- Provides a more fluid and seamless user experience by avoiding full-page reloads.

### 2. Client-side Bundle

In the context of web development, a client-side bundle refers to a collection of JavaScript files and other assets bundled together to be delivered to the client's web browser.

 >**Key Components:**
- **JavaScript Files:** The application's logic and functionality are written in JavaScript files. Bundling involves combining these files into a single or multiple bundles.
- **Stylesheets, Images, and Other Assets:** Along with JavaScript, other assets like stylesheets, images, and fonts may be included in the bundle for efficient delivery to the client.

 >**Advantages:**
- Reduces the number of HTTP requests, improving loading times.
- Enables code splitting and lazy loading for optimising performance.
- Simplifies deployment and maintenance by organising code into manageable bundles.


### 3. Client-side Routing

Client-side routing refers to the process of managing navigation within a Single Page Application (SPA) entirely on the client side, without making additional requests to the server for each new view.

 >**Key Features:**
- Utilises the browser's History API to manipulate the URL without triggering full page reloads.
- Enables dynamic content updates based on the route, improving user experience.
- Typically implemented using libraries like React Router for React applications or Vue Router for Vue.js applications
## Routing

- In Pre-react days when a user used to change pages on an application a request would be sent to the server which in response sent the requested HTML files and other dependencies.
- After the introduction of the `React` it enabled developers to create `single Page application`. What happens is that all the required files and dependencies are sent to the client when the first request is sent to the server. 
- A Client side routing of pages happens on client which is responsible for dynamic applications.

## React Router DOM

In React, routing is commonly achieved using the React Router DOM library, which provides a set of components for handling navigation within a React application. The main components involved in React Router DOM are `BrowserRouter`, `Routes`, and `Route`. Here's an overview of how routing is typically implemented using these components:

#### 1. BrowserRouter
- The `BrowserRouter` component is a top-level component that should be used to wrap your entire application. It enables the use of routing features throughout your React application.
- It utilises the HTML5 History API to manipulate the URL without triggering full page reloads.

#### 2. Routes
- The `Routes` component is used to define the routes for your application. Inside the `Routes` component, you specify individual `Route` components for each route in your application.
- The `Routes` component can contain multiple `Route` components, each representing a different view or page.

#### 3. Route
- The `Route` component is responsible for rendering specific components based on the current URL path. It takes two main props: `path` and `element`.
- The `path` prop defines the URL path that should match for the route to be rendered, and the `element` prop specifies the component to render when the path matches.

```js
function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/" element={<Landing />} />
      </Routes>
    </BrowserRouter>
  );
}```

> It you want to navigate programatically between pages then `windows.location.href` can to used to change the pages within the application.

```js
<button
        onClick={() => {
          window.location.href = "/";
        }}
>
```

### Issue with `window.location.href`

When using `window.location.href` for navigation in a React application, it triggers a full page reload, which is not desirable in client-side routing. A full page reload involves fetching the HTML, CSS, and other assets again, leading to a slower and less efficient user experience.

> **Solution**

To address this issue, React Router DOM provides a solution in the form of the `useNavigate` hook. This hook is designed for programmatic navigation within a React component without triggering a full page reload. By using `useNavigate`, you can ensure smoother transitions between different views in a single-page application (SPA) without unnecessary overhead.

> **Note** - The `useNavigate` hook in React Router DOM is designed to work within the context of a `BrowserRouter`. It should be used inside a component that is a descendant of `BrowserRouter` to ensure access to the correct router context. This limitation is intentional, as `useNavigate` relies on the router context for scoped navigation, enabling seamless client-side routing without triggering a full page reload. Placing the hook within the correct context ensures its proper functionality for dynamic view and URL updates.


```js
function App() {
  return (
    <div>
      <BrowserRouter>
        <Appbar />
        <Routes>
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/" element={<Landing />} />
        </Routes>
      </BrowserRouter>
    </div>
  );
}

 function Appbar() {
  const navigate = useNavigate();
  return (
    <div>
      <button
        onClick={() => {
          navigate("/");
        }}
      >
        Landing Page
      </button>
      <button
        onClick={() => {
          navigate("/dashboard");
        }}
      >
        Dashboard Page
      </button>
    </div>
  );
```

## Lazy Loading

Lazy loading in React is a technique used to optimise the performance of a web application by deferring the loading of certain components until they are actually needed. This can significantly reduce the initial bundle size and improve the overall loading time of the application.
 
In React, lazy loading is typically achieved using the React.lazy function along with the Suspense component. The `React.lazy` function allows you to load a component lazily, meaning it is only fetched when the component is actually rendered. Here's a simple example:
\
```js

const Dashboard = React.lazy(() => import("./Components/Dashboard"));
function App() {
  return (
    <div>
      <BrowserRouter>
        <AppBar />
        <Routes>
          <Route
            path="/dashboard"
            element={
              <Suspense fallback={"loading..."}>
                <Dashboard />
              </Suspense>
            }
          />
          <Route
            path="/"
            element={
              <Suspense fallback={"loading..."}>
                <Landing />
              </Suspense>
            }
          />
        </Routes>
      </BrowserRouter>
    </div>
  );
}

```


## Prop Drilling 

Passing Props is a great way to explicitly pipe data through your UI tree to the components that use it.

But passing props can become verbose and inconvenient when you need to pass some prop deeply through the tree, or if many components need the same prop. The nearest common ancestor could be far removed from the components that need data, and [lifting state up](https://react.dev/learn/sharing-state-between-components) that high can lead to a situation called “prop drilling”.

**Lifting States**![[Pasted image 20240828001510.png]]


**Prop-Drilling**![[Pasted image 20240828001535.png]] 
>**Why Prop Drilling?**

1. **State Management:** Prop drilling is often used to manage state in a React application. By passing state down through the component tree, you can share data between components without resorting to more advanced state management solutions like context or state management libraries.

2. **Simplicity:** Prop drilling keeps the application structure simple and makes it easier to understand the flow of data. It's a straightforward way of handling data without introducing more complex tools.

## Drawbacks

1. Readability- Prop drilling can make the code less readable, especially when you have many levels of components. It might be hard to trace where a particular prop is coming from.
2. Maintenance- If the structure of the component tree changes, and the prop needs to be passed through additional components, it requires modifications in multiple places.

```js
import react, { useState } from "react";

const CountContext = createContext(0);
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Count count={count} setCount={setCount} />
    </div>
  );
}

function Count({ count, setCount }) {
  return (
    <div>
      {count}
      <Buttons count={count} setCount={setCount} />
    </div>
  );
}

function Buttons({ count, setCount }) {
  return (
    <div>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Increase
      </button>
      <button
        onClick={() => {
          setCount(count - 1);
        }}
      >
        Decrease
      </button>
    </div>
  );
}

```

> In the above example though the `setCount` prop is not being used by the `Count` component it has to be drilled down as the `Button` component requires it.

## Context API

- Context API is a feature in React that provides a way to share values like props between components without explicitly passing them through each level of the component tree. It helps solve the prop drilling problem by allowing data to be accessed by components at any level without the need to pass it through intermediate component

1. `createContext`- The `createContext` function is used to create a context. It returns an object with two components - `Provider` and `Consumer`.

```js
const MyContext = React.createContext();
```
2. `Provider`- The `Provider` component is responsible for providing the context value to its descendants. It is placed at the top of the component tree.

```js
<MyContext.Provider value={/* some value */}>   {
    /* Components that can access the context value */} 
</MyContext.Provider>
```

3. `Consumer` **(or** `**useContext**` **hook):** The `Consumer` component allows components to consume the context value. Alternatively, the `useContext` hook can be used for a more concise syntax.

```js

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <CountContext.Provider value={{ count, setCount }}>
        <Count></Count>
      </CountContext.Provider>
    </div>
  );
}

function Count() {
  return (
    <div>
      <CountRenderer />
      <Buttons />
    </div>
  );
}

function CountRenderer() {
  const { count, setCount } = useContext(CountContext);
  return <div>{count}</div>;
}

function Buttons() {
  const { count, setCount } = useContext(CountContext);
  return (
    <div>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Increase
      </button>
      <button
        onClick={() => {
          setCount(count - 1);
        }}
      >
        Decrease
      </button>
    </div>
  );```

> Problem - The `Count` also re-renders if through it is not using the state variable.  