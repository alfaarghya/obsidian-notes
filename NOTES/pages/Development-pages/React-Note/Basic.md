
## How to create a react app ???

1. Open CLI (on where u want to create a REACT-app)
2. then Run this command

```bash
 npm create vite@latest
```

1. Then Select Option as u want
2. then go to that newly created directory through terminal and install all dependency 
```bash
npm install
```

1. now finally to start this app
```bash
npm run dev
```


at last this page will come
![Screenshot 2023-12-21 215733.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/Screenshot_2023-12-21_215733.png)


---

## Lets understand File structure

![s2.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/s2.png)

1. `public` folder is contain some elements which we want to make publicly avaliable 
2. `src` folder contains our all code, JSX code, JSX components, Style sheets etc.
3. `index.html` our actual page
4. `main.jsx` this file contains app component only. it is the gateway for html file.
5. `components` in this folder we are going to put our all JSX components.
6. `style` in this folder we are going to put style components for corresponding JSX component.
7. `App.jsx` in this file we will write our code or put our JSX components & `App.css` is the style sheet for App.jsx

### Let create some new folders
![s3.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/s3.png)

---

## Let’s create a component
 React applications are built from isolated pieces of UI called *components*. A React component is a JavaScript function that you can sprinkle with markup. Components can be as small as a button, or as large as an entire page. Here is a `Gallery` component rendering three `Profile` components:

***First Card component*** 

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code.png)


---

## **Importing and exporting components**
 can declare many components in one file, but large files can get difficult to navigate. To solve this, I can *export* a component into its own file, and then *import* that component from another file:

***App.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%201.png)

***Card.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%202.png)

---

# JSX

## What is JSX???
 ⇒ JSX stands for JavaScript Extension Syntax. It's a syntax extension used in React that allows developers to write HTML-like code directly within JavaScript. So in one word JSX is not a JavaScript it’s a combination of JS and HTML.
JSX is complied in JS by Babel.

⇒ Each React component is a JavaScript function that may contain some markup that React renders into the browser. React components use a syntax extension called JSX to represent that markup. JSX looks a lot like HTML, but it is a bit stricter and can display dynamic information.
If we paste existing HTML markup into a React component, it won’t always work:

```jsx
const element = <h1>Hello, world!</h1>;
```


---

## Some Rules Of JSX

**1. Return a single root element:**
To return multiple elements from a component, **wrap them with a single parent tag.**
For example, you can use a `<div>`:

```jsx
	
    <div> //parent tag
      <div>hello world</div>
			<p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptates,
        numquam?</p>
    </div>

```

if u don’t want to add extra `<div>` to your code, u can write `<>` & `</>` instead

```jsx
	
    <> //parent tag
      <div>hello world</div>
			<p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptates,
        numquam?</p>
    </>

```

>This empty tag is called Fragment, It let u group thing without leaving any trace in the browser HTML tree.

**2. Close all the tags**
JSX requires tags to be explicitly closed: self-closing tags like `<img>` must become `<img />`, and wrapping tags like `<li>oranges` must be written as `<li>oranges</li>`.

**3. camelCase all most of the things!**
JSX turns into JavaScript and attributes written in JSX become keys of JavaScript objects. In your own components, you will often want to read those attributes into variables. But JavaScript has limitations on variable names. For example, their names can’t contain dashes or be reserved words like `class`.

---

## **JavaScript in JSX with Curly Braces**
 JSX lets you write HTML-like markup inside a JavaScript file, keeping rendering logic and content in the same place. Sometimes you will want to add a little JavaScript logic or reference a dynamic property inside that markup. In this situation, you can use curly braces in your JSX to open a window to JavaScript.

```jsx
import React from "react";

function Card(props) {
  let str = "Hii everyone!!!";
  return (
    <>
      <h3>{str}</h3>
      <p>2*2 = {2 * 2}</p>
    </>
  );
}

export default Card;
```

---

## Props 🥠
 React components use *props* to communicate with each other. Every parent component can pass some information to its child components by giving them props. Props might remind you of HTML attributes, but you can pass any JavaScript value through them, including objects, arrays, functions, and even JSX!

Props are the information that you pass to a JSX tag.

 ***Example***

***App.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%203.png)

***Card.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%204.png)

 ***Specifying a default value for a prop***

 want to give a prop a default value to fall back on when no value is specified, you can do it with the destructuring by putting `=` and the default value right after the parameter:
