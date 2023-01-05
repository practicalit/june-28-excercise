# Fetching data in React

Often when you create a React app, you will want to fetch data from an API and display it inside your components. How do we do this in React?

You might think that we could just fetch the data in the component like this, but unfortunately, it **won't work**

```jsx
function PhotoFetcher() {
  let imgSrc = null;

  fetch(
    `https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=2015-6-3&api_key=DEMO_KEY`
  )
    .then((res) => res.json())
    .then((data) => {
      imgSrc = data.photos[0].img_src;
    });

  console.log(`The image src is ${imgSrc}`);
  return <img src={imgSrc} />;
}
```

This is because React is synchronous, while `fetch` is asynchronous. If we look in the console, we'll see that the `imgSrc` will always be `null` when we try to render it. React will try to render before `fetch` has had time to get the data from the API.

We need a way of running the `fetch` call **after** we have rendered for the first time, so that it is not *racing* against React updating the DOM. Then once we have got the data back we can use state to tell React to re-render with the new data.

The way we do this is with another Hook provided by React. This one is called `useEffect`
.

## **Importing `useEffect`**

```jsx
import React, { useEffect } from "react";

console.log(useEffect);
```

If we look in the console, we'll see that `useEffect` is also a function like `useState`.

Often, we will need to use `useState` and `useEffect` together. They are imported together like this:

```jsx
import React, { useState, useEffect } from "react";
```

## **Using `useEffect`**

Now let's look at how to use the `useEffect` Hook

```jsx
function PhotoFetcher() {
  useEffect(() => {
    fetch(
      `https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=2015-6-3&api_key=DEMO_KEY`
    )
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
      });
  }, []); // Always remember to put an empty array here!

  return <div>Hello useEffect!</div>;
}
```

The `useEffect` Hook takes two arguments:

1. A callback function, where we can put our `fetch` call. In this example, we're fetching some data from the NASA API! 🚀
2. An array, which we'll look at later but is very important that you don't forget it!

**NOTE**

When writing your `useEffect`, write the "skeleton" first, then fill in the callback function later.

```jsx
*// Write this bit first!*
useEffect(() => {
 *// Write this bit later!*
}, []);
```

You might have noticed that we still haven't rendered the data from the API. We now need to tell React to re-render once we get the data. This sounds like a job for state!

Let's look an example of how we can use state and `useEffect` to do this

```jsx
function PhotoFetcher() {
  const [marsPhotoData, setMarsPhotoData] = useState(null);

  useEffect(() => {
    console.log("Fetching data from NASA");

    fetch(
      `https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=2015-6-3&api_key=DEMO_KEY`
    )
      .then((res) => res.json())
      .then((data) => {
        setMarsPhotoData(data);
      });
  }, []);

  if (marsPhotoData) {
    return <img src={marsPhotoData.photos[0].img_src} alt='Martian surface' />;
  } else {
    return null;
  }
}
```

The timeline of this component is now what we wanted at the start:

1. The component renders for the first time. Notice that we are returning `null` here: if a component returns `null`, then React will render nothing on-screen
2. After rendering, the `useEffect` callback is run, so it fetches data from the NASA API
3. When the response is received, we update the state
4. This causes a re-render so that we can show the data on-screen

You might notice that even though we re-rendered, we did **not** run the `useEffect` a second time. The way we've set it up, `useEffect` will only run after the **first** time a component renders. We'll look at controlling this in more detail later.

## Exercise:

You should complete the following steps:

1. Open the `employee-app` React application again.
2. Open the `App.js` and remove or comment out the `employees` array
3. Create a new state variable called `employees` and initialise it to `null`.

   Refer [here](https://github.com/practicalit/june-28-excercise/blob/master/week-4/State/state-managment.md) if you get stuck (hint: `const [employees, setEmployees] = useState(null)`)

4. Now add a `useEffect` call, but leave the callback function empty for now. **Make sure you remember to add the empty array after the callback function**.
5. Inside the `useEffect` callback, call the `fetch` function with this URL:

   [`https://lit-dusk-21328.herokuapp.com/api/employees/allemployees`](https://lit-dusk-21328.herokuapp.com/api/employees/allemployees)

6. Add a `.then` handler into the `fetch` function (remember this needs to come immediately after the `fetch` call) which converts the response from JSON (hint: `.then(res => res.json())`).
7. Add a second `.then` handler after the one we just added, where the callback function will receive an argument called `data`.
8. Within the second `.then` callback function, log out the data that we just received (hint: `console.log(data)`). Inspect the data in the dev tools console. Is there any interesting data? (Hint: think about what the component is trying to render).
9. Still within the second `.then` callback, set the `pokemonData` state to be the `data` object we received from the API.
