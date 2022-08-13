# Unsorted Notes

Notes below are from LIL - React.js Essential Training - Eve Porcello
## React State in the Component Tree
### Destructuring arrays and objects
- Destruturing is a simple property that is used to make code clearly readable when passing props
- Destructuring objects: takes out a section of the object and assigns them to new variables

Using props object:
```
function App(props) {
  return (
    <div className="App">
      <h1>Hello from {props.library}</h1>
    </div>
  );
}
```

Using destructuring:
```
function App({library}) {
  return (
    <div className="App">
      <h1>Hello from {library}</h1>
    </div>
  );
}
```

- Destructuring arrays: assigning a variable name based on a position in the array

```
const cities = ["Tokyo", "Tahoe City", "Bend"];
console.log(cities[0]); //returns Tokyo
```

```
const [firstCity, secondCity] = ["Tokyo", "Tahoe City", "Bend"];

console.log(firstCity); //returns Tokyo
console.log(secondCity); //returns Tahoe City
```

### Understanding the `useState` Hook
- Managing state is done through destructuring and using a hook called `useState`
- `useState()`: takes in an initial state value when site is first rendered and returns an array that includes two items: initial state value and a function
	- Must include import statement to use (`import {useState} from "react";`)
	- Destructuring the array returned is what makes this function most useful
	- State value can be string, boolean, object or array

```
import {useState} from "react";

function App() {
  const [emotion, setEmotion] = useState("happy");

  return (
    <div className="App">
      <h1>Current emotion is {emotion}</h1>
      <button onClick={() => setEmotion("sad")}>Sad</button>
      <button onClick={() => setEmotion("excited")}>Excited</button>
    </div>
  );
}
```

1. Import `useState` function
2. Use destructuing to create variables holding state value and function to update state value
3. `emotion` can be called on to display
4. `setEmotion()` can be called on when buttons are used to update the current state value `emotion`

### Working with `useEffect` Hook
- `useEffect` is a hook that is typically used to manage side effects (actions that happen alongside render) that aren't related to a components render (console messages, loading data, animations can benefit from this hook)
- `useEffect()`: takes in two arguements, a function that is going to be called whenever we want effect to happen and a dependency array that defines when the effect is called
	- Must include import statement to use (`import {useEffect} from "react";`)
	- Effect will always occur on initial render
	- Passing in no dependency array means effect will occur if any state value change occurs
	- Passing in an empty dependency array means the effect won't occur after initial render
	- Can pass in state values to listen to any changes made to them

Example 1: Passing in `[emotion]` as the dependency array means that each time the `emotion` state value is changed by pressing a button, the console prints the current emotion.
```
import { useState, useEffect } from "react";

function App() {
  const [emotion, setEmotion] = useState("happy");

  useEffect(() => {
    console.log(`It's ${emotion} right now`);
	}, [emotion]);

  return (
	  <div className="App">
		<h1>Current emotion is {emotion}</h1>
		<button onClick={() => setEmotion("sad")}>Sad</button>
		<button onClick={() => setEmotion("excited")}>Excited</button>
	</div>
  );
}
```
 Example 2: Passing in `[emotion, secondary]` as the dependency array means that each time the `emotion` ***or*** `secondary` state values are changed by pressing a button, the console prints the current primary emotion. A second `useEffect` is used to print the secondary emotion to the console when that state value is changed.
 In sum, one effect occurs when changing `emotion`, two effects occur when change `secondary`.
 ```
import { useState, useEffect } from "react";

