# Destructuring arrays and objects
#react #destructuring

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