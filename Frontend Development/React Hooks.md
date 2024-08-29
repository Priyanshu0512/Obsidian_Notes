- Function which start with `use` are called Hooks.
- In React Hooks are the functions which allow you to hook into the `React State` and `lifecycle` features from function components.

### Side Effects - 

> In React the concept of side effects encompasses any operation that reach outside the functional scope of a react component. In order words any operation that it not related to rendering anything to the DOM. These operations can affect other components, interact with the browser or perform any asynchronous operation.

## Some Common Hooks 
## 1. useState

- This hook lets you describe the state of your app. Whenever the state updates, it triggers a re-render which finally results in state update.

```js
function App() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <button
        onClick={function () {
          setCount(count + 1);
        }}
      >
        Click me{count}
      </button>
    </div>
  );
}
```
 
## 2.useEffect

- The `useEffect` allows the user to perform `side-effects` in functional components.
- The `useEffect` performs the same function as `life-cycle` methods `componentWillUpdate`, `componentDidUpdate`,`componentDidMount` all under the same api

```js
  useEffect(() => {
    axios.get("http://localhost:3000/todo").then(function (response) {
      setTodos(response.data.allTodos);
    });
  }, []);
```

- `[]` empty array means the functions runs once after the component is mounted.

> The top level function in the `useEffect` hook cannot be a async function.

One way to use a async function is  as follows but this has a security flaw in it hence not recommended.

```js
async function  main(){
  const response = await axios.get("http://localhost:3000/todo");
  setTodos(response.data.allTodos);
}
useEffect(() => {
  main();
}, [todo]);

```

> The problem with the above function is that on a state change of the `todo` the api call will be made but it is an asynchronous function hence if the request is not resolved and another state change happens another api call will be made which might get resolved first then the earlier call.\


## 3.useMemo

- `useMemo` is a React Hook that is used to memoize the result of a computation, preventing unnecessary recalculations when the component re-renders. It takes a function (referred to as the "memoized function") and an array of dependencies. The memoized function will only be recomputed when the values in the dependencies array change.
- `useMemo` is particularly useful when dealing with expensive calculations or when you want to optimise performance by avoiding unnecessary computations during renders.

>The problem with the below code is that when a state change happens on the `counter` variable the entire root component is re-rendered which also includes the expensive operation of the for loop.

```js
function App() {
  const [counter, setCounter] = useState(0);
  const [input, setInput] = useState(1);

  let count = 0;
  for (let i = 1; i <= input; i++) {
    count += i;
  }
  return (
    <div>
      <input
        onChange={function (e) {
          setInput(e.target.value);
        }}
        placeholder="Enter a Number"
      ></input>
      <br />
      Sum from 1 to {input} is {count}
      <br />
      <button
        onClick={() => {
          setCounter(counter + 1);
        }}
      >
        Counter({counter})
      </button>
    </div>
  );
}```

A better version of the above code can be obtained by using the `useEffect` hook which tracks the input state and re-renders it only when its value changes.

```js
const [input, setInput] = useState(0);
const [finalValue, setFinal] = useState(0);

let count = 0;
useEffect(() => {
    for (let i = 1; i <= input; i++) {
      count += i;
    }
    setFinal(count);
}, [input]);
```

> Moreover this code also causes two re-renders as first re-render happens when the value is entered through the `setInput` then as the `input` changes it causes another re-render from the `useEffect` hook.

The cleaner way to approach this is to use a `useMemo` hook. Here the state will re-render only if the input changes.

```js
let count = useMemo(() => {
    let count = 0;
    for (let i = 1; i <= input; i++) {
      count += i;
    }
    return count;
}, [input]);
```



## 4. useCallback

- It is used to memoize functions which can help in optimising the performance of your applications especially in cases involving child components that reply on reference equality to prevent unnecessary renders.

```js
function App() {
  const [count, setCount] = useState(0);

function inputFunction() {
   console.log("child clicked");
}

  return (
    <div>
      <ButtonComponent inputFunction={inputFunction} />
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Click me {count}
      </button>
    </div>
  );
}

const ButtonComponent = memo(({ inputFunction }) => {
  console.log("child render");

  return (
    <div>
      <button>Button clicked</button>
    </div>
  );
});
```

> In the above code snippet the `ButtonComponent` is re-rendered even though it is wrapped in the `React.memo` as its content does not changes. This is due to the fact that every-time the button is clicked the `inputFunction` is re-initialised hence it is not equal `referencially` even though it contents remains same.

```js
const inputFunction = useCallback(() => {
    console.log("hi there");
}, []);
```

> The above problem of `reference equality` can be solved if we use the `useCallback` hook which ensures that the function reference changes only when something in the dependencies array change. This is the reason why `useCallback` hook is used to memoize functions that rely on  reference equality.

> Note - Anytime the value in the dependency array changes the function signature stored in the variable changes.(The function is not called.) It is only called when the event with which it is attached happens.

To call a function when something changes in the dependencies array use the `useEffect` hook.

```js
function main(){
// logic
}
useEffect(()=>{
   main();
},[input]);
```

## Custom Hooks

- Custom Hooks can be created all the state logic needs to directly go into the custom hook function but the function should start with the `use` word to signify it is a hook.

```js
function useTodo() {
  const [todo, setTodo] = useState([]);

  useEffect(() => {
    axios.get("Something").then((res) => {
      setTodos(res.data.todo);
    });
  }, []);
  return todo;
}

function App() {
  const todos = useTodo();

  return <div>{todos}</div>;
}
```



### Asynchronous Nature of `setState` function

```js
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button
        onClick={() => {
          setCount(count + 1);
          console.log(count);
          setCount(count + 1);
        }}
      >
        Click me
      </button>
      <p>Count is {count}</p>
    </div>
  );
}```


> In the above code the `setCount` function updates the count variable asynchronously hence the output on the console will be `1` and the value of count in both the `setCount` function will on the first click will be `0` hence 2 re-renders will happen but the value will update by only one on each click.


```js
function App() {
  const [c, setCount] = useState(0);

  return (
    <div>
      <button
        onClick={() => {
          setCount((c) => c + 1);
          setCount((c) => c + 1);
        }}
      >
        Click me
      </button>
      <p>Count is {c}</p>
    </div>
  );
}```



> To solve this we can make the operation in the `setCount` function synchronous hence after the first `setCount` is finished updating the value of count that will be passed onto the second `setCount` will be the updated value.


### Different use-case scenario for `useCallback` & `useMemo` 

### useCallback - 
 - The primary use case scenario for `useCallback` is to memoize the function signature and change it when values in the dependencies array changes.

### useMemo - 
- The primary use case scenario for `useMemo` is to memoize the return value for a given input and will execute the function only if the value in dependency array changes.


>Therefore `useCallback` is used to memoize function signature while `useMemo` runs a function when input value changes. Though same functionality can be achieved by both the hooks but they both differ in the use-case scenario.