function App() {

  const [emotion, setEmotion] = useState("happy");
  const [secondary, setSecondary] = useState("tired");

  useEffect(() => {
    console.log(`It's ${emotion} around here!`);
    }, [emotion, secondary]);

  useEffect(() => {
    console.log(`It's ${secondary} around here!`);
    }, [secondary]);

  return (
    <div className="App">
      <h1>Current emotion is {emotion}</h1>
      <button onClick={() => setEmotion("sad")}>Sad</button>
      <button onClick={() => setEmotion("excited")}>Excited</button>

      <h2>Current secondary emotion is {secondary}</h2>
      <button onClick={() => setSecondary("grateful")}>Grateful</button>
    </div>
  );
}
```

### Incorporating `useReducer` Hook
- `useReducer()`: takes in two arguments, the function that is going to be used to update state value and the initial state value
	- Must include import statement to use, `import { useState } from "react";`
	- Helps prevent bugs by pulling logic code out from the return value
	- Function used to update state value will have the same logic eachtime it's called *guarenteed*

Below are two sets of code that functionally do the same thing, however, by using `useReducer`, the logic being passed into setChecked in the first set can instead be separated and applied to setChecked.

```
import { useState } from "react";

function App() {
  const[checked, setChecked] = useState(false);

  return (
    <div className="App">
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked((checked) => !checked)} 
      />
      <label>{checked ? "checked":"not checked"}</label>
    </div>
  );
}
```

```
import { useReducer } from "react";

function App() {
  const[checked, setChecked] = useReducer(checked => !checked, false);

  return (
    <div className="App">
      <input
        type="checkbox"
        value={checked}
        onChange={setChecked}
      />
      <label>{checked ? "checked":"not checked"}</label>
    </div>
  );
}
```

## Handling Forms in React
### Working with uncontrolled components
- Uncontrolled component: a container created to give its current value when requested in the code
	- To manage elements outside of state
- Anytime `useRef` is used, an uncontrolled component is being created
- `useRef()`: function is used to create a reference that can be tied to an element via ref property, and returns current element
	- Must include import statement, `import { useRef } from "react";`
	- Hook that is going to reach out to an element and get its value
	- `useRef` will not rerender if there is a change (like `useState`), `.current.value` will need to be used to reach out to the current state
- A ref or reference is a way to reach out to an individual element and check in with what its value is

Below, the form created is an uncontrolled component.
```
import { useRef } from "react";  

function App() {
  const txtTitle = useRef();
  const hexColor = useRef();

  console.log(txtTitle);

  const submit = (e) => {
    e.preventDefault();
    const title = txtTitle.current.value;
    const color = hexColor.current.value;
    alert(`${title}, ${color}`);
    txtTitle.current.value="";
    hexColor.current.value="";
  };

  return (
    <form onSubmit={submit}>
      <input
        ref={txtTitle}
        type="text"
        placeholder="color title..."
      />
      <input ref={hexColor} type="color"/>
      <button>ADD</button>
    </form>
  );
}
```


### Creating controlled form elements
- Whenever state value is being used with a form, it is a controlled component
- Controlled Component: controlling form by creating state values for elements

Below, form element is a controlled component
```
import { useState } from "react";

function App() {
  const [title, setTitle] = useState("");
  const [color, setColor] = useState("#000000");

  const submit = (e) => {
    e.preventDefault();
    alert(`${title}, ${color}`);
    setTitle("");
    setColor("#000000");
  };

  return (
    <form onSubmit={submit}>
      <input
        value={title}
        onChange={(event) => setTitle(event.target.value)}
        type="text"
        placeholder="color title..."
      />
      <input
        value={color}
        type="color"
        onChange={(event) => setColor(event.target.value)}
      />
      <button>ADD</button>
    </form>
  );
}
```

### Building a custom hook
- If there is repeatable behavior, it can likely be replaced by a custom hook
- Custom Hook:
	- Must always begin with 'use' keyword
	- Can take in parameters
	- Can have any return


From the previous two examples, this code still has the same form functionality, however, now a custom hook is used  to reduce replicable code.
```
import { useState } from "react";

function useInput(initialValue){
  const [value, setValue] = useState(initialValue);
  return [
    {value, onChange: e => setValue(e.target.value)},
    () => setValue(initialValue)
  ]
}

