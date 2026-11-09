# React Fundamentals – Understanding the Basics

## 1. What is React?

React is a JavaScript library used for building user interfaces. It helps us create interactive websites by dividing the UI into small, reusable pieces called components.

Imagine building an e-commerce website. It contains a navbar, search bar, product cards, shopping cart and footer. Instead of writing everything in one file, we can create separate components for each part and combine them.

The main advantage of React is reusability. We can create a component once and use it multiple times.

For example:

```jsx
function Welcome() {
  return <h1>Hello React!</h1>;
}
```

Here, Welcome is a component that displays a heading.

The main idea is that we describe what the UI should look like, and React updates it when the data changes.

## 2. What are JSX, Components and Props?

### JSX

JSX stands for JavaScript XML. It allows us to write HTML-like syntax inside JavaScript.

For example:

```jsx
const element = <h1>Hello World</h1>;
```

This looks like HTML, but it is actually JSX.

A few differences between HTML and JSX:

- We use `className` instead of `class`.
- Every tag should be properly closed.
- We use curly braces `{}` to write JavaScript expressions inside JSX.

Example:

```jsx
const name = "Teja";

function App() {
  return <h1>Hello {name}</h1>;
}
```

JSX makes our code easier to read and write.

### Components

A component is a reusable piece of UI. It helps us divide a large application into smaller and manageable parts.

For example, a website can have:

```text
App
 |
 |-- Navbar
 |
 |-- Sidebar
 |
 |-- ProductList
 |       |
 |       |-- ProductCard
 |
 |-- Footer
```

Each part can be created as a separate component.

```jsx
function Navbar() {
  return <h1>My Website</h1>;
}
```

We can reuse this Navbar component wherever required.

### Props

Props stands for properties. They are used to pass data from one component to another, mainly from parent to child.

Think of props like function arguments. We pass different values to the same component to get different results.

Example:

```jsx
function User(props) {
  return <h2>Hello {props.name}</h2>;
}

function App() {
  return (
    <>
      <User name="Teja" />
      <User name="Rahul" />
    </>
  );
}
```

Here, we are using the same User component with different names.

One important rule: Props are read-only. A child component should not directly modify the props it receives.

## 3. What is Babel and what role does it play in React?

Browsers understand JavaScript, but they cannot directly understand JSX.

For example:

```jsx
const element = <h1>Hello React</h1>;
```

If we write JSX directly in a browser without transforming it, the browser will throw an error.

This is where Babel comes in.

Babel is a JavaScript compiler that transforms JSX and modern JavaScript syntax into JavaScript that browsers can execute.

For example, JSX:

```jsx
const element = <h1>Hello</h1>;
```

Can be transformed into something like:

```javascript
const element = React.createElement(
  "h1",
  null,
  "Hello"
);
```


## 4. What is the difference between Virtual DOM and Real DOM?

First, let's understand what DOM means.

DOM stands for Document Object Model. It represents an HTML document as a tree-like structure.

### Real DOM

The Real DOM is the actual document structure maintained by the browser.

Whenever we change something in the DOM, the browser may need to update its layout and repaint the screen.

### Virtual DOM

The Virtual DOM is a lightweight JavaScript representation of the UI that React uses to determine what needs to be updated.

Imagine you have a list containing 100 products, and you update the price of only one product.

React compares the previous and updated UI representations and identifies the necessary changes.

This process is called reconciliation.

The basic process:

1. Something changes in the application, such as state.
2. React renders the component again.
3. React compares the previous and new UI representations.
4. It determines the necessary changes.
5. React commits those changes to the Real DOM.

### Difference between Virtual DOM and Real DOM

| Real DOM | Virtual DOM |
|---|---|
| Actual DOM maintained by the browser | Lightweight representation of UI |
| Directly represents HTML elements | Represents UI in memory |
| Browser manages DOM updates | React uses it to determine updates |
| DOM operations can be expensive | Helps React manage UI updates efficiently |

## 5. What is a Bundler?

A React project contains multiple files such as JavaScript files, CSS files, images and external packages.

Managing all these files individually can become difficult.

A bundler is a tool that processes application files and their dependencies and prepares them for the browser.

It also helps with:

- Dependency resolution.
- Combining application modules.
- Minifying code.
- Optimizing assets.
- Preparing production builds.

Some examples of bundlers and build tools are Webpack, Parcel, Rollup and Vite.

Think of a bundler like combining multiple chapters into one organized book before giving it to the reader.

## 6. Why are we using Vite instead of Create React App?

Create React App (CRA) was previously used to create React projects without manually configuring the development environment.

