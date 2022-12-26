# Deploy a React App into GitHub Pages

- Create a repo in your GitHub account. Use the name of the app you want to deploy, e.g., `my-app`
- `create-react-app` takes care of initializing our react app with git (we don’t need to worry about it here.)
- in your terminal. Use the `git remote add origin [https://github.com/<username>/my-app](https://github.com/<username>/my-app)` command to connect your app with your remote GitHub repo.
- Next, run `git push - origin master` to push your code into the GitHub repo.
- Open the `package.json` file on your code editor and add `"homepage": "https://<username>.github.io/my-app"`
- Install `gh-pages` and add `deploy` to `scripts` in the `package.json` file
  - `npm install --save gh-pages`
  - or `yarn add ph-pages`
- add the following scripts in your `package.json` file
  ```jsx
  "scripts": {
  +   "predeploy": "npm run build",
  +   "deploy": "gh-pages -d build",
      "start": "react-scripts start",
      "build": "react-scripts build",
  }
  ```
  The `predeploy` script will run automatically before `deploy` run
- Deploy the site by running `npm run deploy`
