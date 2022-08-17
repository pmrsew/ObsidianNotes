# Handling Forms in React
#react #forms #useref #component

## Working with uncontrolled components
- Uncontrolled component: a container created to give its current value when requested in the code
	- To manage elements outside of state
- Anytime `useRef` is used, an uncontrolled component is being created
- `useRef()`: function is used to create a reference that can be tied to an element via ref property, and returns current element
	- Must include import statement, `import { useRef } from "react";`
	- Hook that is going to reach out to an element and get its value
	- `useRef` will not rerender if there is a change (like `useState`), `.current.value` will need to be used to reach out to the current state
- A ref or reference is a way to reach out to an individual element and check in with what its value is

Below, the form created is an uncontrolled component
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


## Creating controlled form elements
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

## Building a custom hook
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

## Form Libraries
https://formik.org - help handle submitting forms
https://react-hook-form.com - help creating form requiring validation