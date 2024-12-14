
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

- Combining multiple atoms into a single atom and then using a selector on it.
```js
export const notificationsAtom = atom({
  key: "allNotifications",
  default: {
    network: 50,
    jobs: 0,
    messages: 100,
    noti: 10,
  },
});

export const totalNotificationSelector = selector({
  key: "totalNotificationSelector",
  get: ({ get }) => {
    const notifications = get(notificationsAtom);
    return (
      notifications.network +
      notifications.jobs +
      notifications.messages +
      notifications.noti
    );
  },
});```
## Asynchronous Data Queries 

-  The default function in the atom must be synchronous. In order to fetch data from the backend and avoid initialisation of the default parameters to 0 selectors can be used for Asynchronous Data Queries.

```js
const UserInfoState = atom({
  key: 'UserInfo',
  default: selector({
    key: 'UserInfo/Default',
    get: ({get}) => myFetchUserInfo(get(currentUserIDState)),
  }),
});

```


## Atom Family

- The `default` parameters return an atom with the matching id.
```js
export const todoAtomFamily = atomFamily({
  key: 'TodoAtomFamily',
  default: id =>{
    return Todo.find(x => x.id ===id) // Finding todo with required id.
  }
});


const currentTodo = useRecoilValue(todoAtomFamily(id)); 
// Instead of the calling the atom we can the atom family with the required id.

```


## selectorFamily

```js
export const todoAtomFamily = atomFamily({
  key: "todoAtomFamily",
  default: selectorFamily({
    key: "todoSelectorFamily",
    default:
      (id) =>
      async ({ get }) => { // {get} is required when accessing other atoms here                              not required.
        const res = await axios.get("//url");
        return res.data.todo;
      },
  }),
});```

> Note - Here default takes in the id and returns an async function which in turn returns the todo.

> If multiple calls are made to the same id the the request is cached hence hence multiple backend calls are not send.


## useRecoilStateLoadable 

- This recoil State is used to when asynchronous a re made to the backend which might take up time hence to prevent the page from freezing `useRecoilStateLoadable` hook is used which gives a `loading` value if the data is being fetched from the backend and if the fetch is complete it returns `hasValue` which can be checked to load the data when available.

```js
const [ todo, setTodo]= useRecoilStateLoadable(todoAtomFamily(id));

if(todo.state === 'loading'){
    return <div>Loading...</div>
}
else if( todo.state ==='hasValue'){
    return <div>
      {todo.contents.title}
      {todo.contents.description}
    </div>
}
```

> Apart form `loading` & `hasValue`   it also has the `hasError` state to catch errors.