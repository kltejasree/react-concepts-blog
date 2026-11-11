

## 1. What are the advantages of using JSX?

- It allows us to write HTML elements inside JavaScript.
- It allows React to show more useful error and warning messages.
- Faster than normal JavaScript as it performs optimizations while translating to regular JavaScript.

## 2. Difference between Virtual DOM and Real DOM

**Real DOM:**

Real DOM is the actual DOM maintained by the browser.

**Virtual DOM:**

Virtual DOM is the lightweight environment used by React to identify the changes in the code.

**Example:**

If any state or reference value is changed in the code, React identifies the changes in the code and updates only that part in the Real DOM.

## 3. What is a bundler?

A bundler is a tool which combines all our files and dependencies into an optimized version to favour the browser.

**Example:**

You have different files in your React project like Navbar, Footer, Main, index.css, App.jsx. All these files are combined by the bundler.

### Webpack

Webpack is a tool that takes our application dependencies and bundles them into static files optimized for web browsers.

## 4. How does Vite.js work?

Vite helps you run and build our React applications.

Vite provides a development server and helps create an optimized production build.

## 5. What is Babel?

Babel is a tool which converts modern JavaScript and JSX into JavaScript so that the browser can easily understand it.

## 6. What is a React Element?

A React element is an object that describes what should appear on the screen.

It is created using JSX or `React.createElement()`.

Example:

```jsx
const element = <h1>Hello React!</h1>;
```

This creates a React element describing an `h1` element.

## 7. List all the situations in which React re-renders the component

- When its state changes.
- When its props change.
- When its parent component re-renders, its child component also re-renders.

**Note:** A child doesn't need its own state or props changes to re-render. Its parent rendering again is enough in the normal case.

Additional situations:

- When a context value changes, components consuming that context re-render.
- When an external store subscription detects a changed snapshot, the subscribed component re-renders.

## 8. Difference between class and functional components

**Class components:**

Class components use JavaScript classes and lifecycle methods. They also use the `render()` method.

**Functional components:**

Functional components use JavaScript functions and React Hooks. They directly return JSX.

## 9. When do we need functional and class components?

### Functional components

We use them when developing new React applications because they support Hooks such as `useState`, `useEffect`, and `useRef` to manage state, side effects, and other React features.

### Class components

We mainly use them when working with older React applications and when implementing Error Boundaries, as React's traditional Error Boundary implementation requires class components.

## 10. Why should React component names start with uppercase?

To distinguish between HTML elements and custom components.

**Example:**

```jsx
function Welcome() {
  return <h1>Hello!</h1>;
}

function App() {
  return <Welcome />;
}
```

Here, `Welcome` is a custom component.

When you specify:

```jsx
function welcome() {
  return <h1>Hello!</h1>;
}

function App() {
  return <welcome />;
}
```

React treats `<welcome />` as a regular HTML tag rather than a custom component.

## 11. What is ReactDOM?

ReactDOM is a library which connects React components with the browser DOM (Real DOM).

It provides methods like `createRoot()` and `render()` to display React applications in the browser.

**React:** Is used to build UI components.

**ReactDOM:** Is responsible for rendering those components into the browser.

## 12. Difference between state and props

### Props

- Input passed to the component.
- Similar to function arguments.
- Immutable (read-only for the receiving component).

### State

- Data managed by a component.
- Similar to local variables.
- Mutable through state setter functions.

## 13. Difference between JSX and HTML

### JSX

- Allows us to write HTML-like elements inside JavaScript.
- We can use conditional rendering.
- We can use JavaScript expressions and methods like `map()` to display lists.

### HTML

- Uses HTML elements and attributes to structure webpages.
- Does not directly support JavaScript expressions or React conditional rendering.

## 14. Why do we use PropTypes?

PropTypes are used to validate the data types of props passed from a parent component to a child component.

In simple words, PropTypes help us check whether a component receives the correct type of data.

```jsx
function User(props) {
  return (
    <h1>
      {props.name} - {props.age}
    </h1>
  );
}

function App() {
  return <User name="Teja" age={22} />;
}
```

Here, name should be a string and age should be a number.

