# React Component Composition

In React, we can make components more generic by accepting `props`, which are to React components what parameters are to functions.

Component composition is the name for passing components as props to other components, thus creating new components with other components.

### How can composition help performance?

Composition is also a great ally if you try to reduce the number of re-renders in your application.
![Employee Component Composition](/week-3/03-React/01-Activities/employee-component-flow-chart.png)

```jsx
<App/>
	<HomePage/>
		<Header/>
		<SearchBar/>
		<EmployeeList/>
			<EmployeeListItem/>
	<EmployeePage/>
		<Header/>
		<EmployeeDetail/>
```

Step 1. `import` `HomePage` and `EmployeePage` components into `App` component and render them on the browser.

Step 2. `import` `Header`, `SearchBar`, and `EmployeeList` inside the `HomePage` component and render them on the browser

Step 3. `import` the `EmployeeListItem` component into the `EmployeeList` component

Step 4. `import` the `Header` and `EmployeeDetail` components into `EmployeePage` components and take a screenshot of what is rendered on the browser
