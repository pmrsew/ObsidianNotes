# Creating React Application

## **create-react-app**

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

### Notes on Files Generated
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

---

## **Using Vite**

Why use Vite?
- Transpile - compilation phase that translates javascript
- Bundling - uses esbuild to build site quickly

How to use:
1. Check for Node.js
2. Check for NPM
3. `npm create vite@latest`
4. Enter project name
5. Select framework
6. Select framework variant
7. `cd [project-name]`
8. `npm install`
9. `npm run dev`

```

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects (main)
$ node -v
v16.14.2

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects (main)
$ npm -v
8.5.0

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects (main)
$ npm create vite@latest
Need to install the following packages:
  create-vite@latest
Ok to proceed? (y) y
√ Project name: ... react-site
√ Select a framework: » react
√ Select a variant: » react

Scaffolding project in C:\Users\aweso\Documents\Code\code_playground\Tutorials\Scrimba_LearnReactFree_Projects\react-site...

Done. Now run:

  cd react-site
  npm install
  npm run dev


Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects (main)
$ cd react-site

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects/react-site (main)
$ npm install

added 86 packages, and audited 87 packages in 7s  

8 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects/react-site (main)
$ npm run dev

> react-site@0.0.0 dev
> vite


  VITE v3.0.9  ready in 3936 ms

  ➜  Local:   http://127.0.0.1:5173/
  ➜  Network: use --host to expose

```


---

## **Quick Start with React.js**

- Add information to the `head` element that accesses the libraries needed (CDNs)
- Add Babel and configure the `script` element
- Add a `div` with ID 'root' to the `body` element

**`index.html`:**
```
<html>
	<head>
		<link rel="stylesheet" href="index.css">
		<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
		<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
		<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
	</head>
	<body>
		<div id="root"></div>
		<script src="index.js" type="text/babel"></script>
	</body>
</html>
```
**`index.css`**:
```
ReactDOM.render(<h1>Hello, everyone!</h1>, document.getElementById("root"))
```
