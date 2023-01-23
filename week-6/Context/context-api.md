# Context API

The **`Context API`** is a feature in React that allows you to pass data and methods down through a component tree without having to pass props down manually at every level. It allows you to share values between components that are not directly related to each other in the component tree.

The **`Context API`** consists of two main parts: the **`context`** itself and the **`context provider`**. The **`context`** is an object that can be created using the **`React.createContext()`** method. It can be used to store data or methods that need to be shared between components. The **`context provider`** is a component that wraps other components and provides the context to them. The wrapped components can then use the **`useContext`** hook to access the context.

The **`Context API`** can be useful when you have data or methods that are needed by multiple components throughout your application, and you want to avoid having to pass props down through all of the components. It can also help to keep your component tree more organized by allowing you to separate the components that handle data and logic from the components that only display data.

```jsx
import React, { useContext } from "react";

// Create the context
const MyContext = React.createContext();

// Create a provider component
const MyProvider = (props) => {
  const [state, setState] = useState({
    /* initial state */
  });

  return (
    <MyContext.Provider value={{ state, setState }}>
      {props.children}
    </MyContext.Provider>
  );
};

// Use the context in a functional component
const MyFunctionalComponent = () => {
  const { state, setState } = useContext(MyContext);

  return (
    <div>
      <p>{state.example}</p>
      <button onClick={() => setState({ example: "new value" })}>
        Change value
      </button>
    </div>
  );
};

// Wrap your app with the provider
const App = () => {
  return (
    <MyProvider>
      <MyFunctionalComponent />
    </MyProvider>
  );
};
```

In this example, we first import the **`useContext`** hook from React. Then we create a context using the **`React.createContext()`** method. Next, we create a provider component that wraps the children components in the context and provides the state and a setState method. Finally, we use the context in the functional component by using the **`useContext`**
hook and destructuring the state and setState from the context.
