DEV Community
# React Props vs State: What's the Difference?

javascript
## When I was learning React, I found that understanding the difference between "props" and "state" can be a bit confusing for beginners. In this blog post, I want to share what I've learned in a way that's easy to grasp, with simple code examples, so that even beginners can begin to understand it.

* Props: Passing Data from Parent to Child

* Imagine a React component as a building block of your web application. Props (short for properties) are like the information or instructions you pass to each building block. They allow you to send data from a parent component to a child component. React's data flow between components is always uni-directional.

** Here's an example of how data can be passed by using props:

## Parent Component
```js
function App() {
  return (
    <ChildComponent name="John" age={30} />
  );
}
```

## Child Component
```js
function ChildComponent(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}
```
* In the example above, the App component is the parent component, and it passes data to the ChildComponent component using props. The ChildComponent component receives the data as an object called props.

* State: Managing Component-Specific Data

* While props are used for passing data from parent to child, state is used to manage data that can change over time within a component. Unlike props, state is managed within the component itself.

# Here's an example of how state can be used in a component:
```js
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```
** In the example above, the Counter component uses the useState hook to manage its own state. The count variable is initialized to 0, and the setCount function is used to update the count variable when the button is clicked.

# Differences Between Props and State

* Here are the key differences between props and state:

*Ownership: Props are owned by the parent component and passed down to child components, while state is owned and managed within the component itself.
*Mutability: Props are immutable, meaning they cannot be changed by the child component. State, on the other hand, can be changed using the setState function.
*Usage: Props are used to pass data from parent to child components, while state is used to manage data that can change over time within a component.
*In summary, props and state are both important concepts in React. Props are used to pass data from parent to child components, while state is used to manage data that can change over time within a component. Understanding the differences between props and state is crucial for building React applications.

# How Parent and Child Components Share Props in React.js

In React, props (short for properties) are used to pass data from a parent component to a child component. The data flows one-way (top-down) from the parent to the child.

## 1️⃣ Passing Props from Parent to Child
The parent component sends props to the child by defining them as attributes on the child component.

### Example:
```jsx
// Parent Component
import React from "react";
import ChildComponent from "./ChildComponent";

const ParentComponent = () => {
  const message = "Hello from Parent!";

  return <ChildComponent greeting={message} />;
};

export default ParentComponent;
```

```jsx
// Child Component
import React from "react";

const ChildComponent = ({ greeting }) => {
  return <h1>{greeting}</h1>;
};

export default ChildComponent;
```

### 🔹 How it works:
- The parent passes `message` as a prop (`greeting={message}`).
- The child receives `greeting` and displays it.

---

## 2️⃣ Passing Data from Child to Parent (Using Callback Functions)
To send data from the child to the parent, the parent can pass a callback function as a prop. The child calls this function with the data it wants to send.

### Example:
```jsx
// Parent Component
import React, { useState } from "react";
import ChildComponent from "./ChildComponent";

const ParentComponent = () => {
  const [childMessage, setChildMessage] = useState("");

  const handleChildData = (data) => {
    setChildMessage(data);
  };

  return (
    <div>
      <h1>Message from Child: {childMessage}</h1>
      <ChildComponent sendDataToParent={handleChildData} />
    </div>
  );
};

export default ParentComponent;
```

```jsx
// Child Component
import React from "react";

const ChildComponent = ({ sendDataToParent }) => {
  const handleClick = () => {
    sendDataToParent("Hello from Child!");
  };

  return <button onClick={handleClick}>Send Data to Parent</button>;
};

export default ChildComponent;
```

### 🔹 How it works:
- The parent passes `handleChildData` as a prop (`sendDataToParent={handleChildData}`).
- The child calls `sendDataToParent("Hello from Child!")`, sending data back.
- The parent updates `childMessage` and displays it.

---

## 3️⃣ Using Context API for Deeply Nested Components
If props need to be passed to deeply nested components, Context API can be used instead of prop drilling.

### Example:
```jsx
import React, { createContext, useContext } from "react";

// Create a Context
const MessageContext = createContext();

const ParentComponent = () => {
  return (
    <MessageContext.Provider value="Hello from Context!">
      <ChildComponent />
    </MessageContext.Provider>
  );
};

const ChildComponent = () => {
  const message = useContext(MessageContext); // Access context value
  return <h1>{message}</h1>;
};

export default ParentComponent;
```

### 🔹 How it works:
- `MessageContext.Provider` shares `value="Hello from Context!"` with all child components.
- `useContext(MessageContext)` allows the child to consume the value without prop drilling.

---

By using props, callback functions, or the Context API, React enables efficient data flow between components. 🎉