But nowadays, we generally use Vite.

Vite is a modern frontend build tool that provides a faster development experience.

### Why Vite?

- **Speed:** Vite starts the development server quickly.
- **Fast updates:** Changes in files are reflected in the browser quickly.
- **HMR:** Hot Module Replacement updates modules without requiring a full page reload in many cases.
- **Production build:** It optimizes the application for production.


To create a React project using Vite:

```bash
npm create vite@latest my-app -- --template react

cd my-app

npm install

npm run dev
```

## 7. Understanding the React Folder Structure

When we create a React project using Vite, it generates a basic folder structure.

```text
my-app/
|
|-- node_modules/
|
|-- public/
|
|-- src/
|    |
|    |-- assets/
|    |
|    |-- components/
|    |
|    |-- App.jsx
|    |
|    |-- App.css
|    |
|    |-- index.css
|    |
|    |-- main.jsx
|
|-- index.html
|
|-- package.json
|
|-- vite.config.js
|
|-- .gitignore
```

Let's understand the important folders and files.

**node_modules:** Contains all the installed packages and dependencies. We don't normally modify this folder manually.

**public:** Contains static files such as images and favicons that can be served directly.

**src:** This is where we write most of our application code.

**assets:** Contains images, icons and other resources used in the application.

**components:** We create reusable UI components here.

**App.jsx:** This is generally the root application component. We combine other components inside it.

**main.jsx:** This is the entry point of our React application. It renders the App component inside the root element.

**index.html:** This contains the root HTML element where React renders the application.

**package.json:** Contains project details, dependencies and scripts such as dev and build.

**vite.config.js:** Contains the configuration for Vite.

### How does the application start?

The execution flow is:

```text
index.html
     |
     v
  main.jsx
     |
     v
   App.jsx
     |
     v
Other Components
     |
     v
  Browser UI
```

The main.jsx file connects our React application to the root element in index.html.

## 8. What is the difference between Class and Functional Components?

React supports two ways of creating components.

### Class Components

Class components are created using JavaScript classes and extend React.Component.

They use a render() method to return JSX.

Example:

```jsx
import { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello React</h1>;
  }
}

export default Welcome;
```

### Functional Components

Functional components are JavaScript functions that return JSX.

Example:

```jsx
function Welcome() {
  return <h1>Hello React</h1>;
}

export default Welcome;
```

Functional components are simpler and allow us to use Hooks for managing state and other React features.

### Difference

| Class Components | Functional Components |
|---|---|
| Created using classes | Created using functions |
| Use render() method | Return JSX directly |
| Use this.state | Use useState |
| Use lifecycle methods | Use Hooks like useEffect |
| Require this keyword | Don't require this keyword |

Nowadays, functional components are generally preferred for new React applications.

## 9. What are Hooks in React?

Hooks are special functions provided by React that allow functional components to use React features such as state, effects and references.

Before Hooks were introduced, developers mainly used class components to manage state and lifecycle methods.

Hooks made it possible to use these features inside functional components.

Some commonly used Hooks are:

- useState
- useEffect
- useRef
- useContext
- useMemo
- useCallback
- useReducer

There are two important rules of Hooks:

1. Always call Hooks at the top level of a component or custom Hook.
2. Don't call Hooks inside loops, conditions or nested functions.

## 10. Understanding Basic Hooks: useState, useEffect and useRef

### useState – Managing State

useState is a React Hook used to manage state inside functional components.

State is data that a component remembers. When state changes, React schedules a re-render to update the UI.

For example, consider a counter application.

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>{count}</h1>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </>
  );
}
```

Here:

- `count` stores the current value.
- `setCount` is used to update the value.
- `useState(0)` initializes the state with 0.

Whenever we click the button, setCount updates the state and React renders the component with the updated value.

A normal variable cannot do this automatically because changing a normal variable doesn't trigger a React re-render.

### useEffect – Handling Side Effects

useEffect is a React Hook used to synchronize a component with external systems.

Some common use cases are:

- Fetching API data.
- Setting up timers.
- Adding event listeners.
- Subscribing to external services.
- Cleaning up resources.

Example:

```jsx
import { useEffect, useState } from 'react';

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    const fetchUsers = async () => {
      const response = await fetch(
        'https://jsonplaceholder.typicode.com/users'
      );

      const data = await response.json();

      setUsers(data);
    };

    fetchUsers();
  }, []);

  return <h1>Total Users: {users.length}</h1>;
}
```

Here, useEffect fetches user data after the component initially mounts.

### Dependency Array

The dependency array controls when the effect runs.

**Without dependency array:**

```jsx
useEffect(() => {
  console.log('Rendered');
});
```

Runs after every committed render.

**With an empty dependency array:**

```jsx
useEffect(() => {
  console.log('Mounted');
}, []);
```

Runs after the initial mount.

**With dependencies:**

```jsx
useEffect(() => {
  console.log('Count changed');
}, [count]);
```

Runs after the initial mount and whenever count changes.

### Cleanup Function

Sometimes we start timers or add event listeners inside useEffect. We need to clean them up when they are no longer required.

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log('Hello');
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

The cleanup function clears the timer when the effect is cleaned up.

### useRef – Accessing DOM Elements

useRef is a React Hook used to store mutable values between renders without triggering a re-render when the value changes.

It is commonly used for two purposes:

1. Accessing DOM elements directly.
2. Storing values such as timer IDs.

For example, imagine we have an input field and a button. When we click the button, the input should automatically get focused.

```jsx
import { useRef } from 'react';