function App() {
  const [titleProps, resetTitle] = useInput("");
  const [colorProps, resetColor] = useInput("#000000");

  const submit = (e) => {
    e.preventDefault();
    alert(`${titleProps.value}, ${colorProps.value}`);
    resetTitle();
    resetColor();
  };

  return (
    <form onSubmit={submit}>
      <input
        {...titleProps}
        type="text"
        placeholder="color title..."
      />
      <input
        {...colorProps}
        type="color"
      />
      <button>ADD</button>
    </form>
  );
}
```

### Form Libraries
https://formik.org - help handle submitting forms
https://react-hook-form.com - help creating form requiring validation

https://usehooks.com - guides to follow when creating custom hooks

## Asynchronous React
### Fetching data with Hooks and Displaying data from an API
Steps to fetch data from external API:
1. fetch data using both `useState()` and `useEffect()` in combination
2. pass properties from object generated by JSON to component
3. pull from the data points needed so that data is displayed

```
import { useState, useEffect } from "react";

//STEP 3
function GithubUser({name, location, avatar}){
  return (
    <div>
      <h1>{name}</h1>
      <p>{location}</p>
      <img src={avatar} height={150} alt="Github user's, pmrsew, avatar"/>
    </div>
  );
}

function App() {
  //STEP 1
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(`https://api.github.com/users/pmrsew`)
      .then((response) => response.json())
      .then(setData);
  }, []);

  //STEP 2
  if (data) return (
    <GithubUser name={data.name} location={data.location} avatar={data.avatar_url} />
  );

  return <h1>Data</h1>;
}
```

Step One in more detail:
```
//useState to handle data
//useEffect to call for external data
import { useState, useEffect } from "react";

function App() {
  //create data container and function to set the data
  const[data, setData] = useState(null);

  useEffect(() => {
    //fetch() is built in and supported by browser
    //provides a way to make an HTTP request for data
    //once data is fetched, take response and turn it into JSON
    //once data is turned into Json, set it to data container
    fetch(`https://api.github.com/users/pmrsew`).then((response) => response.json()).then(setData);
  }, []) //empty array so api is only called on ONCE

  //check for data and return if exists using pre tag
  //pre tag is a preformatted tag for JSON
  if(data) return (<pre>{JSON.stringify(data, null,2)}</pre>);

  //return if no data is found
  return (
    <h1>Data</h1>
  );
}
```

### Handling loading states
- When fetching data from external API, possible states it can be in include:
	- Loading state, fetching but not back yet
	- Success state, data has been fetched from api
	- Error state, data couldn't load
- States can be handled with `useState()`
- If an asynchronous request is being made, loading needs to be handled
```
import { useState, useEffect } from "react";

function GithubUser({ name, location, avatar }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{location}</p>
      <img src={avatar} height={150} alt={name} />
    </div>
  );
}

function App() {
  const [data, setData] = useState(null);

  //handling state of API data
  const[error, setError] = useState(null);
  const[loading, setLoading] = useState(null);
  
  //handle loading at beginning and end of fetch
  //.catch can be used to catch errors within the chain
  useEffect(() => {
    setLoading(true);
    fetch(`https://api.github.com/users/moonhighway`)
      .then((response) => response.json())
      .then(setData)
      .then(() => setLoading(false))
      .catch(setError);
  }, []);

  //what webpage is displaying based on state of data
  if(loading) return <h1>Loading...</h1>;
  if(error) return <pre>{JSON.stringify(error)}</pre>;
  if(!data) return null;

  return (
    <GithubUser
      name={data.name}
      location={data.location}
      avatar={data.avatar_url}
    />
  );
}
```

### Fetching data with GraphQL
- GraphQL: a way of creating an API where you can specify what data you want by using its field

```
import { useState, useEffect } from "react";

//query body used in request
const query = `
query{
  allLifts{
    name
    elevationGain
    status
  }
}
`; 

