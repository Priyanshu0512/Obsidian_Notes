
- **Recoil** is a state management library developed by Facebook specifically for React applications.
- It introduces the concept of atoms and selectors, providing a more flexible and scalable approach to managing and sharing state.

## Problem with Context API

- Context API in React is a powerful tool for solving the prop drilling problem by allowing the passing of data through the component tree without the need for explicit props at every level. However, it does not inherently address the re-rendering issue.
 
- When using the Context API, updates to the context can trigger re-renders of all components that consume that context, even if the specific data they need hasn't changed. This can potentially lead to unnecessary re-renders and impact the performance of the application.
 
> To mitigate this, developers can use techniques such as memoization (with useMemo or React.memo) to prevent unnecessary re-renders of components that don't depend on the changes in context. Additionally, libraries like Redux, Recoil, or Zustand provide more fine-grained control over state updates and re-renders compared to the built-in Context API.


## Recoil API & Hooks

### Recoil Root 
- The `RecoilRoot` is a component provided by Recoil that serves as the root of the Recoil state tree. It must be placed at the top level of your React component tree to enable the use of Recoil atoms and selectors throughout your application.
### Recoil Atom
- In Recoil, an atom is a unit of state. It represents a piece of state that can be read from and written to by various components in your React application. Atoms act as shared pieces of state that can be used across different parts of your component tree.
## Recoil Hooks

In Recoil, the hooks `useRecoilState`, `useRecoilValue`, and `useSetRecoilState` are provided to interact with atoms and selectors.

1. `useRecoilState`- 
     - This hook returns a tuple containing the current value of the Recoil state and a function to set its new value.

```js
const [count, setCount] = useRecoilState(countState);
```

2. `useRecoilValue`- 
    - This hook retrieves and subscribes to the current value of a Recoil state.

```js
const count = useRecoilValue(countState);
```

3. `useSetRecoilState`- 
    - This hook returns a function that allows you to set the value of a Recoil state without subscribing to updates.

```js
const setCount = useSetRecoilState(countState);
```

These hooks provide a convenient way to work with Recoil states in functional components. `useRecoilState` is used when you need both the current value and a setter function, `useRecoilValue` when you only need the current value, and `useSetRecoilState` when you want to set the state without subscribing to updates. They contribute to making Recoil-based state management more ergonomic and straightforward.


## Recoil  Selectors 

- In Recoil, selectors are functions that derive new pieces of state from existing ones. They allow you to compute derived state based on the values of atoms or other selectors. Selectors are an essential part of managing complex state logic in a Recoil application.


```js
export const evenSelector = selector({
  key: "evenSelector",
  get: ({ get }) => {
    const count = get(countAtom);
    return count % 2;
  },
});

function Even() {
  const isEven = useRecoilValue(evenSelector);
  console.log(isEven);
  return <div>{!isEven ? "It is even" : null}</div>;
  }
```