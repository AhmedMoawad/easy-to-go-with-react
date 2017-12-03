# React - The Lego Game
In this tutorial we will talk about how to go through <strong> React </strong> and prepare you to be able to build web apps using the amazing <strong> React </strong> like you play with <em> lego bricks </em> :smile:.

<br />

## Table of Contents

  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
  - [Tutorial Map](#tutorial-map)
  - [Quick Look at ES6](#quick-look-at-es6)
    - [let](#let)
    - [const](#const)
    - [Arrow Functions](#arrow-functions)
    - [Default Parameters](#default-parameters)
    - [String Interpolation](#string-interpolation)
    - [Modules](#modules)
  - [React Overview](#react-overview)
  - [Big Picture](#big-picture)
  - [Virtual DOM](#virtual-dom)
  - [JSX](#jsx)
    - [Intro](#intro)
    - [What JSX compiles to](#what-jsx-compiles-to)
    - [Expressions](#expressions)
    - [HTML Attributes](#html-attributes)
    - [Styles](#styles)
    - [Binding Events](#binding-events)
  - [First Lego](#first-lego)
    - [Create it](#create-it)
    - [Render it](#render-it)
  - [Overview on React Components](#overview-on-react-components)
    - [Props](#props)
    - [State](#state)
  - [Treating with Forms](#treating-with-forms)
  - [Tips and Tricks: Part 1](#tips-and-tricks)
  - [Communication between Components](#communication-between-components)
    - [From Parent to Child](#from-parent-to-child)
    - [From Child to Parent](#from-child-to-parent)
  - [Component Life Cycle](#component-life-cycle)
    - [constructor](#constructor)
    - [componentWillMount](#componentwillmount)
    - [render](#render)
    - [componentDidMount](#componentdidmount)
    - [componentWillReceiveProps](#componentwillreceiveprops)
    - [shouldComponentUpdate](#shouldcomponentupdate)
    - [componentWillUpdate](#componentwillupdate)
    - [componentDidUpdate](#componentdidupdate)
    - [componentWillUnmount](#componentwillunmount)
- [Type checking with PropTypes](#type-checking-with-proptypes)

## Prerequisites
In order to go ahead with this tutorial, You should have good knowledge about the following

- [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
<br />

## Setup

We will use in this tutorial the simple and easy method to create react app called `create-react-app` package
1. Install `create-react-app` NPM package globally
```
 npm i -g create-react-app
```   
2. Create your app
```
 create-react-app your-project-name
 
 cd your-project-name
 
 yarn install
```
3. Start your app
```
 yarn start
```

You can visit [Create React App](https://github.com/facebookincubator/create-react-app) for more info.
<br />

## Tutorial Map
![Tutorial Map](https://user-images.githubusercontent.com/11356226/33302591-e89a294a-d405-11e7-9485-cbffc33b79a5.png)
<br />

## Quick Look at ES6
> We will take here a quick tour on the new features on EchmaScript 6.

### let
We all know that declaring variable with `var` makes this variable available only on the function scope that it has been declared in. But with `let` every `{ }` consider a scope so any variable that declared with `let` will available only on this curly braces scope.

> Example using `var`:
```javascript
if (true) {
   var x = 5
}
console.log("using var: ", x)
```
it will result: ` using var: 5 `

> Example using `let`:
```javascript
if (true) {
   let x = 5
}
console.log("using let: ", x)
```
it will result:  `ReferenceError: x is not defined`

So `let` make a scope within `if` statement curly braces and `var` don't.

### const
`const` almost used to daclare any variables that will not changed or in accurate say you will not assign it a new value using `=` because when you declare a composite typed variable like objects or arrays you can add or remove elements to or from it normally but you can't asign to the variable another value.

```javascript
const x = [1, 2, 3]
x.push(4)       // x will now be [1, 2, 3, 4]
                // but
x = [1, 4, 6]   // It will raise TypeError: Assignment to constant variable
```

### Arrow Functions
Arrow Functions is a special type of functions that solve the problem of `this` keyword strange behavior when calling function from a context other than its own one ( it's not strange if you know how it works :smile: ) and convert it to Lexical `this` so that it maintains that the context that call it will be the reference `this`.

Examples on How to write it:
```javascript 
// Shorthand arrow functions with returned expression
const expressionFn = (x, y) => x + y;

// Statement Arrow Functions
const statementFn = (x, y) => {
  if (x && y) {
    return x + y
  }
  return false
}
```

### Default Parameters
EcmaScript6 added the ability to add default values to the given parameters if it's not be provided to the function. And that's for sure make the code more readable and organizable.

Here is an example 
```javascript 
function doSum (x, y = 7, z = 12) {
 return x + y + z;
}

doSum(2)         // output: 21
doSum(2,4)       // output: 18
doSum(2,4,10)    // output: 16
```
> Note: You must make function default parameters the last parameters of it in arrangement or assign its value to `undefined` when calling the function but that will be little confusing
```javascript
function doSum (x, y = 7, z) {
 return x + y + z;
}

doSum(2,undefined,6)       // output will be 2 + 7 + 6 = 15 
```

### String Interpolation
String Interpolation give the ability to write more readable and organized strings without need to use `+` operator to concatenate the string typed variables with each other.

Here is an example for that

```javascript
const firstName = 'Ahmed'

const lastName = 'Moawad'

let fullName = 'Full Name is ' + firstName + ' ' + lastName        // The old way

fullName = `Full Name is ${firstName} ${lastName}`                 // New String Interpolation

// Result for both: Full Name is Ahmed Moawad
```

### Modules
This is a big new feature and all JavaScript was waiting for releasing it to make your code more modular and organized. There is three points that we will talk about for this feature:

#### 1. Exporting
> In order to make class, function or any variable inside a file (module) available in other files (modules) we use module exporting, and here are some examples for how to do that:

```javascript
/**
* @file index.js 
*/

// Exporting Function
export function getFullName(firstName, lastName) { 
   return `${firstName} ${lastName}` 
}

// Exporting variable
export const title = "Frontend Engineer"

```

#### 2. Importing
> In order to import class, function or any type of variable inside a file (module) to be able to use it in this file we use module importing, and here are some examples for how to do that:

```javascript
/**
* @file about.js 
*/

// Import getFullName function and title variable from index module
import { getFullName, title } from 'index'

// Use them
const fullName = getFullName('Ahmed', 'Moawad')

console.log(`My Name is ${fullName} and I'm ${title}`)

// Result: My Name is Ahmed Moawad and I'm Frontend Engineer

```

#### 3. Default Exporting
> This is an awesome feature in order to make any kind of variables the default one when exporting to other modules. Here is an example that will explain it's functionality in more details:

```javascript
/**
* @file index.js 
*/

/*
* .... brevious code
*/

// Export the following Object as the default export for index module
export default {
 firstName: 'Ahmed',
 lastName: 'Moawad',
 title: 'Frontend Engineer'
}


/**
* @file about.js 
*/

// Import Default without the curly braces and with any name you choose for it
import myData, { getFullName } from index

const fullName = getFullName(myData.firstName, myData.lastName)

console.log(`My Name is ${fullName} and I'm ${myData.title}`)

// Result: My Name is Ahmed Moawad and I'm Frontend Engineer

```
<br />

## React Overview
In this section we will talk about React and why using it over other like libraries.

> If you don't need from me to prove to you that React is amazing :smile: you can just move to [Big Picture](#big-picture) section directly.

#### What is React
> Source of following definition is from [React official website](https://reactjs.org/tutorial/tutorial.html#what-is-react)

React is a declarative, efficient, and flexible JavaScript library for building user interfaces.

#### So Why React? 
Of course, there are many reasons to use <strong>React</strong> but I will write down some of them:

##### 1. React is a component based Libray
That's mean with React you can produce reusable isolated elements called components that reduce the redundancy of your application elements, improve code quality and inspire collaboration with it's community.

##### 2. React is Fast
React uses [Virtual Dom](#virtual-dom) mechanism to improve the application rendering performance and reduce the unnecessary rendering and modification So your application will be very healthy and efficient.

##### 3. React has a single source of truth
React adopt the concept of unidirectional Data Binding. So it removes the ambiguity of conflicts results from the existance of different sources of the data.

##### 4. React has a full support to [Redux](https://redux.js.org)
So You can manage your application state with the awesome Redux.

##### 5. React has a growing EcoSystem
Facebook and React community developed React and it's ecosystem rapidly. You can find [ReactNative](https://facebook.github.io/react-native/) for mobile development, [ReactRouter](https://reacttraining.com/react-router/) for client and server rendering, [Redux](https://redux.js.org) integration for managing your Application State, [Jest](https://facebook.github.io/jest/) and [Enzyme](http://airbnb.io/enzyme)for testing your React Applications and many others.

##### 6. React has awesome DevTools
React has it's official [DevTools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) to enhance the way you debug your React application.

##### 7. React scale from small to Big applications
React give you the ability to produce small scale appication and can easily scale to a large web applications.

> There are many other reasons to develop with React. I hope you touch them while developing with React
<br />

## Big Picture

<p align="center">
  <img src ="https://user-images.githubusercontent.com/11356226/33383928-52be15a2-d52d-11e7-9dd9-05c81dcc592b.gif" />
  <p align="center">
    -- Illustrative Example explains React Components in a simple way --
  </p>
</p>
<br/>
<br/>

React is component based library so <strong>Component</strong> is considered the core unit of React. 

As we have seen in the illustrative example, The component is consists of some <strong> props </strong> that will be provided to it at its construction and have a <strong> state </strong> that is represents the behaviour of the component and will be initialized during component construction.

After Construction Your component Layout (HTML Template) will be rendered based on the provided props and the initialized State.

And If the component be provided by different <strong>props</strong> or the <strong>state</strong> of it changes, The component will be rendered another time with the new effect.

The component have a life cycle we will talk about it later in details to show how to use it the best way.

<br />

## Virtual DOM
> React uses Virtual DOM in order to enhance the web application performance, So React is very fast.

### Problem to Be solved
Manipulating with the <strong>DOM</strong> is slow because changing it directly change the web page. So If you changed it many times you will suffer from rendering performance issue and nowadays Most of Web Apps needs to change the DOM frequently. So <strong> Virtual DOM </strong> came to solve this problem.

### What is Virtual DOM
> Source of following definition is [Codecademy](https://www.codecademy.com/articles/react-virtual-dom)

A virtual DOM object is a representation of a DOM object, like a lightweight copy.

A virtual DOM object has the same properties as a real DOM object, but it lacks the real thing's power to directly change what's on the screen.

Manipulating the DOM is slow. Manipulating the virtual DOM is much faster, because nothing gets drawn onscreen. So React updates all DOM changes on the virtual DOM then at the end it will compare the `actual DOM` with the `virtual DOM` and only redraw the affected components by these changes.

Think of manipulating the virtual DOM as editing a blueprint, as opposed to moving rooms in an actual house.

<br />

## JSX
> It’s not a new language, but it is awesome

### Intro
Look at the following Code

```jsx
const element = <h1>Hello, React lovers!</h1>;
```
<p align=center>
  What is that Code? 
</p>
<p align=center>
  It's neither HTML nor JavaScript. It just the awesome <strong>JSX</strong>.
</p>

### What JSX compiles to
> We use JSX to transpile it to vanilla JavaScript using [Babel](https://babeljs.io/)

The following code is JSX:
```jsx
const element = <h1 className = 'greet'>Hello, React Lovers!</h1>;
```
will be compiled using [Babel](https://babeljs.io/) to the following Code:

```javascript
// Create a React Element
const element = React.createElement(
	'h1' ,                                  // The Tag Name of the element
	{className: 'greet'} ,                  // The properties of this element
	‘Hello, React Lovers!’                  // HTML Content inside the Element
)
```
and <strong>React</strong> now will take it's responsibility to convert that to HTML DOM Element as follows:

```html
<h1 class='greet'> Hello, React Lovers!</h1>
```
Now, We will take a quick tour on How to write <strong>JSX</strong> in order to write React web apps

### Expressions
Now we will introduce how treat with JavaScript Expressions and how to interpolate them in JSX templates in order to generate dynamic components.

```jsx
var name = 'Ahmed'
//Interpolation in JSX
var element = <h1>Hello, { name }</h1>;

//Use JSX as an Expression
function sayHello(name){
    if(name)
          return <h1>Hello, { name }</h1>;
    return <h1>Hello, Guest</h1>;
}
```

So the generated HTML based on the above parameters will be:

```html
<h1>Hello, Ahmed</h1>
```

### HTML Attributes
Now let's talk about how to provide the elements with the HTML attributes

> Note: JSX  use JavaScript Syntax (camelCase) not HTML Syntax in adding attributes i.e 

There are the list of HTML attributes that you can use in JSX:

```
accept acceptCharset accessKey action allowFullScreen allowTransparency alt async 
autoComplete autoFocus autoPlay capture cellPadding cellSpacing challenge charSet
checked cite classID className colSpan cols content contentEditable contextMenu 
controls controlsList coords crossOrigin data dateTime default defer dir disabled 
download draggable encType form formAction formEncType formMethod formNoValidate 
formTarget frameBorder headers height hidden high href hrefLang htmlFor httpEquiv 
icon id inputMode integrity is keyParams keyType kind label lang list loop low 
manifest marginHeight marginWidth max maxLength media mediaGroup method min 
minLength multiple muted name noValidate nonce open optimum pattern placeholder
poster preload profile radioGroup readOnly rel required reversed role rowSpan 
rows sandbox scope scoped scrolling seamless selected shape size sizes span 
spellCheck src srcDoc srcLang srcSet start step style summary tabIndex target
title type useMap value width wmode wrap
```

You can notice that <strong>class</strong> HTML attribute has been renamed with `className` in order to doesn't make a conflict with `class` keyword in JavaScript. and Html label attribute <strong>for</strong> converted to `htmlFor` too.

Here an Example:
```jsx
var cls = 'greet';
var element = <h1 className={cls} id = '2'>Hello, { name }</h1>;

```

### Styles

You can add inline styles to your element using the follwing method

```jsx
// Construct a Style Object
var styles = {
  backgroundColor: 'red',		// the style properties follows JavaScript naming convention
  color : 'orange'
}

var element = <h1 style={ styles } >Hello There </h1>;

```

### Binding Events
Now, Let's talk about how to bind events to the element, we will use this naming covention:

For Example, <strong>Click</strong> Event will be `onClick` instead of `onclick`.

Here are some examples for doing that

```jsx
// Add Input event using anonymous function
let input = <input type=‘text’ onInput={(e)=>(e.target.value)}/>;

// Add Click Event use predifned function called someFn
let button = <button onClick={ someFn }>Hello, React!</button>;

var v;
let select= (<select onChange = {function(e){v = e.target.value}}>
		 	<option> Egypt </option>
			<option> USA </option>
			<option> Spain </option>
                </select>);
```
<br />

## First Lego
> I mean First React Component :wink:
As we have seen in [Big Picture](#big-picture) section that the component is the main component and here we will create it and then rendered it.

Let first setup our application using the instructions in [Setup](#setup) section. 

Then Create a file called `Hello.js` in `src` directory. So the hierarchy will be something like that:
```
Your-App-Name
  |
  - public
  |   |
  |   - index.html 
  |
  - src
  |  |
  |  - index.js
  |  - Hello.js
```

### Create it
Here is an example of how to create new Component in the created file `Hello.jsx`
```jsx
/**
* @file Hello.js
*/

// import React 
import React from 'react';

// Create Hello Component
class Hello extends React.Component {
  /**
  * Render Function is responsible for render this component
  */
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
<p align='center'>
    <img width='250px' src='https://user-images.githubusercontent.com/11356226/33449976-08e7925a-d613-11e7-882b-a203f22f6799.png'/>
<p>

### Render it
Now, Let's render it on our application. Open file called `index.js` and use your component inside it like the following

```js
/**
* @file index.js
*/

// Import React DOM - It responsible for compiling React Component into HTML Element
import ReactDOM from 'react-dom';

// Import Your Component
import Hello from 'Hello';

// Run the Render Function to render your App
ReactDOM.render(
  <Hello name = ‘Ahmed’ />,			// Use your component and provide it with name prop
  document.getElementById('root')		// Render your App into the element whose id named root
);

```

What happens above is that we use <strong>ReactDOM</strong> method called `render` to render your application into the static html file called `index.html`.

<p align='center'>
    <img width='250px' src='https://user-images.githubusercontent.com/11356226/33451154-ce0994c2-d616-11e7-924e-3ab574f82682.png'/>
</p>

Now run this command: `yarn start`

Congratulations :tada:! you just created your first React Component Keep the good spirit on :muscle:.

<br />

## Overview on React Components
> I mean Lego bricks :confused:

Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.

We will talk now in details about the [props](#props) (Inputs) and the [state](#state) of the component. 

Later when we will be familiar with React, will discuss the component [Life Cycle](#life-cycle)

### Props
> Props regarding to the component are like Eye Color regarding to you, I hope you don’t put lenses

Component haven't any responsiblity on creating or updating the `props` it uses it only to generate it's `state` and it's HTML Template UI. 

You can think of `props` like weather temperature (Something you have no hand on changing it), If the temperature goes down, We put on more clothes and vice versa.

> Note: All React components must act like pure functions with respect to their props.
 
#### Use it
Here is an example on How to use props on component

```jsx
/**
* @file Hello.js
*/

/* ... */
class Hello extends React.Component {
  render() {
    return <div> 
             <img src={this.props.nationality + ‘.png’} />
	     Hello, I'm {this.props.name} 
           </div>;
  }
}

```

```jsx
/**
* @file index.js
*/

/* ... */
ReactDOM.render(
  <Hello name = 'Ahmed' nationality = 'egypt' />,
  document.getElementById('root')
);

```
And the result will be something like that

<p align='center'>
	<img width='20px' src='https://upload.wikimedia.org/wikipedia/commons/a/a0/Flag_of_the_Arab_Republic_of_Egypt_1984.png'/>
	Hello, I'm Ahmed
</p>

### State
> State regarding to the component are like your mood regarding to you, I hope you’re happy

React Component have the full control of it's state. It can initialize, use and update it.

You can think of `state` like your mood based on the weather. Some of us feel happy when it's raining, but some others feel bored.

So The weather temperature will be like a `prop` and your mood that depending on the weather will be like `state`.

Let's know How to manage the component state.

#### Initialize and use it 

We can initialize the state of the component in the `constructor` method of the component `class`

```jsx
/**
* @file Hello.js
*/

/* ... */
class Hello extends React.Component {
  constructor(props) {
    // we must call super method at the first in order to define the class as React component
    super(props)
    
    // we can initialize the state like the following
    this.state = {mood: 'happy'}
  }
  
  render() {
    return (<div>
    		<img src={this.state.mood + '.png'} />
		Hello, {this.props.name} 
            </div>);
  }
}
```

and the result will be something like that:

<p align='center'>
	:grinning: Hello, I'm Ahmed
</p>

#### Change it

We can update the state using `setState`. Let's take an example

```jsx
class Hello extends React.Component {
  constructor(props) { 
    /* ... */
    
    // Add interval to change the mood every 0.5 sec
    window.setInterval(this.toggleMood, 500) 
  }
  
  toggleMood () {
     let currentMood = (this.state.mood === ‘happy’)? ‘sad’ : ‘happy’; 
     this.setState({mood: currentMood});
  }
  
  render() {
    return( <div>
	      Hello, {this.props.name}
	      <img src={this.state.mood + ‘.png’} />
            </div> );
  }
}
```

The result will be something like that 

<p align='center' >
	<img width='25px' src='https://user-images.githubusercontent.com/11356226/33455319-5962aff6-d624-11e7-9687-8f6ea797c9ad.gif'/>
	Hello, I'm Ahmed
</p>

<br />

## Treating with Forms
> In React, We doesn’t treat forms as like classic way

### Overview
<p align='center'>
	<img width="453" src="https://user-images.githubusercontent.com/11356226/33496498-24459ca2-d6d3-11e7-81bb-97f3f3a90c57.png">
</p>

Submitting Form doesn’t mean reloading the web page because that's not the react way and herrewe treat with a single page application.

Form Component State are the source of truth for the form values so when we proceed to submit the form we get it's values from the state of it's React component in order to maintain the unidirectional data flow mechanism.

### Implement It
Here are an example of how to create a form and manage it's submittion.

```jsx
class CustomForm extends React.Component {
  constructor(props) { 
    super(props);
    
    // initialize the form values state here
    this.state = {value: ''};
    
    // bind all prototype methods to the component context - we will discuss this issue below 
    this.handleSubmit = this.handleSubmit.bind(this)
    this.handleChange = this.handleChange.bind(this)

  }
  
  render() {
    return <form onSubmit={this.handleSubmit}>
              <input type="text" value={this.state.value} onChange={this.handleChange} />
	      <input type="submit" value="Submit" />
      	   </form>;
  }
  
  handleChange (e) {
     // update the state based on the changing input value
     this.setState({value: e.target.value})
  }
  
  handleSubmit (e) {
     e.preventDefault()
     /*
     * We have now all the form values stored on the component state,
     * So we can make an ajax request or validate the date before that, 
     * or do whatever your business required
     */
  }
}

```

Now let's discuss what we have done with the above Form Component in many points:

1. If we want to have a controlled Component, we must map every form input values to a state property as we have done above.

2. We notice that we use `bind` method to bind `handleSubmit` and `handleChange` methods to the component context. That's because when we use it in the jsx template these methods loses the context of the component so if we didn't bind them like that then if we use `this` keyword in these methods it will not refer to any context so must bind it hardly to the context that we want in order to everything go as we have planned.

3. We notice that we bind the input value attribute to the state property `value` so the value of this component came from one source of truth (The state) and then we handle `change` event on the input to get the value that came from the user and update the state with it so the bound input value will be changed by changing the state.

4. In `handleChange` we can validate the coming value before updating the state with in order to grauntee that the values that will be submitted is correct.

5. In `handleSubmit` we prevent the default behaviour from happening, and then we can use the state as the source of the form values that we will submit.

## Tips and Tricks

### Use the magic of `&&`
> Let's explain firstly how `&&` works

`&&` operator seeks for the falsy value of the two operands. And it will stop seeking when it finds any <strong>falsy</strong> and return the last value it stops at. Here are some examples of it

> Note: Falsy values in JavaScript are (`false`, `0`, `NaN`, `''`, `undefined`, `null`)

```javascript
4 && 0           // return 0
'' && 'React'    // return ''
true && 5	 // return 5 (not true)
```

now let's show how to use it in React:

```jsx
class Visit extends React.Component {
  render() {
    return <div>
	     { this.props.visits > 0 && <p> You have {this.props.visits} visits </p> }
	   </div>;
  }
}


ReactDOM.render( <Visit visits = { 6 } />, document.getElementById('root'));

```
When rendering this compoenent it will show the following

<p align='center'> You have 6 visits </p>
<br />

That's because the `visits` prop is `6` that is greater than `0` so the first expression will return `true` So `&&` will continue seeking for the falsy value so it returns the second operand which is the element that we want to render if the `visits` prop is greater than `0`.

### Use the `map` function

Map function is one of the JavaScript Array's methods that use an array to produce another array based on the first one. Here is an example of it. 

And You can read about it in [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 

```javascript

let arr = ['A', 'M', 'Z']

// Now let generate an array of char code based on the previous array
let codeArr = arr.map(ch => ch.charCodeAt(0))    // codeArr will be [65, 77, 90]
```

Now let's use it to generate alist of elements in React:
```jsx

class NameList extends React.Component {
  render() {
    return <ul>
	     {this.props.users.map( user => <li>{ user }</li> )}
	   </ul>;
    }
}

ReactDOM.render( <NameList users = {['Ahmed', 'Ali', 'Sara']} />, document.getElementById('root'));

```
Now the result will be something like the following:

<ul>
   <li>Ahmed</li>
   <li>Ali</li>
   <li>Sara</li>
</ul>
<br />

## Communication between Components

<p align='center'>
   <img width="781" alt="screen shot 2017-12-01 at 11 44 36 pm" src="https://user-images.githubusercontent.com/11356226/33504822-ad50ef74-d6f1-11e7-8967-aa2532a03a9b.png">
</p>

The above illustration explains how components communicate with each others. 

let's devide the communication between components into two types based on their position:

### From Parent to Child
This is the tradional way of communication because the Parent component is responsible for providing the props to it's children So when parent want to communicate with child it provide it with props.

> Here is an example of that:

```jsx
// Build Child Component
class Child extends React.Component {
  render() {
    return <p>{this.props.name}</p>;
  }
}

```

```jsx

import Child from 'Child'

// Use Child Component
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {name: 'Ahmed'}
  }
  render() {
    return <div>
		<Child name = {this.state.name} />
	    </div>;
  }
}

```

So We see here that Child prop `name` is depending on the Parent `name` state property.

### From Child to Parent
Another way of communication is when child want to notify the parent about something change in it. So In React we use callback Invoking that's mean that the parent provide the component with callback prop that will be invoked on the right time to change something in Parent Component.

> Let's take an Example

```jsx
class Parent extends React.Component {
  /* ... */
  render() {
    return <div> 
    	     <p>{this.state.value}</p>
	     {/* we can provide the callback as prop like onChange prop*/}  
	     <Child name={this.state.name} onChange={this.handleChange} />
           </div>;
  }
  
  handleChange(v){
	this.setState({value : v})	
  }
}

```
```jsx
class Child extends React.Component {
  /* ... */
  render() {
    return <div> 
	      <p>{this.props.name}</p>
              <input onChange={this.handleInputChange} /> 
	   </div>;
  }
  
  handleInputChange(e){
  	// Here we use onChange Prop to invoke the parent handleChange Method
  	this.props.onChange(e.target.value)	
  }
}

```

As we have seen above in child component if the user change the input `handleInputChange` will be invoked. And when `handleInputChange` have invoked it will invoke the provided method prop `onChange` and pass it the required parameter that will change the state of parent.

<br />

## Component Life Cycle
> And Component Said: Yes, I have my own life. Deal with it

Life Cycle is a way to hook the Component life phases to do the right action on the right time

Component Have three main life phases:

#### :triangular_flag_on_post: Mounting Phase

This is the phase where the component been constructed, initialized and rendered for the first time on the DOM.
 
 <p align='center'>
	<img width="781" alt="screen shot 2017-12-01 at 9 40 38 pm" src="https://user-images.githubusercontent.com/11356226/33500141-6ec1ad86-d6e0-11e7-8ee5-01c6f5d71f79.png">
 </p>
 <br />
 
#### :triangular_flag_on_post: Updating Phase

After Mounting the Component, Anytime, the state or props change the component will enter this phase.
 
 <p align='center'>
	<img width="783" alt="screen shot 2017-12-01 at 9 50 19 pm" src="https://user-images.githubusercontent.com/11356226/33500514-b7c7780c-d6e1-11e7-9e1c-25e8ab19d848.png">
 </p>
 <br />
 
#### :triangular_flag_on_post: Unmounting Phase

This phase occurs when the component is about to be removed from the DOM and destroyed.
 
  <p align='center'>
	<img width="778" alt="screen shot 2017-12-01 at 9 50 58 pm" src="https://user-images.githubusercontent.com/11356226/33500593-0643898a-d6e2-11e7-9d65-30a6959b0e2f.png">
 </p>
 <br />
 
### `constructor`
##### Definition    
```javascript 
constructor(props)
```
`props` is the initial props that provided to the component

##### Calling Time
The constructor for a React component is called before it is mounted

##### Uses
1. Initialize The Component State Object
2. Bind The methods to the component

##### Notes
1. If you didn’t use it , no need to implement it
2. When implement it don’t forget to call `super(props)` before anything else.
<br />

### `componentWillMount`
##### Definition    
```javascript 
componentWillMount()
```
##### Calling Time
invoked immediately before mounting occurs and before `render` method

##### Uses
1. Update The Component State based on Props (Must use `setState` method)

##### Notes
1. It runs one time through the Component Life Cycle
<br />

### `render`
##### Definition    
```javascript 
render()
```

##### Calling Time
Called After `componentWillMount` & `componentWillUpdate`

##### Uses
1. Use States & Props to return a Single React Element represent the Component.
2. We can return `null` or `false` to indicate that you don't want anything rendered


##### Notes
1. render method is required to be implemented.
2. render method should be pure function.
<br />

### `componentDidMount`
##### Definition    
```javascript 
componentDidMount()
```

##### Calling Time
invoked immediately after a component is mounted

##### Uses
1. Treat with DOM executed here
2. Load data from remote server

##### Notes
1. Run one time through the Component Life Cycle.
2. If we use `setState` it will run render method another time 
<br />

### `componentWillReceiveProps`
##### Definition    
```javascript 
componentWillReceiveProps(nextProps)
```
`nextProps` is the new provided props that still not attached to the component

##### Calling Time
invoked before a mounted component receives new `props`

##### Uses
1. update the state in response to prop changes.

##### Notes
1. Calling this method doesn’t mean the value of props has changed.
2. Calling setState generally doesn't trigger this method.
<br />

### `shouldComponentUpdate`
##### Definition    
```javascript 
shouldComponentUpdate(nextProps, nextState)
```
`nextProps` is the new provided props that still not attached to the component
`nextState` is the updated state after using `setState` method on the previous hooks that still not attached to the component

##### Calling Time
invoked before rendering when new props or state are being received

##### Uses
1. Allows your Component to exit the Updating Phase if there is no reason to apply a new `render`.

##### Notes
1. When implement it don’t forget to return <strong>Boolean</strong> value.
2. Returning `true` means that `render` method will be called.
3. Returning `false` means that `render` method won’t be called.
<br />

### `componentWillUpdate`
##### Definition    
```javascript 
componentWillUpdate(nextProps, nextState)
```
`nextProps` is the new provided props that still not attached to the component
`nextState` is the updated state after using `setState` method on the previous hooks that still not attached to the component

##### Calling Time
invoked immediately before rendering when new props or state are being received

##### Uses
1. perform preparation tasks before an update occurs

##### Notes
1. you cannot call `setState` method here because it will make the component runs in recussive way and will raise maximumm stack exceed.
<br />

### `componentDidUpdate`
##### Definition    
```javascript 
componentDidUpdate(prevProps, prevState)
```
`prevProps` is the props that previously attached to the component but it is not now it's current props
`prevState` is the state that previously attached to the component but it is not now it's current state

##### Calling Time
is invoked immediately after updating occurs

##### Uses
1. Treat with DOM executed here
2. Load data from remote server

##### Notes
1. You can control here if you want to get data from the remote server or not based on the changing of props
<br />

### `componentWillUnmount`
##### Definition    
```javascript 
componentWillUnmount()
```
##### Calling Time
is invoked immediately before a component is unmounted and destroyed

##### Uses
1. Perform any necessary cleanup (tear down) tasks in this method like removing timeouts or intervals that is used during component life cycle. 

<br />

## Type checking with PropTypes

We all know that JavaScript is Dynamic Data Typed Language so there is no restrictions on variables types. This feature gives us the felixibility in many cases but in other cases in order to improve your code quality and to ensure that everything works fine we need to check the types of variables. From this prespective, The Type checking concept appears in many ways:

- [TypeScript](https://www.typescriptlang.org/) 
We can find that there is a complete language to solve this issue and other issues

- [Flow](https://flow.org/)
A static type checker tool called that can be integrated with many IDEs

- [PropTypes](https://github.com/facebook/prop-types) 
A npm package that was made espcially for React Components Props type checking.

> So let's introduce `PropTypes` in the following points.

<p align='center'>
	<img src='https://user-images.githubusercontent.com/11356226/33525383-0baad080-d837-11e7-9de4-00656388096c.gif'>
</p>

### Use PropTypes
First we must install the `prop-types` npm package using the following command:

```
cd your-project
npm install --save prop-types
```

> Here is an exmample of how to use <strong>PropTypes</strong>:

```jsx
// import PropTypes package
import PropTypes from 'prop-types';

class User extends React.Component {
  render() {
    return ( 
      <div> 
	<h1>{this.props.name}</h1>
	<p>{this.props.age}</p>
      </div>);
  }
}

// Add your Props types in order to be checked during app running
User.propTypes = {
     name: PropTypes.string,
     age: PropTypes.number
}

```

Let's take a quick tour on `prop-types`

### Basic Types
```jsx

import PropTypes from 'prop-types';

class Student extends React.Component { /* ... */ }

Student.propTypes = {
     name: PropTypes.string,		     // Define prop name as String type
     age: PropTypes.number,		     // Define prop name as Number
     isEgyptian: PropTypes.bool,             // Define prop name as Boolean
     scores: PropTypes.array,		     // Define prop name as Array
     schedule: PropTypes.object,	     // Define prop name as Object
     study: PropTypes.func,		     // Define prop name as Function
};

```

> Note: Use 'object' PropType is not recommended, Use [shape](#shape) propType instead.

### Enums

PropTypes Enums can be: 
- Prop value be one of list of specific values.
- Prop type be one of list of specific types.

Here is an example of how to do that:

```jsx
import PropTypes from 'prop-types';
class Student extends React.Component { ... }

Student.propTypes = {
     subject: PropTypes.oneOf([‘React’, ‘Angular’]),       // subject value may be React or Angular only
     id: PropTypes.oneOfType([			           // id data type may be Number or String only
     	PropTypes.number,
	PropTypes.string
     ])
}
```

### Collection of Specific Type
### Shape
### isRequired
### isInstance