//request options and body
const opts = {
  method: "POST",
  headers: {"Content-Type":"application/json"},
  body: JSON.stringify({query})
};

//function creates lift component for each row of data retrieved
function Lift({ name, elevationGain, status }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{elevationGain} {status}</p>
    </div>
  );
}

function App() {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(false);

  //website goes to a GraphQL Playground used to send requests for data
  useEffect(() => {
    setLoading(true);
    //pass into fetch() address AND request
    fetch(
      `https://snowtooth.moonhighway.com`,
      opts
    )
      .then((response) => response.json())
      .then(setData)
      .then(() => setLoading(false))
      .catch(setError);
  }, []);

  if (loading) return <h1>Loading...</h1>;
  if (error)
    return <pre>{JSON.stringify(error)}</pre>;
  if (!data) return null;

  //iterate over data and create Lift components with passed in properties
  return (
    <div>
      {data.data.allLifts.map((lift) => (
        <Lift
          name={lift.name}
          elevationGain={lift.elevationGain}
          status={lift.status}
        />
      ))}
    </div>
  );
}
```

### Working with render props
- A way to display data while handling data loading
```
//array of data to display
const tahoe_peaks = [
  {name: "Freel", elevation: 10891},
  {name: "Monument", elevation: 10067},
  {name: "Pyramid", elevation: 9983},
  {name: "Tallac", elevation: 9735}
];

//function that takes in:
//  data array
//  function to help render an individual list item
//  what will be displayed if array is empty
//returns data as unordered list unless empty
function List({data, renderItem, renderEmpty}){
  return !data.length ? renderEmpty:(
    <ul>
      {data.map((item) => (
        <li key={item.name}>{renderItem(item)}</li>
      ))}
    </ul>
  );
}

function App() {
  //calling on List function and passing in required arguments
  return (
    <List
      data={tahoe_peaks}
      renderEmpty={<p>This list is empty</p>}
      renderItem={(item) => (
        <>
          {item.name} - {item.elevation} ft.
        </>
      )}
    />
  );
}
```

## React Router
### Installing React Router v6

After creating the React application, you need to install React Router:
```
$ npm install react-router-dom@6
```

### Configuring the Router

Done in `index.js` after page comonents are created:
- Import needed compontents to display
- Import needed compontents from `react-router-dom`
- Using `render()`, add `BrowserRouter` and nested `Routes` components
- Inside the `Routes` component, add individual `Route` components for each page
```
import { App, About, Contact} from "./App";
import { BrowserRouter, Routes, Route } from "react-router-dom";

ReactDOM.render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />}/>
      <Route path="/about" element={<About />}/>
      <Route path="/contact" element={<Contact />}/>
    </Routes>
  </BrowserRouter>,
  document.getElementById("root")
);
```

### Incorporating the Link component
- Must import `Link` component using import statment (`import {Link} from "react-router-dom";`)
- Use `Link` component to display links to other pages
```
import {Link} from "react-router-dom";

function Home() {
  return (
    <div>
      <nav>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>
      <h1>My Website</h1>
    </div>
  );
}
```

### Nesting links with React Router v6
- `Routes` can be used to display a component under another via nesting a `Route` component inside another
	- NOTE: make sure to omit a slash in the path
- After creating the nested `Route`, use an `Outlet` component in the component code for the parent `Route` element
- Nested `Route` configurations are powerful because page hierarchies can be created

#### `index.js`
```
ReactDOM.render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />} />
      <Route path="/about" element={<About />}>
        <Route
          path="history"
          element={<History />}
        />
      </Route>
      <Route path="/contact" element={<Contact />}/>
    </Routes>
  </BrowserRouter>,
  document.getElementById("root")

);
```
#### `app.js`
```
export function About() {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>
      <h1>About Us</h1>
      <Outlet/>
    </div>
  );
}

export function History(){
  return(
    <div>
      <h1>Our History</h1>
    </div>
  );
}
```