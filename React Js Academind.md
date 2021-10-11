# React Js Academind

## [source of learning](https://www.youtube.com/watch?v=Dorf8i6lCuk&t=1505s)

[Basic Setup](#basic-setup)

[create project](#create-project)

[run project](#run-project)

[cleaning up files](#cleaning-up-files)

[How react works & understanding components](#how-react-works--understanding-components)

[More about components & styliing with css classes](#more-about-components--styliing-with-css-classes)

[Building & reusing another component](#building--reusing-another-component)

[exports and import methods:](#exports-and-import-methods)

[Props and dynamic content](#props-and-dynamic-content)

[Handling Events](#handling-events)

[Adding more components](#adding-more-components)

[Introducing States](#introducing-states)

[Event props](#event-props)

[Adding Routing](#adding-routing)

[Adding Links & Navigation](#adding-links--navigation)

[CSS modules](#css-modules)

[Props Children](#props-children)

[Getting User Input and handling Form Submission](#getting-user-input-and-handling-form-submission)

[Preparing the App for HTTP](#preparing-the-app-for-http)

[Navigating Programmatically](#navigating-programmatically)

[Getting started with Fetching Data](#getting-started-with-fetching-data)

[UseEffect](#useeffect)

[Introducing React Context](#introducing-react-context)

# Basic Setup

## create project

- create react project with the command

```jsx
npx create-react-app <project_name>
```

## run project

- run project with the command

```jsx
1. cd <project_name>
2. npm install / yarn install
```

---

## cleaning up files

- remove all the files except of `App.js` `index.css index.js`
- remove imports and usage of remove files in remaining files

# How react works & understanding components

- HTML in javaScript is jsx code
- concept of component

# More about components & styliing with css classes

- styling can be done with `index.css` as primary file and then can be imported later on respective files
- individual files on css can be prepared and then imported respectively acc to usage as well

# Building & reusing another component

- component files are added as seperate part of code which can be reused
- all component files are kept inside `src>components` directory
- name of component file should start in uppercase letter
- creating component

  - creating and exporting component file:

  ```jsx
  function component_name() {
  	// codes here
  }

  export default component_name;
  ```

  - importing component file in App.js file:

  ```jsx
  import component_name from "<file_path>"

  function App(){
  	return(
  		<div>
  			<component_name>
  		</div>
  	)
  }
  ```

### exports and import methods:

- exporting methods:
  ```jsx
  1. exports.function_name = () ⇒ {}
  2. export default function_name;
  ```
- importing methods:
  ```jsx
  1. const name = require("<path>")
  2.  import name from "<path>"
  ```

# Props and dynamic content

- props provides the component dynamic
- to pass data in the components we use concept of props
- to use props it has to be used as parameter with the component/ function
- in the component props is then used as javaScript expression (i.e inside pair of parenthesis "{ }" )
- example:

  - passing props from `App.js` file
  - usage is highlighted with orange color

  ```jsx
  import Todo from "./components/Todo";

  function App() {
  	return (
  		<div>
  			****
  			<Todo title="title1" />
  		</div>
  	);
  }

  export default App;
  ```

  - using props inside `Todo.js` component file.
  - usage is highlighted with orange color

  ```jsx
  const Todo = (props) => {
  	return (
  		<div className="card">
  			<h1>My Tools </h1>
  			<h2>{props.title}</h2>
  			<div className="actions">
  				<button className="btn">Delete</button>
  			</div>
  		</div>
  	);
  };

  export default Todo;
  ```

# Handling Events

- event handlers are mostly used within the tag itself with dynamic expression (i.e " { }" )
- within the dynamic expression we then pass the handler functions
- note: don't use parenthesis while using handler function to the expression. It will execute it immediately. Instead use just handler function name
- example:

  - using event listener for button onclick event
  - usage is highlighted with orange color

  ```jsx
  const Todo = (props) => {
  	const handleClick = () => {
  		console.log(props.title);
  	};

  	return (
  		<div className="card">
  			<h1>My Tools </h1>
  			<h2>{props.title}</h2>
  			<div className="actions">
  				<button className="btn" onClick={handleClick}>
  					Delete
  				</button>
  			</div>
  		</div>
  	);
  };

  export default Todo;
  ```

# Adding more components

- same previous standard rules are used to add components

# Introducing States

- State is a plain JavaScript object used by React to represent an information about the component's current situation. It's managed in the component (just like any variable declared in a function).
- Because state is dynamic, it enables a component to keep track of changing information in between renders and for it to be dynamic and interactive
- using states with functional component includes:
  ### 1. importing `useStae` hook
  ```jsx
  import { useState } from "react";
  ```
  - `useState` hook always returns array with two elements they are usually destructed to use `useState` hook. The array includes:
    1. initial value
    2. modifier function
    - example:
      ```jsx
      const [name, setName] = useState("pankaj");
      ```
      - here `name` is initial value which is "pankaj" and modifying function is `setName` .
  ### 2. using `useState` hook to render components conditionally :
  - defining initial state and modifier functions:
    ```jsx
    const [isModelOpen, setisModelOpen] = useState(false);
    ```
  - to use state modifier function:
    ```jsx
    // changing isModelOpen value from false to true
    setIsModelOpen(true);
    ```
  - using conditional rendering to render modal and backdrop if `isModelOpen` state is true:
    ```jsx
    {
    	isModelOpen && <Modal />;
    }
    ```
    - the rendering method is javaScript AND which renders second element if both are true

# Event props

- event props/functions can be passed just like any other props.
- we can create a event handler in parent file and then pass it as props which can be used in respective component files

  - for `Todo.js` which is parent

    ```jsx
    // defining states
    const [isModelOpen, setIsModelOpen] = useState(false);

    // event handler function
    const handleClick = () => {
    	setIsModelOpen(true);
    };

    // passing event handler function as props to components
    {
    	isModelOpen && <Backdrop onClick={handleClick} />;
    }
    ```

  - for `Backdrop.js` file which is child component
    ```jsx
    const Backdrop = (props) => {
    	return <div className="backdrop" onClick={props.onClick} />;
    };
    ```

# Adding Routing

- we need `react-router-dom` package to use react routing
- to install run `npm install react-router-dom`
- to use:

  - in `index.js` file:

    1. import `BrowserRouter` from `react-router-dom`

       ```jsx
       import { BrowserRouter } from "react-router-dom";
       ```

    2. use to wrap `App` component

       ```jsx
       ReactDOM.render(
       	<BrowserRouter>
       		<App />
       	</BrowserRouter>,

       	document.getElementById("root")
       );
       ```

  - in `App.js` file

    1. import `Route` from `react-roter-dom`

       ```jsx
       import { Route } from "react-router-dom";
       ```

    2. use to wrap components

       ```jsx
       import { Route } from "react-router-dom";
       import AllMeetups from "./pages/AllMeetups";
       import Favorites from "./pages/Favorites";
       import NewMeetup from "./pages/NewMeetup";
       function App() {
       	return (
       		<div>
       			<Route path="/">
       				<p> this is home route </p>
       			</Route>
       			<Route path="/allmeetups">
       				<AllMeetups />
       			</Route>
       			<Route path="/new-meetup">
       				<NewMeetup />
       			</Route>
       			<Route path="/favorites">
       				<Favorites />
       			</Route>
       		</div>
       	);
       }
       ```

       - paths are setup for specific routes
       - home route will be seen for all routes coming after home routes like [`localhost:3000`](http://localhost:3000) is home route but for route [`localhost:3000/allmeetups`](http://localhost:3000/allmeetups) also includes home route elements as well since it includes home route in it's path as well
       - To solve the issue we can use switch statements in the route. On doing this only one route will be used and no nested routes will work later on

         ```jsx
         import { Route, Switch } from "react-router-dom";
         import AllMeetups from "./pages/AllMeetups";
         import Favorites from "./pages/Favorites";
         import NewMeetup from "./pages/NewMeetup";

         function App() {
         	return (
         		<div>
         			<Switch>
         				<Route path="/" exact>
         					<p> this is home route </p>
         				</Route>
         				<Route path="/allmeetups">
         					<AllMeetups />
         				</Route>
         				<Route path="/new-meetup">
         					<NewMeetup />
         				</Route>
         				<Route path="/favorites">
         					<Favorites />
         				</Route>
         			</Switch>
         		</div>
         	);
         }

         export default App;
         ```

         - exact is used to compare the exact route else it won't look for the route

# Adding Links & Navigation

- anchor tag isn't used in react since it requests to the page and then redirects to the link. Instead we want to access the items and then embed in appropriate routes
- for that we use `Link` provided by `react-router-dom` which can be imported by:
  ```jsx
  import { Link } form "react-router-dom"
  ```
- using `Link` property:

  ```jsx
  import { Link } from "react-router-dom";

  const MainNavigation = () => {
  	return (
  		<header>
  			<div>react meetups</div>
  			<ul>
  				<li>
  					<Link to="/">home</Link>
  				</li>
  				<li>
  					<Link to="/allmeetups">All meetups</Link>
  				</li>
  				<li>
  					<Link to="/newmeetup">New meetup</Link>
  				</li>
  				<li>
  					<Link to="/favorites">Favorites</Link>
  				</li>
  			</ul>
  		</header>
  	);
  };

  export default MainNavigation;
  ```

  - `to="/allmeetups"` means the route to point to which is defined by react routes

# CSS modules

- modules in css are used to define styles for specific components and import to required files to mange files properly.
- note: make sure to write css file as <file_name>.module.css for importing as module
  - example
    ```jsx
    import navClasses from "./MainNavigation.module.css";
    ```

# Props Children

- props children are those parts of code which are wrapped inside of any components which can be used by `props.children` property
- props are passed to any component by default
- example:

  ```jsx
  import Card from "./comonents/Card";

  const SampleComponent = () => {
  	<Card>
  		<div>
  			<h1> this is child of the Card component</h1>
  		</div>
  	</Card>;
  };
  ```

# Getting User Input and handling Form Submission

- `onSubmit` event handler can be used to handle user inputs
- `event.preventDefalut()` method is to prevent default behaviours of form
- we use `useRef` hook read datas of the form
- to use :

  ```jsx
  import { useRef } from "react";

  const NewMeetupForm = (props) => {
  	const titleInputRef = useRef();

  	const submitHandler = (event) => {
  		event.preventDefault();
  		const enteredTitle = titleInputRef.current.value;

  		const meetupData = {
  			title: enteredTitle,
  		};

  		console.log(meetupData);
  	};

  	return (
  		<Card>
  			<form className={classes.form} onSubmit={submitHandler}>
  				<div className={classes.control}>
  					<label htmlFor="title">Meetup Title</label>
  					<input type="text" id="title" required ref={titleInputRef} />
  				</div>
  			</form>
  		</Card>
  	);
  };

  export default NewMeetupForm;
  ```

# Preparing the App for HTTP

- create a new project and setup real time database with test mode
- it then provies the api url to do tests
- to make post request to the api after the api link we have to add our table name/ database name .json and it is firebase rule. e.g:
  ```jsx
  fetch("<api_link>.<table_name>.json");
  ```
- by default fetch method is used for get to configure it to do post request we have to do:
  ```jsx
  fetch(
  			"<api_link>/<table_name>.json",
  			{
  				method: "POST",
  				// we need to send json data only
  				body: JSON.stringify(meetUpData),
  				header: {
  					"Content-Type": "application/json",
  				},
  			}
  ```
- on successful submission of data firebase should create a database with the provided values

# Navigating Programmatically

- we use `react-router-method` called `useHistory()` for that after adding data to databases as callback
- example:
  ```jsx
  fetch().then(() => {
  	// blocks of code
  	// will navigate to homeroute
  	history.replace("/");
  });
  ```

# Getting started with Fetching Data

- we use `fetch()` method to fetch the data we posted on firebase
- [this link](https://www.youtube.com/watch?v=Dorf8i6lCuk&t=10507s) has coding tut for best learning

# UseEffect

- is used for first render only
- it prevents rerender issues
- example:

  ```jsx
  import { useEffect } from "react";

  useEffect(() => {
  	// block of code to execute
  }, [dependency_states]);
  ```

  - `dependency_states` are passed to re-render the app only when those states value are changed

# Introducing React Context

-
