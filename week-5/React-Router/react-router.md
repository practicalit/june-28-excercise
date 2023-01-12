# React Router

### **Introduction to React Router**

In the past few weeks, you've learned how to build applications with React, and the different applications and examples were all built on a single page. However, what if you wanted to have different pages, with each page having its own URL (so you can bookmark it, for example)? You will need to introduce a router in your application. In JavaScript, a router is the piece of code that is in charge of switching between views of your application and keeping each view in sync with a specific URL. For example, you could imagine having a homepage reachable from the root path `/`
 and a `users` page with the path `/users` . In React, a popular library to help you achieve this is [React Router.](https://reactrouter.com/en/6.6.2/start/overview#client-side-routing)

Let's look at a first example

```jsx
const Index = () => {
  return <h2>Home</h2>;
};

const About = () => {
  return <h2>About</h2>;
};

const Users = ({ names }) => {
  return (
    <div>
      <h2>Users</h2>
      <ul>
        {names.map((name, index) => (
          <li key={index}>{name}</li>
        ))}
      </ul>
    </div>
  );
};

const AppRouter = () => {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to='/'>Home</Link>
            </li>
            <li>
              <Link to='/about/'>About</Link>
            </li>
            <li>
              <Link to='/users/'>Users</Link>
            </li>
          </ul>
        </nav>
        <Routes>
          <Route path='/' element={<Index />} />
          <Route path='/about/' element={<About />} />
          <Route
            path='/users/'
            element={<Users names={["Raresh", "Nate"]} />}
          />
        </Routes>
      </div>
    </BrowserRouter>
  );
};
```

React Router provides some default React components that you can use to enable routing in your application. First, notice the top`-`level `<BrowserRouter>` component which wraps everything else. Then, the `<Routes>` component which will choose one `<Route>` based on the current path. Each route is defined with the `<Route>` component which maps a path (defined with the `path` props) to a React component. You can pass an entire component including its properties to the `element={...}` prop. Finally, the `Link` component can be used to create links to navigate to different routes.