```jsx
function Avatar({ person, size = 100 }) {
  // ...
}

```

 ***Forwarding props with the JSX spread syntax***
```jsx
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```


***Passing JSX as children*** 
```jsx
<Card>
  <Avatar />
</Card>
```

When you nest content inside a JSX tag, the parent component will receive that content in a prop called `children`. For example, the `Card` component below will receive a `children` prop set to `<Avatar />` and render it in a wrapper div
```jsx
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```

---

## Style in CSS

 In react we create style component for each components. Like for `Card.jsx` we will create `Card.css` in style folder.
```css
.Card {
  padding: 20px;
  border: 2px solid gray;
}

h3 {
  color: aqua;
}
```

```jsx
import React from "react";
import "../style/Card.css"; //import card css from style

function Card(props) {
  let str = "Hii everyone!!!";
  return (
    <>
      <div className="Card"> //3rd rule for JSX -> class become className
        <h3>Hello Word</h3>
      </div>
    </>
  );
}

export default Card;
```

### Inline style in JSX
```jsx
import React from "react";
import "../style/Card.css"; //import card css from style

function Card(props) {
  let str = "Hii everyone!!!";
  return (
    <>
      <div style = {{
					padding: '20px',
					border: '2px solid gray'
			}}>
        <h3 style={{color: 'aqua'}}>Hello Word</h3>
      </div>
    </>
  );
}

export default Card;
```

---

## **Conditional Rendering**
 In react we can render components based on certain conditions.

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%205.png)

- In React, you control branching logic with JavaScript.
- You can return a JSX expression conditionally with an `if` statement.
- You can conditionally save some JSX to a variable and then include it inside other JSX by using the curly braces.
- In JSX, `{cond ? <A /> : <B />}` means *“if `cond`, render `<A />`, otherwise `<B />`”*.
- In JSX, `{cond && <A />}` means *“if `cond`, render `<A />`, otherwise nothing”*.
- The shortcuts are common, but you don’t have to use them if you prefer plain `if`.

---

# #Hooks

*Hooks* let you use different React features from your components. You can either use the built-in Hooks or combine them to build your own. This page lists all built-in Hooks in React.

[https://react.dev/reference/react/hooks](https://react.dev/reference/react/hooks)

## States in react ⚛️

### let’s understand with example
now lets try to build a counter. 
we are going to build a component where if we click a button our value will increase by one

### Count.jsx
```jsx
import React from "react";

function Count() {
  let count = 0;
  const increase = () => {
    count++;
    console.log(count);
  };
  return (
    <div
      className="box"
      style={{
        border: "1px solid aqua",
        padding: "20px",
        width: "150px",
        height: "150px",
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
      }}>
      <div>{count}</div>
      <button onClick={increase}>click</button>
    </div>
  );
}

export default Count;
```

### App.jsx
```jsx
import "./App.css";
import Count from "./components/Count";

function App() {
  return (
    <>
      <Count />
    </>
  );
}

export default App;
```

here in this code if we click `click` button our page will not going to update. but at the same time if we look at console window we can see our `count` is increase by 1. 

to resolve this problem we use #useState 

#useState is used to update elements because it allows functional components to maintain and manage their own state. By using #useState , React ensures that when the state changes, it triggers a re-render of the component, updating the UI to reflect the new state. This approach helps keep the user interface responsive and in sync with the data changes in the component. Essentially, #useState  is crucial for managing state changes within functional components and facilitating dynamic updates in the displayed elements of a React application.

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%206.png)

---

## ✔️Let’s build  a like button
today any social media platform have like buttons, where if we click it will fill up and again we clicked it will back to previous sate.

For example we can take Instagram Like button.
### LikeButton.jsx
```jsx
import React from "react";
import { useState } from "react";
import "remixicon/fonts/remixicon.css"; //before using this run a npm command "npm install remixicon --save" 

function LikeButton() {
  const [liked, setLiked] = useState(false);
  const clicked = () => {
    setLiked(!liked);
  };
  return (
    <>
      <span style={{ fontSize: "30px", color: "red" }} onClick={clicked}>
        {liked ? (
          <i className="ri-heart-fill"></i>
        ) : (
          <i className="ri-heart-line"></i>
        )}
      </span>
    </>
  );
}

export default LikeButton;
```

![s4.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/s4.png)

![s5.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/s5.png)

---