function App() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />

      <button onClick={handleClick}>
        Focus Input
      </button>
    </>
  );
}
```

Here:

- `useRef(null)` creates a reference object.
- `ref={inputRef}` connects the reference to the input element.
- `inputRef.current` gives access to the actual DOM element.
- `focus()` places the cursor inside the input.

Unlike useState, updating the current property of a ref doesn't trigger a re-render.

### Difference between useState and useRef

| useState | useRef |
|---|---|
| Used to manage state | Used to store mutable values |
| Updating state triggers a re-render | Updating current doesn't trigger a re-render |
| Used when UI needs to update | Used for DOM access and storing values |

A simple way to remember:

Use useState when the screen needs to change. Use useRef when you want to store a value or access an element without triggering a re-render.

## 11. How do we pass data from one component to another?

In React, data generally flows in one direction, from parent to child.

There are different ways to communicate between components.

### Parent to Child

We use props to pass data from the parent component to the child component.

```jsx
function App() {
  return <Profile name="Teja" />;
}

function Profile({ name }) {
  return <h1>Hello {name}</h1>;
}
```

Here, App is the parent and Profile is the child.

### Child to Parent

A child cannot directly pass props to its parent.

Instead, the parent passes a callback function to the child, and the child calls that function to send data back.

```jsx
function App() {
  const handleData = (data) => {
    console.log(data);
  };

  return <Child sendData={handleData} />;
}

function Child({ sendData }) {
  return (
    <button onClick={() => sendData('Hello Parent')}>
      Send Data
    </button>
  );
}
```

Here, the child calls the function received through props.

### Sibling to Sibling

If two components are siblings, we cannot directly pass props between them.

We can solve this using a concept called Lifting State Up.

## 12. What is Lifting State Up?

Lifting State Up means moving state from child components to their closest common parent component.

Imagine we have two components:

- SearchBar
- ProductList

When we enter something in the SearchBar, the ProductList should display matching products.

Both components need access to the search value.

Instead of maintaining separate states, we move the state into their common parent.

```text
          App
        (State)
         /    \
        /      \
  SearchBar  ProductList
```

Now both components receive the same state through props.

The benefits are:

- Maintains a single source of truth.
- Allows sibling components to share data.
- Keeps components synchronized.
- Avoids duplicate state.

## 13. How do we use Event Listeners in React?

Event handling allows us to perform actions when users interact with the application.

For example:

- Clicking a button.
- Typing in an input field.
- Submitting a form.
- Pressing a keyboard key.
- Moving the mouse over an element.

React provides event handlers through JSX attributes.

### onClick

Used when a user clicks an element.

```jsx
function App() {
  const handleClick = () => {
    alert('Button clicked');
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}
```

### onChange

Used when an input value changes.

```jsx
function App() {
  const handleChange = (event) => {
    console.log(event.target.value);
  };

  return <input onChange={handleChange} />;
}
```

Here, event.target.value gives the current input value.

### onSubmit

Used when submitting a form.

```jsx
function App() {
  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" />

      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

We use event.preventDefault() to prevent the browser's default form submission behavior, which normally causes a page reload.

### Using addEventListener()

Sometimes we need to listen to browser-level events such as window resize.

For this, we can use addEventListener() inside useEffect().

```jsx
useEffect(() => {
  const handleResize = () => {
    console.log(window.innerWidth);
  };

  window.addEventListener('resize', handleResize);

  return () => {
    window.removeEventListener('resize', handleResize);
  };
}, []);
```

Here, we add a resize event listener and remove it during cleanup.

