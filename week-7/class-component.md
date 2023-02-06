# Class component

A React class component, also known as a "class component," is a type of component in the React JavaScript library that is defined as a JavaScript class. It allows you to write components using an object-oriented syntax, and provides additional features such as lifecycle methods and the ability to use a constructor and state.

Here is an example of a basic React class component:

```jsx
import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      message: "Hello, World!",
    };
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
}

export default ExampleComponent;
```

In this example, we define a class **`ExampleComponent`** that extends the **`Component`** class from the **`react`** library. The class has a **`constructor`** method that calls **`super(props)`** to pass the props from the parent component to the base class. We also define a **`state`** object with a **`message`** property.

The **`render`** method returns a JSX template that displays the **`message`** from the **`state`** object.

The **`constructor`** method is a special method in a React class component that is called when an instance of the component is created. It's used to set the initial state of the component and bind event handlers to **`this`**. In a class component, you must call the **`super`** method with the **`props`** argument inside the constructor, before using **`this`**. This allows you to access the props passed down from the parent component and makes sure that the **`Component`** class' constructor is also called.

The **`super`** keyword refers to the parent class. In this case, when we call **`super(props)`** in the constructor, we are calling the constructor of the **`Component`** class, which is the parent class of our custom **`ExampleComponent`** class. By passing **`props`** to **`super`**, we make sure that the **`props`** are correctly passed from the parent to the **`Component`** class.

Here's an example to help illustrate:

```jsx
class ExampleComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      message: "Hello, World!",
    };
  }
  // ...
}
```

In a class component, the **`state`** object is used to store the component's internal data. You can update the state using the **`setState`** method, which triggers a re-render of the component.

Event handling in class components is done by binding event handlers to **`this`** in the constructor, then passing them as callbacks to event properties in the component's render method.

Here's an example that demonstrates how to handle an input field change event in a class component:

```jsx
import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: "",
    };
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(event) {
    this.setState({
      inputValue: event.target.value,
    });
  }

  render() {
    return (
      <div>
        <input
          type='text'
          value={this.state.inputValue}
          onChange={this.handleChange}
        />
        <p>{this.state.inputValue}</p>
      </div>
    );
  }
}

export default ExampleComponent;
```

In this example, we define a **`handleChange`** method that updates the component's state when the input field's value changes. We bind the method to **`this`** in the constructor so that we can access **`this.setState`** inside the method. We then pass the **`handleChange`** method as a callback to the **`onChange`** event of the input field.

When the user types in the input field, the **`handleChange`** method is called and updates the component's state, which triggers a re-render of the component and displays the updated input value.

**Lifecycle Methods**

React class components have several lifecycle methods that allow you to run logic at specific points in the process of rendering a component. These methods give you control over when and how a component is updated, as well as how it is created and destroyed.

Here are the most commonly used lifecycle methods:

- **`constructor`**: Called before the component is mounted. You can use this method to set up the initial state and bind event handlers to **`this`**.
- **`render`**: Returns the JSX that represents the component. This method is called every time the component's state or props change.
- **`componentDidMount`**: Called after the component has been rendered to the DOM. You can use this method to trigger network requests or set up subscriptions.
- **`shouldComponentUpdate`**: Called before a re-render of the component. You can use this method to optimize performance by avoiding unnecessary re-renders.
- **`componentDidUpdate`**: Called after the component has been updated. You can use this method to run logic that depends on the updated state or props.

Here's a simple example that demonstrates how to use the **`componentDidMount`** lifecycle method:

```jsx
import React, { Component } from "react";

class ExampleComponent extends Component {
  constructor(props) {
    super(props);
    this.state = {
      message: "Hello, World!",
    };
  }

  componentDidMount() {
    console.log("Component did mount");
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
}

export default ExampleComponent;
```

In this example, we define a class component **`ExampleComponent`** that sets the initial state in the constructor. The **`componentDidMount`** lifecycle method is called after the component has been rendered to the DOM. In this example, it logs a message to the console to indicate that the component has been mounted.

**Use cases**

Lifecycle methods have various use cases in real-world applications. Here are a few common examples:

- **`componentDidMount`**: This method is often used to trigger network requests or set up subscriptions. For example, if you have a component that displays a list of articles, you can use **`componentDidMount`** to fetch the articles from an API and update the component's state with the results. This ensures that the component is updated with the latest data as soon as it is mounted.
- **`shouldComponentUpdate`**: This method is useful for improving performance by avoiding unnecessary re-renders. For example, if you have a component that displays a large list of items, you may want to avoid re-rendering the entire list every time the component's state changes. You can use **`shouldComponentUpdate`** to compare the current state to the next state and only re-render the component if the difference is significant.
- **`componentDidUpdate`**: This method is often used to run logic that depends on the updated state or props. For example, if you have a component that displays a form, you can use **`componentDidUpdate`** to scroll the page to the top whenever the form is submitted and the component is updated with the results.
- **`constructor`**: This method is used to set up the initial state and bind event handlers to **`this`**. For example, if you have a component that allows users to submit a form, you can use the constructor to initialize the component's state and bind the **`submit`** method to **`this`** so that it can access the component's state.

In general, lifecycle methods give you fine-grained control over how a component is updated, created, and destroyed. By using these methods, you can write more efficient and maintainable React components that are optimized for performance and functionality.

```jsx
import React, { Component } from "react";

class ArticleList extends Component {
  constructor(props) {
    super(props);
    this.state = {
      articles: [],
      loading: true,
    };
  }

  componentDidMount() {
    // Fetch articles from API
    fetch("https://my-api.com/articles")
      .then((res) => res.json())
      .then((articles) => {
        this.setState({ articles, loading: false });
      });
  }

  shouldComponentUpdate(nextProps, nextState) {
    // Avoid re-rendering the entire list for minor state changes
    return (
      nextState.articles.length !== this.state.articles.length ||
      nextState.loading !== this.state.loading
    );
  }

  componentDidUpdate(prevProps, prevState) {
    // Scroll to top of the page after the component is updated
    if (prevState.articles.length !== this.state.articles.length) {
      window.scrollTo(0, 0);
    }
  }

  render() {
    const { articles, loading } = this.state;
    return (
      <div>
        {loading && <p>Loading articles...</p>}
        {!loading && (
          <ul>
            {articles.map((article) => (
              <li key={article.id}>{article.title}</li>
            ))}
          </ul>
        )}
      </div>
    );
  }
}

export default ArticleList;
```

In this example, we have a **`ArticleList`** component that fetches a list of articles from an API when the component is mounted (**`componentDidMount`**). The **`shouldComponentUpdate`** method is used to avoid re-rendering the entire list for minor state changes. The **`componentDidUpdate`** method is used to scroll the page to the top whenever the list of articles is updated. The component shows a loading message while the articles are being fetched and displays the list of articles once they are loaded.

**What are `nextProps` and `nextState` parameters?**

In React class components, the **`nextProps`** and **`nextState`** parameters are used in the **`shouldComponentUpdate`** and **`componentDidUpdate`** lifecycle methods to compare the current props and state to the next props and state that will be used to render the component.

- **`nextProps`**: The **`nextProps`** parameter is an object that contains the updated props that will be passed to the component when it re-renders. You can use **`nextProps`** to compare the current props to the updated props and determine whether or not the component should update.
- **`nextState`**: The **`nextState`** parameter is an object that contains the updated state that will be used to render the component. You can use **`nextState`** to compare the current state to the updated state and determine whether or not the component should update.

By using **`nextProps`** and **`nextState`**, you can write more efficient and performant React components that only re-render when it is necessary. This can improve the overall performance of your application, especially when working with large and complex components.
