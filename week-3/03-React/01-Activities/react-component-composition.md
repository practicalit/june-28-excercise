# React Component Composition

In React, we can make components more generic by accepting `props`, which are to React components what parameters are to functions.

Component composition is the name for **********************************\*\*\*\***********************************passing components as props to other components,**********************************\*\*\*\*********************************** thus creating new components with other components.

### How can composition help performance?

Composition is also a great ally if you try to reduce the number of re-renders in your application.

[https://lucid.app/lucidchart/e1f1cf0d-af5f-4adc-9a02-c82a673550e5/edit?viewport_loc=313%2C55%2C939%2C1107%2C-V_hJxkKSEro&invitationId=inv_baba496a-8da6-4eaf-8d7f-d7350381531e](https://lucid.app/lucidchart/e1f1cf0d-af5f-4adc-9a02-c82a673550e5/edit?viewport_loc=313%2C55%2C939%2C1107%2C-V_hJxkKSEro&invitationId=inv_baba496a-8da6-4eaf-8d7f-d7350381531e)

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
