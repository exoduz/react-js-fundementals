# React.js Fundementals #
##### http://courses.reactjsprogram.com/courses/reactjsfundamentals #####

## Section 1 - Intro to the React Ecosystem ##

### Video ###

**Imperative:** Telling your program how to do something

```javascript
var numbers = [4, 2, 3, 6];
var total = 0;
for (var i = 0; i < numbers.length; i++) {
	total += numbers[i];
}
```

**Declarative:** Telling your program what you want to do

```javascript
var numbers = [4, 2, 3, 6];
numbers.reduce(function(previous, current) {
	return previous + current;
});
```


## Section 2 - Setting up your first React component with NPM, Babel and Webpack ##

### First React Component ###

```javascript
var React = require('react')
var ReactDOM = require('react-dom')
var HelloWorld = React.createClass({
	render: function() {
		return (
			<div>
				Hello World!
			</div>
		)
	}
});
ReactDOM.render(<HelloWorld />, document.getElementById('app'));
```

`ReactDom.render` takes in 2 arguments. The 1st is the component you want to render, and the 2nd is is the DOM node where you want to render the component.

**JSX** simply allows us to write HTML like syntax which gets transformed to lightweight JavaScript objects. React is then able to take these JavaScript objects and from them form a “virtual DOM” or a JavaScript representation of the actual DOM.

Manipulating actual **DOM** is slow, React is able to minimise manipulations to the actual **DOM** by keeping track of a **virtual DOM** and only updating the real **DOM** when necessary.


## Section 3 - Pure Functions. f(d)=v. Props and Nesting Components. ##

### Nested Components and Props ###

**Props** is a simple system for passing data from one component to another child component.

```javascript
//Basic example of props
var HelloUser = React.createClass({
	render: function() {
		return (
			<div> Hello, { this.props.name }</div>
		)
	}
});
ReactDOM.render(<HelloUser name="Tyler" />, document.getElementById('app')); //passing name attribute
```

```javascript
//Passing attribute to a child component
var FriendsContainer = React.createClass({
	render: function() {
		var name = 'Tyler McGinnis';
		var friends = ['Ean Platter', 'Murphy Randall', 'Merrick Christensen'];
		
		return (
			<div>
				<h3> Name: { name } </h3>
				<ShowList names={ friends } />
			</div>
		)
	}
});

//Child component
var ShowList = React.createClass({
	render: function() {
		//array.map !important
		var listItems = this.props.names.map(function(friend){
			return <li> { friend } </li>;
		});
    
		return (
			<div>
				<h3> Friends </h3>
				<ul>
					{ listItems }
				</ul>
			</div>
		)
	}
});
```


### Building UIs with Pure FUnctions and Function Composition ###

`f(d)=V` A **Function** takes in some **Data** and returns a **View**

**Pure Functions**

- Pure functions always return the same result given the same arguments.
- Pure fucntion's execution doesn't depend on the state of the application.
- Pure functions don't modify the variables outside of their scope.

```javascript
//.slice is a pure function
var friends = ['Ryan', 'Michael', 'Dan'];
friends.slice(0, 1); // 'Ryan'
friends.slice(0, 1); // 'Ryan'
friends.slice(0, 1); // 'Ryan'

//.splice is not a pure function
var friends = ['Ryan', 'Michael', 'Dan'];
friends.splice(0, 1); // ["Ryan"]
friends.splice(0, 1); // ["Michael"]
friends.splice(0, 1); // ["Dan"]
```


## Section 4 - this.props.children and getting started with React Router ##

### `this.props.children` ###

`this.props.children` is a method to access specific data between opening and closing elements.


## Section 5 - Container vs Presentational Components, PropTypes, and Stateless Functional Components ##

### Stateless Functional Components ###
