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
