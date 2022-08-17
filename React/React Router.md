# React Router
#react #router

## Installing React Router v6
After creating the React application, you need to install React Router:
```
$ npm install react-router-dom@6
```

## Configuring the Router
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

## Incorporating the Link component
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

## Nesting links with React Router v6
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