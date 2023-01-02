So far, we have only looked at React apps that are "static": they don't respond to user input. This week we will look at making our apps *dynamic.*

## **Recap: First-class functions in JavaScript**

Before we look more at React, we need to recap a concept in JavaScript. You may remember that functions in JavaScript are "first class" - that means we can pass a *reference*
 to a function (as a variable) and then call it elsewhere. Let's look at an example.

```jsx
function hello() {
  return "Hello!";
}

console.log(hello); // Logs: "ƒ hello() {}"
console.log(hello()); // Logs: "Hello!"
```

In the example above `hello` is a **reference** to a function. In the first `console.log` we log out the whole function. The function is **not called** until we use parentheses `()`, so we only log the string `"Hello!"` in the second `console.log`.

This is a really important and useful in React, as we can make a function and pass it to React so that it can call it when a user interacts with our app.

## **Event handlers in component**

In previous lessons we learned how to attach event listeners with `addEventListener`

```jsx
// Create an event handler
function logWhenClicked() {
  console.log("buttonElement was clicked!");
}

// Listen for events and call the event handler when triggered
buttonElement.addEventListener("click", logWhenClicked);
```

We still need to listen to events in React, but event handlers are set up in a slightly different way.

```jsx
const EmployeeListItem = () => {
  const handleEmployeeDetail = () => {
    console.log("Employee was clicked!");
  };

  return <div onClick={handleEmployeeDetial}>...</div>;
};
```

Every element in React has some special props that start with `on`
 that can be assigned to a function that will be called when the event is triggered.

Here's a few examples (a full list is available [here](https://reactjs.org/docs/events.html#reference)):

- `onClick` - the element was clicked
- `onCopy` - the clipboard is used to copy some text
- `onKeyDown` - a key is pressed down
- `onBlur` - the element loses "focus"
- `onChange` - only available for `<input>` & `<select>` (and a few others), triggered when changed
- `onDoubleClick` - the element was double-clicked!
- `onPlay` - a video starts playing
- `onSubmit` - a form element is submitted

Notice that just like with `addEventListener`
 above, we pass the function **reference** to `onClick` instead of **calling** the function. If we call the function, it will run the function when we render, not when the user clicks on the button. (Remember that *rendering* is the term in React for inserting into the DOM).

## Exercise

You should then complete the following steps:

1. Open the `employee-app` React application and open the `EmployeeListItem.js` file.
2. Add a function named `handleEmployeeDetail` within the `EmployeeListItem.js` component. (Hint: look at the example above).
3. In the `handleEmployeeDetail` function, `console.log` a message (it doesn't matter what the message is).
4. Add an `onClick` handler to the wrapper `<div>` that will call `handeEmployeeDetail`. (Hint: look at the example above).
5. In your web browser, try clicking on an employee. What do you see in the JavaScript console?
6. Take a screenshot and post it on the `june-27-class` channel.
