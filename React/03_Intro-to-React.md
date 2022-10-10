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
