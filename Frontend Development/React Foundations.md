- `React` - It determines the difference between the newState and the previousState.
- `React DOM` - This is responsible for change the State on the DOM.

`.jsx` - It is a javascript file inside which both javascript and XML can be written.
## Understanding DOMs

### 1. Virtual DOM

- React uses an virtual DOM to optimise and improve performance. It is an in-memory, lightweight representation of the actual DOM.
- When changes are made to the `State` of a `React Component`, React creates a new virtual DOM tree which it compares with the previous virtual DOM tree to determine the changes made.
### 2. Real DOM

- Real DOM is the actual structure of the HTML document. When React determines the updates that need to be made from the virtual DOM , it updates the Real DOM with only the necessary changes.
Note- Updation to the real DOM is an expensive process hence React tries to minimise it's interaction with the Real DOM as much as possible.

## Some React Jargon

### 1. State
- State is an Object that represents the current state of the app.
- It only represents the dynamic things of the app.
### 2. Component
- Components in React the building blocks that are rendered on to the DOM.
- Each piece of Component has its own use and can be used again and again.
### 3. Re-rendering 
- In React, when the state changes, React automatically re-renders the component to reflect that change. This way, your users always see the most up-to-date and accurate information on the screen.

Example of how react somewhat works under the hood to re-render components.
```html
<body>
  <div id="parent"></div>
  <script >
    let state={
      count:0
    }
    function onButtonPress(){
      state.count++;
      reRender(); // Re-render function call on State change.
    }
    function reRender(){
      document.getElementById('parent').innerHTML="";
      const component = createComponent(state.count); // Creating a component.
      document.getElementById('parent').appendChild(component);
    }

    function createComponent(count){
      const button=document.createElement('button');
      button.innerHTML= `Counter ${count}`;
      button.setAttribute("onclick","onButtonPress()");
      return button;
    }

    reRender(); // Intial Render of the component.
  </script>
</body>
```


**Using React**

```js
import { useState } from "react";
import "./App.css";
import PropTypes from "prop-types";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <CustomButton count={count} setCount={setCount}></CustomButton>
    </div>
  );
}

CustomButton.propTypes = { // Called Prop  Validation covered in Eslint.
  count: PropTypes.number.isRequired,
  setCount: PropTypes.func.isRequired,
};

function CustomButton(props) {
  function onClickHandler() {
    props.setCount(props.count + 1);
  }
  return <button onClick={onClickHandler}>Counter {props.count}</button>;
}

export default App;
```

**Important Points** 
- `count` is a constant hence should be updated directly but through the setCount function provided by the `useState` hook.
- Any Javascript should be enclosed inside the `{}` brackets.
- Flow of Code 
     - `Change of State` - Firstly the app function gets called. When their is a state change command goes into the `CustomButton` and state variable are passed into  the component `CustomButton`.
     - `Component change/updation` - The component is updated according to the handler function here `onClickHandler` which increases the count and return the `button` elementR
     - `Rendering of Component` - The returned component is rendered onto the Real DOM.


## React Props

- In React, props (short for properties) are a way to pass data from a parent component to a child component. They allow you to customise and configure child components based on values provided by their parent components.

![[Pasted image 20240820182132.png]]

Here is the breakdown of the React Props - 
### 1. Passing Data: 
- Props enable the flow of data from a parent component to a child component.
- They are passed as attributes in JSX when rendering a child component.
### 2.Functional Components:
- In functional components, props are received as an argument to the function.

```js
function MyComponent(props) {
  // Access props here
}
```
### 3.Class Components:
- In class components, props are accessed using `this.props`.

```js
class MyComponent extends React.Component {   
    render() {    
    // Access props using this.props 
} }
```

### 4.Immutable and Read-Only
- Props in React are read-only. A child component cannot modify the props it receives from a parent. Props are intended to be immutable.

### 5. Customisation and Reusability
- Props allow you to customise the behaviour and appearance of a component, making it versatile and reusable in different contexts.

### 6. Default Values:
- You can provide default values for props to ensure that the component works even if certain props are not explicitly passed.

### 7. De-structuring Props:
- You can use de-structuring to extract specific props from the `**props**` object, making code cleaner.
```js
function MyComponent({ prop1, prop2 }) {   
   // Access prop1 and prop2 directly 
}
```

### 8.Passing Functions as Props:
- You can pass functions as props, allowing child components to communicate with their parent components.


