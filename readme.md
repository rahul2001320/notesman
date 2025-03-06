# React.js Version 18 Study Notes

## Table of Contents

1. [Introduction to React.js](#introduction-to-reactjs)
   - [What is React?](#what-is-react)
   - [History and Evolution](#history-and-evolution)
   - [Key Features](#key-features)
2. [Setting Up the Environment](#setting-up-the-environment)
   - [Node.js and npm](#nodejs-and-npm)
   - [Create React App](#create-react-app)
   - [Project Structure](#project-structure)
3. [JSX (JavaScript XML)](#jsx-javascript-xml)
   - [Introduction to JSX](#introduction-to-jsx)
   - [Embedding Expressions in JSX](#embedding-expressions-in-jsx)
   - [JSX Syntax and Best Practices](#jsx-syntax-and-best-practices)
4. [Components](#components)
   - [Functional Components](#functional-components)
   - [Class Components](#class-components)
   - [Component Lifecycle](#component-lifecycle)
   - [Props and State](#props-and-state)
   - [Handling Events](#handling-events)
5. [State Management](#state-management)
   - [useState Hook](#usestate-hook)
   - [useReducer Hook](#usereducer-hook)
   - [Context API](#context-api)
   - [Third-Party Libraries (Redux, MobX)](#third-party-libraries-redux-mobx)
6. [Hooks](#hooks)
   - [Introduction to Hooks](#introduction-to-hooks)
   - [useEffect](#useeffect)
   - [useContext](#usecontext)
   - [Custom Hooks](#custom-hooks)
   - [Rules of Hooks](#rules-of-hooks)
7. [React Router](#react-router)
   - [Introduction to React Router](#introduction-to-react-router)
   - [Setting Up React Router](#setting-up-react-router)
   - [Route Parameters](#route-parameters)
   - [Nested Routes](#nested-routes)
   - [Redirects and Navigation](#redirects-and-navigation)
8. [Forms and Input Handling](#forms-and-input-handling)
   - [Controlled Components](#controlled-components)
   - [Uncontrolled Components](#uncontrolled-components)
   - [Form Validation](#form-validation)
9. [Styling in React](#styling-in-react)
   - [CSS and Inline Styles](#css-and-inline-styles)
   - [CSS Modules](#css-modules)
   - [Styled-Components](#styled-components)
   - [Emotion](#emotion)

## 1. Introduction to React.js
### What is React?
React is a JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies. React allows developers to create large web applications that can update and render efficiently in response to data changes.

### History and Evolution
- **2011:** React was created by Jordan Walke, a software engineer at Facebook.
- **2012:** Deployed on Facebook's newsfeed.
- **2013:** Open-sourced at JSConf US.
- **2015:** React Native was introduced.
- **2017:** React Fiber was introduced.
- **2021:** React 18 introduced Concurrent Mode.

### Key Features
- **Declarative:** React makes it painless to create interactive UIs. Design simple views for each state in your application, and React will efficiently update and render just the right components when your data changes.
- **Component-Based:** Build encapsulated components that manage their own state, then compose them to make complex UIs.
- **Learn Once, Write Anywhere:** You can develop new features in React without rewriting existing code. React can also render on the server using Node and power mobile apps using React Native.
- **Virtual DOM:** React uses a virtual DOM to optimize updates and rendering.
- **JSX:** A syntax extension that allows mixing HTML with JavaScript.

## 2. Setting Up the Environment
### Node.js and npm
Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. npm is the package manager for Node.js. Make sure you have Node.js installed on your machine.

### Create React App
Create React App is an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.

```bash
npx create-react-app my-app
cd my-app
npm start
```

### Project Structure
```
my-app/
├── node_modules/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   └── serviceWorker.js
├── .gitignore
├── package.json
└── README.md
```

## 3. JSX (JavaScript XML)
### Introduction to JSX
JSX is a syntax extension to JavaScript. It is used with React to describe what the UI should look like. JSX produces React "elements".

```jsx
const element = <h1>Hello, world!</h1>;
```

### Embedding Expressions in JSX
You can embed any JavaScript expression in JSX by wrapping it in curly braces.

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

### JSX Syntax and Best Practices
- **Use camelCase for HTML attributes:** For example, `class` becomes `className` in JSX.
- **Close all tags:** JSX requires that tags be explicitly closed.
- **Use fragments to group multiple elements:** Fragments let you group a list of children without adding extra nodes to the DOM.

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

## 4. Components
### Functional Components
Functional components are simple functions that return JSX. They are stateless and do not have lifecycle methods.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### Class Components
Class components are ES6 classes that extend from `React.Component`. They have a render method that returns JSX.

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Component Lifecycle
React components go through a lifecycle of events:
- **Mounting:** When the component is being inserted into the DOM.
  - `constructor()`
  - `static getDerivedStateFromProps()`
  - `render()`
  - `componentDidMount()`
- **Updating:** When the component is being re-rendered as a result of changes to props or state.
  - `static getDerivedStateFromProps()`
  - `shouldComponentUpdate()`
  - `render()`
  - `getSnapshotBeforeUpdate()`
  - `componentDidUpdate()`
- **Unmounting:** When the component is being removed from the DOM.
  - `componentWillUnmount()`

### Props and State
Props are read-only and passed to components. State is managed within the component.

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

### Handling Events
Handling events in React is similar to handling events in DOM elements. However, there are some syntactic differences.

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

## 5. State Management
### useState Hook
The `useState` hook lets you add state to functional components.

```jsx
import React, { useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### useReducer Hook
The `useReducer` hook is usually preferable to `useState` when you have complex state logic.

```jsx
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

### Context API
Context provides a way to pass data through the component tree without having to pass props down manually at every level. 

```jsx
const ThemeContext = React.createContext('light');

class App extends React.Component {
  render() {
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```

### Third-Party Libraries (Redux, MobX)
Redux and MobX are popular state management libraries for React.

## 6. Hooks
### Introduction to Hooks
Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

### useEffect
The `useEffect` hook lets you perform side effects in function components.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### useContext
The `useContext` hook lets you subscribe to React context without introducing nested render props.

```jsx
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}
```

### Custom Hooks
You can create custom hooks to extract and share logic between components.

```jsx
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    // Assume ChatAPI is an external system for managing user status
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  }, [friendID]);

  return isOnline;
}
```

### Rules of Hooks
- Only call Hooks at the top level.
- Only call Hooks from React function components or custom Hooks.

## 7. React Router
### Introduction to React Router
React Router is a standard library for routing in React. It enables the navigation among views of various components in a React Application, allows changing the browser URL, and keeps UI in sync with the URL.

### Setting Up React Router
```bash
npm install react-router-dom
```

### Route Parameters
Route parameters are used to capture specific values from the URL.

```jsx
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
  useParams
} from "react-router-dom";

function App() {
  return (
    <Router>
      <div>
        <ul>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/users">Users</Link>
          </li>
        </ul>

        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/users">
            <Users />
          </Route>
          <Route path="/:id">
            <Child />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}

function Child() {
  let { id } = useParams();
  return (
    <div>
      <h3>ID: {id}</h3>
    </div>
  );
}
```

### Nested Routes
Nested routes allow you to render sub-routes inside a parent route.

```jsx
function App() {
  return (
    <Router>
      <Switch>
        <Route path="/:id" children={<Child />} />
      </Switch>
    </Router>
  );
}

function Child() {
  let { id } = useParams();
  return (
    <div>
      <h3>ID: {id}</h3>
    </div>
  );
}
```

### Redirects and Navigation
Redirects can be used to programmatically navigate users to different routes.

```jsx
import { Redirect } from "react-router-dom";

function App() {
  return (
    <Router>
      <div>
        <Switch>
          <Route path="/home">
            <Home />
          </Route>
          <Redirect from="/old-home" to="/home" />
          <Route path="/login">
            <Login />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}
```

## 8. Forms and Input Handling
### Controlled Components
In controlled components, form data is handled by the React component.

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Uncontrolled Components
Uncontrolled components store form data in the DOM.

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.input = React.createRef();
  }

  handleSubmit = (event) => {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Form Validation
Validation can be performed using state and controlled components.

```jsx
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      username: '',
      email: '',
      password: '',
      errors: {
        username: '',
        email: '',
        password: ''
      }
    };
  }

  handleChange = (event) => {
    const { name, value } = event.target;
    let errors = this.state.errors;

    switch (name) {
      case 'username':
        errors.username =
          value.length < 5
            ? 'Username must be at least 5 characters long!'
            : '';
        break;
      case 'email':
        errors.email =
          value.includes('@')
            ? ''
            : 'Email is not valid!';
        break;
      case 'password':
        errors.password =
          value.length < 8
            ? 'Password must be at least 8 characters long!'
            : '';
        break;
      default:
        break;
    }

    this.setState({ errors, [name]: value });
  }

  handleSubmit = (event) => {
    event.preventDefault();
    if (this.validateForm(this.state.errors)) {
      console.info('Valid Form')
    } else {
      console.error('Invalid Form')
    }
  }

  validateForm = (errors) => {
    let valid = true;
    Object.values(errors).forEach(
      (val) => val.length > 0 && (valid = false)
    );
    return valid;
  }

  render() {
    const { errors } = this.state;
    return (
      <form onSubmit={this.handleSubmit}>
        <div>
          <label>Username</label>
          <input type="text" name="username" onChange={this.handleChange} />
          {errors.username.length > 0 && 
            <span>{errors.username}</span>}
        </div>
        <div>
          <label>Email</label>
          <input type="email" name="email" onChange={this.handleChange} />
          {errors.email.length > 0 && 
            <span>{errors.email}</span>}
        </div>
        <div>
          <label>Password</label>
          <input type="password" name="password" onChange={this.handleChange} />
          {errors.password.length > 0 && 
            <span>{errors.password}</span>}
        </div>
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

## 9. Styling in React
### CSS and Inline Styles
You can style components directly with CSS or use inline styles.

```jsx
const divStyle = {
  color: 'blue',
  backgroundImage: 'url(' + imgUrl + ')',
};

function HelloWorldComponent() {
  return <div style={divStyle}>Hello World!</div>;
}
```

### CSS Modules
CSS Modules allow you to scope CSS to a particular component.

```css
// styles.module.css
.error {
  color: red;
}
```

```jsx
import styles from './styles.module.css';

function ErrorMessage() {
  return <div className={styles.error}>Error!</div>;
}
```

### Styled-Components
Styled-components use tagged template literals to style components.

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
`;

function App() {
  return (
    <div>
      <Button primary>Primary Button</Button>
      <Button>Default Button</Button>
    </div>
  );
}
```

### Emotion
Emotion is a library designed for writing CSS styles with JavaScript.

```jsx
/** @jsxImportSource @emotion/react */
import { css } from '@emotion/react';

const style = css`
  color: hotpink;
`;

function App() {
  return <div css={style}>This is hotpink.</div>;
}
```
