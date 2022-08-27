# Unsorted Notes
Notes from the Scrimba - Learn React Free course by Bob Ziroll

## Create React App - Easy Way:
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

## Create React App - Correct Way:
[[Creating React Application]]

### Using Vite
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


## Why use React?
- It's *composable code*: individual pieces of code (components) that build on one another to make the larger application
	- Maintainable - changes are made to only necessary components and is more easily organizable
	- Flexible - remove and add isolated components as needed
- It's *declarative*: code says what to do, the computer will decide how to do that action
	- Opposite is *imperative* meaning the code describes how an action should be done step by step
	- React reduces the amount of code written by using JSX (the HTML used inside JavaScript)

#### Declarative - JSX:
```
ReactDOM.render(<h1 className="header">Hello, everyone!</h1>, document.getElementById("root"))
```
#### Imperative - Vanilla JS:
```
const headerElement = document.createElement('h1');
headerElement.textContent = "Hello, react!";
headerElement.className = "header";
document.getElementById("root").insertAdjacentElement('beforeend', headerElement);
```

## How to make React component
1. Start by creating a function, the name of the function is the name of the component, use PascalCase
2. Have function return the html elements wanted
3. Call on the component via `render()`, synax will be similar to an HTML element
***In React 18, ReactDOM.render is not used, instead createRoot should be used. If you run React 18 with ReactDOM.render, the app will behave as if it's React 17.***

`ReactDOM.render()`
```
import React from "react"
import ReactDOM from "react-dom"

function MainContent(){
    return(
        <h1>I'm learning React!</h1>
    );
}

ReactDOM.render(
	
	<MainContent />,
	document.getElementById("root")
)
```
`ReactDOM.createRoot()`
```
import React from "react"
import ReactDOM from "react-dom/client"

function MainContent(){
    return(
        <h1>I'm learning React!</h1>
    );
}

const root = ReactDOM.createRoot(doucment.getElementById("root"))
root.render(<MainContent/>)
```

## JSX - Javascript XML
- Flavor of Javascript that looks like HTML
- Some syntax is different from HTML:
	- use `className` property instead of `class` when coding with React
- Functions that return objects React can understand, turn to elements, and communicate to the DOM
- Only return a single element -- many elements can be returned, but only if they are all under the same, single parent element
- Pre-React v17, `import React from "react"` was required to interpret JSX; with v17, you no longer need to import

```
// Vanilla JavaScript:
const h1 = document.createElement("h1")
h1.textContent = "Hello world"
h1.className = "header"
console.log(h1)

// returns <h1 class="header">

// JSX
const element = <h1 className="header">This is JSX</h1>
console.log(element)

/*
	Returns:
	{
		type: "h1",
		key: null,
		ref: null,
		props: {
			className: "header",
			children: "This is JSX"
		},
		_owner: null,
		_store: {}
	}
*/
```

- To insert Javascript into JSX, use curly braces(`{}`) to create JSX expression:

Using JS Variables:
```
function App() {
	const firstName = "Joe"
	const lastName = "Schmoe"

	return (
		<h1>Hello, {firstName} {lastName}!</h1> // Hello, Joe Schmoe!
	)
}
```
Using JS Functions:
```
function App() {
	return (
		<h1>It is currently about {new Date().getHours() % 12} o'clock!</h1>
	)
	//It is currently about 3 o'clock!
}
```

## Deploy React App with Netlify
1. `npm install`
2. `npm run build`
3. When using Vite, final build files will be in the folder `/dist`
4. Upload that file to Netlify

```
Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects/react-site (main)
$ npm install

up to date, audited 87 packages in 806ms

8 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

Paige@Lenovo MINGW64 ~/Documents/Code/code_playground/Tutorials/Scrimba_LearnReactFree_Projects/react-site (main)
$ npm run build

> react-site@0.0.0 build
> vite build

vite v3.0.9 building for production...
✓ 35 modules transformed.
dist/assets/reactjs-icon-bg.cd027592.png   6.94 KiB
dist/index.html                            0.71 KiB
dist/assets/index.0c353fd1.css             0.75 KiB / gzip: 0.41 KiB    
dist/assets/index.a06e789f.js              141.96 KiB / gzip: 46.63 KiB 
```

## Props
- Props make components more resuable (only used by React components, custom props won't work with native DOM elements (lowercase elements))
- Properties are assigned to React componenets when they are called to be rendered
	- Strings can be used by wrapping quotes
	- For non-strings, wrap in curly braces
- Use `props` object to pass attributes (properties) into a component
- Use properties inside component with the following syntax: `props.[defined property name]`

App.js
```
function App(){
	return (
		<Contact
			img="./images/mr-whiskerson.png"
			name="Mr. Whiskerson"
			phone="(212) 555-1234"
			email="mr.whiskaz@catnap.meow"
			age={3}
		/>
	)
}
```
Contact.js
```
export default function Contact(props) {
	return (
		<div className="contact-card">
			<img src={props.img}/>
			<h3>{props.name}</h3>
			<p>{props.phone}</p>
			<p>{props.email}</p>
			<p>{props.age}
		</div>
	)
}
```
Contact.js using DESTRUCTURING
```
export default function Contact({img,name,phone,email}) {
	return (
		<div className="contact-card">
			<img src={img}/>
			<h3>{name}</h3>
			<p>{phone}</p>
			<p>{email}</p>
		</div>
	)
}
```
*Conditional Rendering* example using `&&` to only display Dom element if prop exisits:
```
export default function Joke(props) {
	return (
	<div>
		{props.setup && <h3>Setup: {props.setup}</h3>}
		<p>Punchline: {props.punchline}</p>
		<hr />
	</div>
	)
}
```

## React and Arrays
1. What does the `.map()` array method do?
Returns a new array. Whatever gets returned from the callback
function provided is placed at the same index in the new array.
Usually we take the items from the original array and modify them
in some way.
2. What do we usually use `.map()` for in React?
Convert an array of raw data into an array of JSX elements
that can be displayed on the page.
3. Why is using `.map()` better than just creating the components
   manually by typing them out?
It makes our code more "self-sustaining" - not requiring
additional changes whenever the data changes.

```
const colors = [
	<h3>Red</h3>,
	<h3>Orange</h3>,
	<h3>Yellow</h3>,
	<h3>Green</h3>,
	<h3>Blue</h3>,
	<h3>Indigo</h3>,
	<h3>Violet</h3>
]

return (
	<div>
		{colors}
	</div>
)
```

```
import jokesData from "./jokesData"

export default function App() {
	const jokeElements = jokesData.map(joke => {
		return <Joke setup={joke.setup} punchline={joke.punchline} />
	})
	return (
	<div>
		{jokeElements}
	</div>
	)
}
```

## Forms and Inputs
- Adding event listeners ([React Mouse Event Properties](https://reactjs.org/docs/events.html#mouse-events))
```
export default function App() {
	function handleClick() {
		console.log("I was clicked!")
	}
	
	function handleHover(){
		console.log("I was hoovered!")
	}
	
	return (
		<div className="container">
			<img onMouseOver={handleHover} src="https://picsum.photos/640/360" />
			<button onClick={()=>handleClick()}>Click me</button>
		</div>
	)
}
```

