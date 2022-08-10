# Creating React Application

## Use terminal to generate React application

1. Check for installations of Node.js and NPM
2. Use `npx create-react-app [enter folder name]` to create an app under the name provided
3. Will need to agree to installing packages (React, React-DOM, and React-Scripts)
4. Navigate to the newly created app folder and use `npm start`
5. App will open automatically in web browser

```
Paige@Lenovo MINGW64 ~/Documents/Code/OnlineCourses/LinkedIn Learning/React Essential Training/Exercise Files/Ch04/04_01/start
$ node -v
v16.14.2

Paige@Lenovo MINGW64 ~/Documents/Code/OnlineCourses/LinkedIn Learning/React Essential Training/Exercise Files/Ch04/04_01/start
$ npm -v
8.5.0

Paige@Lenovo MINGW64 ~/Documents/Code/OnlineCourses/LinkedIn Learning/React Essential Training/Exercise Files/Ch04/04_01/start
$ npx create-react-app react-app
Need to install the following packages:
  create-react-app
Ok to proceed? (y) y
npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.

Creating a new React app in C:\Users\aweso\Documents\Code\OnlineCourses\LinkedIn Learning\React Essential Training\Exercise Files\Ch04\04_01\start\react-app.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...


added 1395 packages in 36s

205 packages are looking for funding
  run `npm fund` for details

Initialized a git repository.

Installing template dependencies using npm...

added 48 packages in 5s

205 packages are looking for funding
  run `npm fund` for details
Removing template package using npm...


removed 1 package, and audited 1443 packages in 2s

205 packages are looking for funding
  run `npm fund` for details

6 high severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.

Created git commit.

Success! Created react-app at C:\Users\aweso\Documents\Code\OnlineCourses\LinkedIn Learning\React Essential Training\Exercise Files\Ch04\04_01\start\react-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd react-app
  npm start

Happy hacking!

Paige@Lenovo MINGW64 ~/Documents/Code/OnlineCourses/LinkedIn Learning/React Essential Training/Exercise Files/Ch04/04_01/start
$ cd react-app/
$ npm start

Compiled successfully!

You can now view react-app in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.1.14:3000

Note that the development build is not optimized.
To create a production build, use npm run build.

webpack compiled successfully
```
## Notes on Files Generated
### `package.json`
```
"dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.3.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
}
```

`react`: Provides everything we need to create React components
`react-dom`: Provides ability to add components to the webpage
`react-scripts`: Handles bundling

### `src/index.js`
- Entry point to application where JavaScript will be rendered
- `<React.StrictMode>`: Used to wrap the main app component and highlight any potential problems via activating additional checks, *this is only for running in development*
- Components are typically located in their own files (see `src/app.js` below)

### `public/index.html`
- Contains the root element where JavaScript is injected from file above

### `src/app.js`
- Contains App() function and exports it as the default
- As changes are made and saved, the browser will update accordingly
- Style is imported from `src/app.css`