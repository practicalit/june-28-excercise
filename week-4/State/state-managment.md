# State

Is a general concept in software engineering. It is used when a part of your app needs to "remember" something that changes when people interact with it.

![State](/week-4/State/state.png)

This is a simple example, but if we had lots of bits of state, then we can make very complex apps.

### React Hooks

React has built-in functionality for initialising and updating state in our components. We will access state via a React *Hook* called `useState`.

Hooks are a new-ish feature in React. You may find older tutorials that don't use Hooks, but don't panic. The concepts we learn here are the same whether or not you use Hooks. We are looking at Hooks first because they are simpler to learn for beginners.

### Importing `useState`

To be able to access the `useState` Hook, we first need to import it from the React package. Let's look at an example.

```jsx
import React, { useState } from "react";

console.log(useState);
```

If we look at the console, `useState` is just a function. It lives inside the React code that you installed when you created the app.

To reference the `useState` function in our component, we need to import it from the React code. The curly braces around `useState` are a bit like writing:

```jsx
import React from "react";
let useState = React.useState;
```

In fact, we can just write `React.useState`
 in our component, if we want! But to type a bit less code, we import it (using the curly braces) once and then can just use `useState`

### Using `useState`

Now let's look at how we can use the `useState` Hook

```jsx
const friends = [
    {
      id: 1,
      image: imageOne,
      name: "John Doe",
      title: "Front end dev",
      callMobile: "123578900",
    },
    {
      id: 2,
      image: imageTwo,
      name: "Eric Johnatan",
      title: "CTO",
      callMobile: "918309834098",
    },
    {
      id: 3,
      image: imageThree,
      name: "Metin Khaled",
      title: "Team Lead",
      callMobile: "838092382",
    },
    {
      id: 4,
      image: imageTwo,
      name: "Rosa Ian",
      title: "QA Lead",
      callMobile: "098392380",
    },
  ];
const [friendDetail, setFreindDetail] = useState(friends[0]);

  return (
    <div className='container'>
      <Wrapper>
        <HomePage
          friends={friends}
          setFriendDetail={seFriendDetail}
        />
        <FriendsPage friends={friends} friendDetail={friendDetail} />
      </Wrapper>
    </div>
  );
}
```

Let's break this down into small pieces. First, let's look at calling the `useState` function:

```jsx
useState(friends[0]);
```

This initialises the state variable to `friends[0]` the first item from the friends array. Any parameter passed to `useState` will be used as the initial value.

In React, `useState` will **always** return an array with two items. The first item in the array is the current value of the `friendDetail` state. In our example it will be 0 on the first render. The second item in the array is a function that we will use to update our state.

When we destructure an array, we can name the variables whatever we want, but there is a naming convention when destructuring the `useState` array. The first variable should be named whatever your state is called, and the second variable should be the same name but prefixed with `set`

```jsx
const [friendDetail, setFreindDetail] = useState(friends[0]);

const [userIsLoggedIn, setUserIsLoggedIn] = useState(false);

const [username, setUsername] = useState("chris");

const [unreadMessages, setUnreadMessages] = useState(5);
```

### Exercise

1. Open [this CodeSandbox](https://codesandbox.io/s/using-usestate-exercise-3kwei?file=/src/Weather.js).
2. Take a few minutes to read the code. Why do you think the app is broken?
3. Initialize a new state variable with `useState` that will fix the app. Think carefully about how you should name the variables

## **Updating State**

```jsx
const FriendsListItem = ({ friends, setEmployeeDetail }) => {
  return friends.map(({ image, name, title }, index) => {
    return (
      <div
        key={index}
        style={StyleFriendsListItem}
        onClick={() => {
          setEmployeeDetail(friends[index]);
        }}
      >
        <img style={StyleImage} src={image} alt={image} />
        <div style={StyleContent}>
          <h3 style={{ margin: "0" }}>{name}</h3>
          <p style={{ margin: "0" }}>{title}</p>
        </div>
      </div>
    );
  });
};
```