## Callback in state
`setState` is an async function for this we can’t call same function multiple times.
for Example - we want to build a button which increase value by 3
### Count.jsx
```jsx
import React from "react";
import { useState } from "react";

function Count() {
  const [count, setCount] = useState(0);
  const increase = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  };
  return (
    <div
      style={{
        border: "1px solid aqua",
        padding: "20px",
        width: "150px",
        height: "150px",
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
      }}>
      <div>{count}</div>
      <button onClick={increase}>click</button>
    </div>
  );
}

export default Count;
```

this code doesn't perform as we want. to solve this problem we use callbacks in JS
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%207.png)

---

## Objects & State
Like number and String we can use Objects & arrays in state. but it’s not so easy.
### LudoBoard.jsx
```jsx
import React from "react";
import { useState } from "react";

function LudoBoard() {
  const [moves, setMoves] = useState({red: 0, green: 0, yellow: 0, blue: 0}); //object

  const updateRed = () => {
    console.log(moves.red);
    setMoves((prevMoves) => {
      return {...prevMoves, red: prevMoves.red+1}; //increase move by 1 & change the address of object using spread operator
    });
  };
  const updateYellow = () => {
    setMoves((prevMoves) => {
      return {...prevMoves, yellow: prevMoves.yellow+1};
    });
  };
  const updateGreen = () => {
    setMoves((prevMoves) => {
      return {...prevMoves, green: prevMoves.green+1};
    });
  };
  const updateBlue = () => {
    setMoves((prevMoves) => {
      return {...prevMoves, blue: prevMoves.blue+1};
    });
  };

  return (
    <>
      <div>Let's begin the game</div>
      <div className="gameBoard" >
        <div className="Red" style={{background: "Red"}}>
          <p>Red Moves: {moves.red} </p>
          <button onClick={updateRed}>+1</button>
        </div>
        <div className="Green" style={{background: "Green"}}>
          <p>Green Moves: {moves.green}</p>
          <button onClick={updateGreen}>+1</button>
        </div>
        <div className="Yellow" style={{background: "Yellow", color: "black"}}>
          <p>Yellow Moves: {moves.yellow} </p>
          <button onClick={updateYellow}>+1</button>
        </div>
        <div className="Blue" style={{background: "Blue"}}>
          <p>Blue Moves: {moves.blue} </p>
          <button onClick={updateBlue}>+1</button>
        </div>
      </div>
    </>
  );
}

export default LudoBoard;
```

here we have to change address of key & value other wise react can’t detect the changes for that reason we use spread operator  [`. . .`]

---

## Prevent Re-Rendering
A re-render means that
1. React did some work to calculate what all should update in this component
2. The component actually got called (you can put a log to confirm this)
3. The inspector shows you a bounding box around the component

It happens when
1. A state variable that is being used inside a component changes
2. A parent component re-render triggers all children re-rendering

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%208.png)

### Let’s minimize re-rendering
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%209.png)


---

## useEffect

`useEffect` is a React Hook that lets you [synchronize a component with an external system.](https://react.dev/learn/synchronizing-with-effects)

```jsx
useEffect(setup, dependencies?)
```

 [https://react.dev/reference/react/useEffect](https://react.dev/reference/react/useEffect)

---

## useMemo

`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```jsx
const cachedValue = useMemo(calculateValue, dependencies)
```

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2010.png)

>[https://react.dev/reference/react/useMemo](https://react.dev/reference/react/useMemo)

---

## useCallback

`useCallback` is a React Hook that lets you cache a function definition between re-renders.

```jsx
useCallback(fn, dependencies)
```

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2011.png)

 [https://react.dev/reference/react/useCallback](https://react.dev/reference/react/useCallback)


---

## useRef

useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

```jsx
const ref = useRef(initialValue)
```

![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2012.png)

 [https://react.dev/reference/react/useRef](https://react.dev/reference/react/useRef)

---

## Custom Hooks

## Routing - react-router-dom

**App.jsx**
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2013.png)

**NavBar.jsx**
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2014.png)

**Landing.jsx**
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2015.png)

**Dashboard.jsx**
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2016.png)


---

# Prop Drilling
Context API use to make code cleaner & get rid of prop drilling, it’s not use increase performance.

[https://react.dev/learn/passing-data-deeply-with-context](https://react.dev/learn/passing-data-deeply-with-context)

***App.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2017.png)

***Context.jsx***
![code.png](React%20js%20b83ecf919a664da5a650f97e1e1319f4/code%2018.png)
