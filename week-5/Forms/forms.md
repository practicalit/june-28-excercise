# Form

## Working with forms in React

Modern web applications often involve interacting with forms such as creating an account, adding a blog post or posting a comment. This would involve using inputs, buttons and various form elements and being able to get the values entered by users to do something with it (like display them on a page or send them in a POST request). So, how do we do this in React?

### Controlled component pattern

A popular pattern for building forms and collect user data is the *controlled component* pattern. A *pattern* is a repeated solution to a problem that is useful in multiple similar cases. Let's have a look at an example

```jsx
function SimpleReminder() {
  const [employee, setEmployee] = useState("");

  function handleChange(event) {
    setReminder(event.target.value);
  }

  return (
    <form>
      <input
        type='text'
        placeholder='Some reminder'
        value={employee}
        onChange={handleChange}
      />
      <p>Today I need to remember to... {employee}</p>
    </form>
  );
}
```

We're controlling the `value` of the input by using the value from the `employee` state. This means that we can only change the value by updating the state.

It is done using the `onChange` attribute and the `handleChange` function which is called every time the input value changes (typically when a new character is added or removed).

If we didn't call `setEmployee` in the `handleChange` function, then the input's value would never change and it would appear as if you couldn't type in the input! Finally, the value we keep in the `reminder` state is displayed on the screen as today's reminder.

In addition, instead of just saving the value of the input in the state, we could have also transformed the string before we set it with `setEmployee`, for example by calling `toUpperCase()` on the string.

### Exercise

1. Open the `employee-app` React application
2. Create a new file `src/components/Form.js`
3. Inside the `Form.js` file, create a functional component
4. Inside the `return` statement create a couple of text input fields as shown below

```jsx
<form>
  <input type='text' placeholder='name' />
  <input type='text' placeholder='occupation' />
</form>
```

1. Render the `Form` component inside the `App` above the `Wrapper` component
2. Inside the `Form` component create two states called `name` and `occupation`
3. Create these two components called `handleName` and `handleOccupation`

and pass these functions to the `onChange` event handler in their corresponding `input` elements

1. Pass the parameter named `event` in each handler functions
2. Add a `console.log` to inspect the value of `event.target.value` . What happens when you type in the input?
3. Using `setName` and `setOccupation` , update the `name` and `occupation` states to what was typed in the input box.

### Form submission

So far, our form examples don't have a way of sending the user data back to the server, so that we can store it in the database.

We will be using a special `submit` event triggered on the `<form>` element. This event is triggered when the user clicks a submit button or if they hit the Enter key. Let's take a look at an exampl

```jsx
function Form() {

  ...

  function handleSubmit(event) {
    event.preventDefault();

    console.log("Sending data to server");

    fetch("https://lit-dusk-21328.herokuapp.com/api/employees/addemployees", {
      method: "POST",
      body: JSON.stringify({
        name: name,
        occupation: occupation,
        callMobile: callMobile,
        callOffice: callOffice,
        sms:sms,
        email: email,
        image: image
      }),
      headers: {
        "Content-Type": "application/json"
      }
    });
  }

  return (
    <form onSubmit={handleSubmit}>
      ...
      <button>Submit</button>
    </form>
  );
}
```

We set up our `<form>` to handle the event by passing the `handleSubmit` function to the `onSubmit` prop. If we click on the Submit button or hit Enter while focused on the form, the event is triggered and the `handleSubmit` function is called.

The first thing we do inside the handler function is call `event.preventDefault()`. This is necessary because the browser has a *default* action when the submit event is triggered on the form to send a GET request to the server. We prevent the default action because we will handle the event ourselves.

We can then do whatever we want with our user data! In this example, we're sending a POST request using the `fetch` method.