React can't automatically validate the prop types, so for that we use PropTypes by installing the package.

**Installation:**

```bash
npm install prop-types
```

**Code:**

```jsx
import PropTypes from 'prop-types';

function User(props) {
  return (
    <h1>
      {props.name} - {props.age}
    </h1>
  );
}

User.propTypes = {
  name: PropTypes.string,
  age: PropTypes.number
};
```

### Common PropTypes

| PropType | Expected data |
|---|---|
| `PropTypes.string` | String |
| `PropTypes.number` | Number |
| `PropTypes.bool` | Boolean |
| `PropTypes.array` | Array |
| `PropTypes.object` | Object |
| `PropTypes.func` | Function |
| `PropTypes.node` | Anything that can be rendered |
| `PropTypes.element` | React element |

We can use `.isRequired` to make a prop mandatory.

Example:

```jsx
User.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number
};
```

## 15. Different ways to update state using setState

### Method 1: Direct value update

When you know the new value, you can pass it directly.

**Example:**

```jsx
const [count, setCount] = useState(0);

setCount(10);
```

### Method 2: Using previous state

When the new state depends on the previous state, use a callback function.

```jsx
const [count, setCount] = useState(0);

setCount((prevCount) => prevCount + 1);
```

### Method 3: Updating an object

```jsx
const [user, setUser] = useState({
  name: "Teja",
  age: 22
});

setUser({
  ...user,
  age: 23
});
```

### Method 4: Updating an array

```jsx
const [items, setItems] = useState([1, 2, 3]);

setItems([...items, 4]);
```

**In class components:**

We use `this.setState()`.

Direct update:

```jsx
this.setState({
  count: 10
});
```

Using previous state:

```jsx
this.setState((prevState) => ({
  count: prevState.count + 1
}));
```

Unlike the `useState` setter, class component `this.setState()` shallowly merges the object you provide with the existing state.

## 16. Explain the statement: useState is asynchronous in nature

Yes, useState is asynchronous because it doesn't update the value as soon as you update it.

**Example:**

```jsx
const [items, setItems] = useState([1, 2, 3]);

setItems([...items, 4]);
```

Here, you are pushing 4 into items, but when you log the items immediately after calling `setItems`, you can see the previous array only. It updates with the new value on the next render.

**Additional example:**

```jsx
const [count, setCount] = useState(0);

function increase() {
  setCount(count + 1);

  console.log(count);
}
```

The console displays the old value because the current render's state value does not change immediately.

## 17. Why should we not update the state directly?

We should not update the state directly because React may not recognize the changes and trigger the required re-render.

React relies on state updates to know when it should render the component again.

**Incorrect example:**

```jsx
const [user, setUser] = useState({
  name: "Teja",
  age: 22
});

user.age = 23;
```

Here, we directly modify the existing state object.

**Correct example:**

```jsx
setUser({
  ...user,
  age: 23
});
```

Here, we create a new object and update the state using the setter function.

## 18. Can you handle form validation in React?

Yes, we can handle form validation in React using different approaches. For simple forms, we can use controlled components with useState and implement validation inside the onSubmit handler. We can also use HTML5 validation attributes such as required, pattern, and minLength. For complex forms, we can use libraries like Formik or React Hook Form to manage form values, validation errors, and submission efficiently.

## 19. What is Virtual DOM and how does it work?

Virtual DOM is a lightweight version of Real DOM used by React to identify the changes.

**Example:**

You change the value using useState.

So instead of directly rendering the Real DOM, React calculates the updated UI, compares it with the previous render, and updates the necessary parts in the Real DOM.

## 20. Difference between controlled and uncontrolled components

### Controlled components

Element data can be controlled by the React component through state and callbacks like `onChange`.

Example:

