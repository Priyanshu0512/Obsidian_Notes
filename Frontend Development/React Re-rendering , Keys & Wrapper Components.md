
### Top Level Parent
While return components in React they need to be enclosed in a top level parent which can be any empty tag or a React Fragment.
```js
return (
    <React.Fragment>
      <Header title="connor1"> </Header>
      <Header title="connor2"> </Header>
    </React.Fragment>
  );
```

One of the most prominent reasons for it is `Reconciliation`. The single-root element rule in React facilitates the `reconciliation` process, where React efficiently updates the real DOM based on changes in the virtual DOM. By having a single root element, React can easily perform the comparison between the previous and current states of the `virtual DOM`.

> While a single root element is required, React provides a feature called fragments that allows you to group multiple elements without introducing an extra node in the real DOM. Fragments don't create an additional parent in the DOM but still satisfy the single-root rule.

```js
(`<></>` or `<React.Fragment></React.Fragment>`)
```

## Reconciliation

Reconciliation involves identifying what parts of the virtual DOM have changed and efficiently updating only those parts in the actual DOM. The single-root structure simplifies this process by providing a clear entry point for React to determine where updates should occur.


## Re-rendering in React

Re-rendering in React refers to the process of updating and rendering components to reflect changes in the application's state or props. When there's a change in the state or props of a component, React re-renders that component and any affected child components. It's important to note that a re-render doesn't necessarily mean a complete re-rendering of the entire DOM; instead, React efficiently updates only the necessary parts of the DOM.

> Basically, anytime a final DOM manipulation happens or when react actually updates the DOM it is called a re-render.

### When Does a Re-render Happen?

1. Changes in a state variable utilised within the component.
2. A re-render of a parent component, which subsequently triggers the re-rendering of all its child components. This cascading effect ensures synchronisation throughout the component tree.

There are two ways to minimise the re-renders
 1. Pushing state variables to the Lowest common Ancestor.
 2. By using memoization

### 1. Pushing the State Down 

- `Pushing the state down` in React refers to the practice of managing state at the lowest -possible level in the component tree.

- When state is kept at a higher level in the component tree, any changes to that state can trigger re-renders for all child components, even if they don't directly use or depend on that particular piece of state.

```js
function App() {
  function HeaderWithButton() {
    let [title, setTitle] = useState("Connor");
    function updateTitle() {
      setTitle(Math.random());
    }
    return (
      <>
        <button onClick={updateTitle}>
          Click on the button to change the title.
        </button>
        <Header title={title}></Header>
      </>
    );
  }
   function updateTitle() {
    setTitle(Math.random());
  }
  return (
    <React.Fragment>
      <HeaderWithButton /> 
      <Header title="raman"> </Header>
    </React.Fragment>
  );
}

function Header({ title }) {
  return <div> My name is {title}</div>;
}```


### 2. Memoization

- `memo` lets to skip re-rendering a component when its props are unchanged.

```js
function App() {
  const [title, setTitle] = useState("Connor");

  function updateTitle() {
    setTitle(Math.random());
  }
  return (
    <div>
      <button onClick={updateTitle}>
        Click on the button to change the title.
      </button>
      <Header title={title}> </Header>
      <Header title="raman"> </Header>
      <Header title="raman"> </Header>
      <Header title="raman"> </Header>
    </div>
  );
}

const Header = memo(function ({ title }) {
  return <div> My name is {title}</div>;
});```

> Remember to wrap all the components in the `<div>` as an empty tag would not be re-rendered an hence the parent element will be the root element hence on state change all its child will all re-render causing re-rendering of all the children whose state was not changed.

### Significance of Keys in React 

In React, when rendering a list of elements using the `map` function, it is crucial to assign a unique `key` prop to each element. The "key" is a special attribute that helps React identify which items have changed, been added, or been removed. This is essential for efficient updates and preventing unnecessary re-renders of the entire list.


## Wrapper Components

In React, wrapper components are used to encapsulate and group common styling or thematic elements that need to be applied consistently across different parts of an application.

```js
function App() {
  return <CardWrapper inner={<TextComponent />}></CardWrapper>;
}

function TextComponent() {
  return <div>hi there</div>;
}

function CardWrapper({ inner }) {
  return <div style={{ border: "2px solid black" }}>{inner}</div>;
}```

### Class Components VS Functional Components

In React, components are the building blocks of a user interface. There are two main types of components: class-based components and functional components.

- ##  Class-Based Components

    - Class-based components are ES6 classes that extend from `React.Component`.
    - They have access to the lifecycle methods provided by React, such as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.
    - State and lifecycle methods are managed within class-based components.
    - They were the primary type of components before the introduction of hooks in React 16.8.

- ### Functional Components

    - Functional components are simpler and more concise. They are essentially JavaScript functions that take props as an argument and return React elements.
    - With the introduction of React hooks in version 16.8, functional components gained the ability to manage state and use lifecycle methods through hooks like `useState` and `useEffect`.
    - They are generally easier to read and write.