```jsx
function App() {
  const [name, setName] = useState('');

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

Here, React state controls the input value.

### Uncontrolled components

Element data can be controlled by the DOM itself.

Example:

```jsx
function App() {
  const inputRef = useRef(null);

  function handleSubmit() {
    console.log(inputRef.current.value);
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

Here, the DOM maintains the input value, and we access it using `useRef`.

## 21. Why do we need to pass the key prop when displaying a list?

As a list contains so many values, each must have a unique key to identify it. In order to give a reference for React, we need to pass the key prop.

Example:

```jsx
const users = [
  { id: 1, name: "Teja" },
  { id: 2, name: "Ram" }
];

function UserList() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

Keys help React identify which items have been added, removed, or changed.

## 22. Lifecycle methods

### Mounting

When the component renders for the very first time.

### Updating

When the component re-renders because of changes in its state or props.

### Unmounting

When the component is removed from the page.

### Class component lifecycle methods

| Lifecycle method | Purpose |
|---|---|
| `constructor()` | Initializes state and binds methods. |
| `render()` | Returns the JSX to display. |
| `componentDidMount()` | Runs after the component is mounted. Useful for API calls and subscriptions. |
| `componentDidUpdate()` | Runs after an update. Useful when an action depends on changed props or state. |
| `componentWillUnmount()` | Runs before the component is removed. Useful for clearing timers and subscriptions. |
| `static getDerivedStateFromProps()` | Updates state based on changes in props in specific cases. |
| `getSnapshotBeforeUpdate()` | Captures information from the DOM before it is updated. |
| `componentDidCatch()` | Handles errors in child components. |

### Functional component equivalent

Functional components use Hooks such as `useEffect()` to handle side effects and cleanup.

Example:

```jsx
useEffect(() => {
  console.log("Component mounted");

  return () => {
    console.log("Component unmounted");
  };
}, []);
```

## 23. Reasons to use Context in React and how it works

Context is used to share data between components without passing props manually through every level.

This problem is called **prop drilling**.

### When do we use Context?

- Sharing user authentication information.
- Sharing theme information (light mode and dark mode).
- Sharing language preferences.
- Sharing common application settings.

### How does it work?

There are three main steps:

1. Create a context using `createContext()`.
2. Provide the value using a Context Provider.
3. Access the value using `useContext()`.

Example:

```jsx
import { createContext, useContext } from 'react';

const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

function Child() {
  const theme = useContext(ThemeContext);

  return <h1>{theme}</h1>;
}
```

Here, the Child component can access the theme value without receiving it through props.

## 24. Use case of React.Fragment

React.Fragment is used to group multiple elements without adding an extra DOM element.

Example:

```jsx
function App() {
  return (
    <React.Fragment>
      <h1>Hello</h1>
      <p>Welcome to React</p>
    </React.Fragment>
  );
}
```

We can also use the short syntax:

```jsx
function App() {
  return (
    <>
      <h1>Hello</h1>
      <p>Welcome to React</p>
    </>
  );
}
```

**Use case:** When we need to return multiple elements from a component without adding an unnecessary `<div>` to the DOM.

## 25. Is it possible to loop inside JSX? Give an example.

Yes, we can loop over data inside JSX using the map function. JSX doesn't directly support writing regular `for` or `while` loops inside its expressions, so we can use `map()`.

**Example:**

```jsx
import React from 'react';

const lights = [1, 2, 3, 4, 5, 6, 7, 8, 9];

const Lights = () => {
  return (
    <div className="">
      {lights.map((each) => (
        <p key={each}>{each}</p>
      ))}
    </div>
  );
};

export default Lights;
```

## 26. Advantages of using Hooks

- Hooks allow functional components to use state and other React features.
- `useState` is used to store and update state values.
- `useEffect` is used for side effects, such as fetching data from outside or performing an action when dependencies change.
- `useRef` is used to store values without triggering a re-render when the ref value changes.
- Hooks allow us to reuse stateful logic using custom Hooks.
- Hooks help us organize related logic inside functional components.

## 27. Write code explaining different types of Hooks

### useState()

```jsx
import { useState } from 'react';

const Example = () => {
  const [count, setCount] = useState(0);

  function increase() {
    setCount((prev) => prev + 1);
  }

  return (
    <>
      <h1>{count}</h1>
      <button onClick={increase}>Increase</button>
    </>
  );
};

export default Example;
```

### useEffect()

```jsx
import { useEffect, useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count changed");
  }, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

### useRef()

```jsx
import { useRef } from 'react';

function Example() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </>
  );
}
```

### useContext()

```jsx
import { createContext, useContext } from 'react';

const UserContext = createContext();

function App() {
  return (
    <UserContext.Provider value="Teja">
      <Child />
    </UserContext.Provider>
  );
}

function Child() {
  const user = useContext(UserContext);

  return <h1>Hello {user}</h1>;
}
```

### useReducer()

```jsx
import { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };

    case 'decrement':
      return { count: state.count - 1 };

    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <h1>{state.count}</h1>

      <button onClick={() => dispatch({ type: 'increment' })}>
        Increase
      </button>

      <button onClick={() => dispatch({ type: 'decrement' })}>
        Decrease
      </button>
    </>
  );
}
```

## 28. How to use useEffect?

`useEffect` is a React Hook used to perform side effects in functional components.

Side effects include:

- Fetching data from an API.
- Setting timers.
- Adding event listeners.
- Updating the document title.
- Subscribing to external services.

### Three ways to use useEffect

**1. Without dependency array**

```jsx
useEffect(() => {
  console.log("Runs after every render");
});
```

It runs after every committed render.

**2. With an empty dependency array**

```jsx
useEffect(() => {
  console.log("Runs when component mounts");
}, []);
```

It runs after the component is initially mounted. In development StrictMode, React may run an additional setup and cleanup cycle.

**3. With dependencies**

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

It runs after the initial mount and when `count` changes.

### Cleanup function

We use a cleanup function to clear timers, remove event listeners, and unsubscribe from external services.

Example:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Timer running");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

## 29. How to use useRef?

`useRef` is a React Hook used to store a value that doesn't cause a re-render when it changes.

It is commonly used for:

- Accessing DOM elements.
- Focusing input fields.
- Storing timer IDs.
- Keeping mutable values between renders.

Example:

```jsx
import { useRef } from 'react';

function App() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleClick}>Focus</button>
    </>
  );
}
```

Here, `inputRef.current` gives us access to the actual input DOM element.

## 30. Explain useContext Hook

`useContext` is a React Hook used to access values from Context without passing props manually through multiple components.

Example:

```jsx
import { createContext, useContext } from 'react';

const MyContext = createContext();

function App() {
  return (
    <MyContext.Provider value="Hello React">
      <Child />
    </MyContext.Provider>
  );
}

function Child() {
  const value = useContext(MyContext);

  return <h1>{value}</h1>;
}
```

Here, the Child component directly accesses the value provided by the parent through Context.

## 31. Explain useReducer Hook

`useReducer` is a React Hook used to manage state using a reducer function.

It is useful when state logic is complex or when multiple state updates depend on different actions.

It accepts two main arguments:

- Reducer function.
- Initial state.

It returns:

- Current state.
- Dispatch function.

Example:

```jsx
import { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return state + 1;

    case 'decrement':
      return state - 1;

    default:
      return state;
  }
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <>
      <h1>{count}</h1>

      <button onClick={() => dispatch({ type: 'increment' })}>
        Increase
      </button>

      <button onClick={() => dispatch({ type: 'decrement' })}>
        Decrease
      </button>
    </>
  );
}
```

## 32. List all the Hooks we can use to manage state in React with examples

The main Hooks used for managing state are:

### 1. useState

Used to manage simple state values.

```jsx
const [count, setCount] = useState(0);

setCount(10);
```

### 2. useReducer

Used to manage more complex state logic.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);

dispatch({ type: 'increment' });
```

### 3. useContext

Used to access shared state provided through Context.

```jsx
const theme = useContext(ThemeContext);
```

**Important:** `useContext` itself does not manage state. It lets components access shared values, which may be managed using `useState` or `useReducer`.

### 4. useSyncExternalStore

Used to subscribe to an external store and read its current snapshot.

```jsx
const snapshot = useSyncExternalStore(
  store.subscribe,
  store.getSnapshot
);
```

It is useful when working with external state-management systems.

## 33. Difference between a DOM element and a React element

### DOM element

A DOM element is an actual object representing an element in the browser's Document Object Model.

Example:

```javascript
const heading = document.createElement('h1');

heading.textContent = 'Hello';
```

Here, `heading` is an actual DOM element.

### React element

A React element is a JavaScript object that describes what should appear on the screen.

Example:

```jsx
const heading = <h1>Hello</h1>;
```

Here, `heading` is a React element, not an actual DOM element.

### Difference

| DOM Element | React Element |
|---|---|
| Represents an actual browser DOM node. | Describes what should appear in the UI. |
| Created using browser DOM APIs. | Created using JSX or `React.createElement()`. |
| Can be directly modified using DOM APIs. | Should be treated as immutable. |
| Exists in the browser DOM. | Used by React during rendering. |

## 34. What happens when a runtime error occurs in JSX? How can we fix it?

When a runtime error occurs during rendering, React may fail to render the affected component tree.

For example:

```jsx
function App() {
  const user = null;

  return <h1>{user.name}</h1>;
}
```

Here, accessing `name` on `null` causes a runtime error.

### How can we fix it?

**1. Optional chaining**

```jsx
<h1>{user?.name}</h1>
```

**2. Conditional rendering**

```jsx
{user && <h1>{user.name}</h1>}
```

**3. Error Boundaries**

Error Boundaries catch errors in their child component tree and display fallback UI.

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      hasError: false
    };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong!</h1>;
    }

    return this.props.children;
  }
}
```

Error Boundaries do not catch every kind of error. For example, they don't catch errors in event handlers or asynchronous callbacks.

## 35. Explain the Rules of Hooks

There are two main Rules of Hooks:

### Rule 1: Only call Hooks at the top level

We should not call Hooks inside:

- Conditions.
- Loops.
- Nested functions.
- Event handlers.

Hooks should be called at the top level of a functional component or a custom Hook.

### Rule 2: Only call Hooks from React functions

We should call Hooks only inside:

- Functional components.
- Custom Hooks.

We should not call Hooks directly inside normal JavaScript functions.

## 36. Why can't we put Hooks inside an if statement?

We cannot call Hooks inside an if statement because React relies on the order of Hook calls to maintain the correct state and other Hook information between renders.

Example of incorrect usage:

```jsx
function App({ isLoggedIn }) {
  if (isLoggedIn) {
    const [name, setName] = useState('');
  }

  return <h1>Hello</h1>;
}
```

If `isLoggedIn` changes, the number and order of Hook calls may change between renders.

This can cause incorrect Hook behavior.

**Correct approach:**

```jsx
function App({ isLoggedIn }) {
  const [name, setName] = useState('');

  if (!isLoggedIn) {
    return <h1>Please login</h1>;
  }

  return <h1>Welcome {name}</h1>;
}
```

Here, the Hook is called at the top level on every render.

## 37. What is the advantage of using React.StrictMode?

React.StrictMode is a development tool used to identify potential problems in a React application.

Advantages:

- Helps identify unsafe lifecycle methods in class components.
- Helps identify unexpected side effects.
- Helps detect deprecated APIs.
- Helps find bugs related to missing cleanup in Effects.
- Helps identify some problems with impure rendering.

Example:

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

**Important:** StrictMode does not affect the production build. In development, it may intentionally run certain functions and Effect setup/cleanup cycles more than once to help identify bugs.

## 38. Can you create the production build of a React app?

Yes, we can create a production build using the build command provided by our build tool.

For a Vite React application:

**Step 1: Open the project terminal.**

**Step 2: Run:**

```bash
npm run build
```

**Step 3: Vite creates an optimized production build inside the `dist` folder.**

**Step 4: To preview the production build locally, run:**

```bash
npm run preview
```

The production build contains optimized assets that can be deployed to a hosting platform.

## 39. Difference between Development and Production

### Development

- Used while developing and testing the application.
- Provides helpful error messages and debugging information.
- Supports features like Hot Module Replacement.
- May include extra development checks.
- Usually not optimized for final deployment.

### Production

- Used when the application is ready for users.
- Contains optimized and bundled files.
- Usually has smaller and compressed assets.
- Removes development-only checks and warnings.
- Designed for better performance.

