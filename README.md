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

```jsx
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

```jsx
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

```jsx
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

```jsx
var Link = React.createClass({
	changeURL: function() {
		window.location.replace(this.props.href);
	},
	render: function() {
		console.log(this.props.children);
		return (
			<span style={{ color: 'blue', cursor: 'pointer' }} onClick={ this.changeURL }>
				{/*
					Gets values in between the <Link> tags and adds them to an array to use
					this.props.children[0] = this.props.username
					this.props.children[1] = 'children2'
					...
				*/}
				{ this.props.children } 
			</span>
		);
	}
});

var ProfileLink = React.createClass({
	render: function() {
		return (
			<div>
				<Link href={ 'https://github.com/' + this.props.username }>
					{ this.props.username } {/* Passed to Link component */}
					children2
					children3
				</Link>
			</div>
		);
	}
});
```

## Section 5 - Container vs Presentational Components, PropTypes, and Stateless Functional Components ##

### Stateless Functional Components ###

```jsx
//Components using a normal function
var HelloWorld = React.createClass({
	render: function() {
		return (
			<div>Hello { this.props.name }</div>
		);
	}
});
ReactDom.render(<HelloWorld name='Robin' />, document.getElementById('app'));

//Components using a stateless function
function HelloWorld(props) {
	return (
		<div>Hello { props.name }</div>
	)
}
ReactDOM.render(<HelloWorld name='Robin' />, document.getElementById('app'));
```

Stateless functions don't support `shouldComponentUpdate`.


### PropTypes ###

**PropTypes** is used for type checking properties that are passed into your components.

```jsx
<Icon
	name='fontawesome|facebook-square' 
	size={ 70 } 
	color='#3b5998'
	style={ styles.facebook } />

//implementing the above PropTypes
var Icon = React.createClass({
	propTypes: {
		name: PropTypes.string.isRequired,
		size: PropTypes.number.isRequired, //if string rather than integer, then console error
		color: PropTypes.string.isRequired,
		style: PropTypes.object
	},
	render: { ... }
});
```

`propTypes.func` not ~~`propTypes.function`~~ because `function` is a **reserved word**  
`propTypes.bool` not ~~`propTypes.boolean`~~ because `boolean` is a **reserved word**


## Section 6 - Life Cycle Events ##

### Life Cycle Events ###

**Lifecycle methods** are methods each component can have that allow us to hook into the views when specific conditions happen (i.e. when the component first renders, or when the component gets updated with new data, etc.)

**React's Lifecycle Methods**

1. When a component gets mounted to the DOM and unmounted
2. When a component receives new data

#### Mounting / Unmounting ####

**Mounting** is when a component is initialized and added to the DOM.  
**Unmounting** is when a component is removed from the DOM.  
Both these only happens once during the life of the component.

##### Establish some default props in our component #####

Use `getDefaultProps` method.

```jsx
var Loading = React.createClass({
	getDefaultProps: function() {
		return {
			text: 'Loading'
		};
	},
	render: function() { ... } //access 'Loading' by this.props.text
});
```

##### Set some initial state in our component #####

Use `getInitialState` method.

```jsx
var Login = React.createClass({
	getInitialState: function() {
		return {
			email: '',
			password: ''
		};
	},
	render: function() { ... }
});
```

Use `this.setState` to pass in a new object which overwrites the original properties.

##### Make an Ajax request to fetch some data needed for this component #####

Use `componentDidMount` method. Called right after the component is mounted to the DOM.

```jsx
var FriendsList = React.createClass({
	componentDidMount: function() {
		return Axios.get(this.props.url).then(this.props.callback); //using Axios (https://github.com/mzabriskie/axios)
	},
	render: function() { ... }
});
```

##### Set up any listeners (i.e. Websockets or Firebase listeners) #####

Use `componentDidMount` method.

```jsx
var FriendsList = React.createClass({
	componentDidMount: function() {
		ref.on('value', function(snapshot) {
			this.setState({
				friends: snapshot.val()
			});
		})
	},
	render: function() { ... }
});
```

##### Remove any listeners initially set up (when unmounted) #####

Use `componentWillUnmount` method.

```jsx
var FriendsList = React.createClass({
	componentWillUnmount: function() {
		ref.off();
	},
	render: function() { ... }
});
```

![React Lifecycle](https://robinjulius.com/blog/wp-content/uploads/2016/05/React-Lifecycle-1024x835.png)


## Section 7 - The `this` keyword ##

### The `this` keyword ###

`this` allows us to reuse functions with different context.

- Implicit Binding
- Explicit Binding
- `new` Binding
- window Binding

When is `this` function invoked?

#### Implicit Binding (Look left of the dot at Call Time) ####

```jsx
var me = {
	name: 'Robin',
	age: 35,
	sayName: function() {
		console.log(this.name); //Robin
	}
};
me.sayName(); //look left of the dot (i.e. me)


var sayNameMixin = function(obj) {
	obj.sayName = function(0 {
		console.log(this.name);
	}
};

var me2 = {
	name: 'Robin',
	age: 35,
};

var you2 = {
	name: 'James',
	age: 21,
};

sayNameMixin(me2); //passes 'me' object
sayNameMixin(you2); //passes 'you' object

me2.sayName(); //Robin (look left of the dot (i.e. me2))
you2.sayName(); //James (look left of the dot (i.e. you2))


var Person = function(name, age) {
	return {
		name: name,
		age: age,
		sayName: function() {
			console.log(this.name);
		},
		mother {
			name: 'Lily',
			sayName: function() {
				console.log(this.name);
			},
		}
	}
}

var jim = Person('Jim', 42);
jim.sayName(); //Jim (look left of the dot (i.e. jim))
jim.mother.sayName(); //Lily (look left of the dot (i.e. jim.mother))
```

#### Explicit Binding (call, apply, bind) ####

`call()` invokes function/method, but does not create a copy like `bind()`, instead it executes the function  
1st parameter is what this should point to, the rest is the parameters you would pass to the function

`apply()` same as `call()` but wants an array as parameters

`bind()` creates a copy of the function, and takes what should be this as the 1st parameter  
Also allows you to set default parameters, the 2nd parameter of `bind()` is the 1st parameter of the function it is bound to, 3rd parameter is 2nd, etc...

```javascript
var sayName = function(lang1, lang2) {
	console.log('My name is ' + this.name + ' and I know ' + lang1 + ', ' + lang2); 
}

var me = {
	name: 'Lily',
	age: 56
};

var languages = ['Javascript', 'PHP'];

sayName.call('stacey', languages[0], languages[1]);
sayName.apply('stacey', languages);
var newFn = sayName.bind('stacey', languages[0], languages[1]); //returns new function instead of invoking
newFn();
```

#### `New` Binding (call, apply, bind) and Window Binding ####

```javascript
//New Binding
var Animal = function(color, name, type) {
	//this = {}
	this.color = color;
	this.name = name;
	this.type = type;
}

var zebra = new Animal('black and white', 'Zorro', 'Zebra');
```

```javascript
//Window Binding
var sayAge = function() {
	console.log(this.age);
}

var me = {
	age: 35
}

sayAge(); //undefined
window.age = 35;
sayAge(); //35
```


## Section 9 - More Container vs Presentational Components ##

### `.reduce` ###

```javascript
var scores = [89, 76, 47, 95];
var initialValue = 0;
var reducer = function (accumulator, item) {
	return accumulator + item;
}
var total = scores.reduce(reducer, initialValue);
var average = total / scores.length;
```

The very first time the `reducer` function is called, it's going to be passed the `initialValue` you gave it (the 2nd argument to `.reduce`) and the first item in the actual array. So in our example above the first time that our `reducer` function runs, `accumulator` is going to be 0 and item is going to be 89. Remember, the goal is to transform an array into a single value. We currently have two numbers, 0 and 89, and are goal is to get that to one value. Because we're wanting to find the sum of every item in the array, we'll add 89 + 0 to get 89. That brings up a very important step. The thing that gets returned from the `reducer` function will then be passed as the `accumulator` the next time the function runs. So when `reducer` runs again, `accumulator` will be 89 and item will now be the second item in the array, 76. This pattern continues until we have no more items in the array and we get the summation of all of our `reducer` functions, which is 307.

```javascript
var votes = [
	'tacos',
	'pizza',
	'pizza',
	'tacos',
	'fries',
	'ice cream',
	'ice cream',
	'pizza'
]
var initialValue = {};
var reducer = function(tally, vote) {
	if (!tally[vote]) {
		tally[vote] = 1;
	} else {
		tally[vote] = tally[vote] + 1;
	}
	return tally;
}
var result = votes.reduce(reducer, initialValue) // {tacos: 2, pizza: 3, fries: 1, ice cream: 2}
```


## Section 10 - Private Functional Stateless Components ##

### Private Components ###

```jsx
var React = require('react');

function FriendsList(props) {
	return (
		<h1>Friends:</h1>
		<ul>
			{ props.friends.map((friend, index) => {
				return (
					<li key={ friend }>{ friend }</li>
				)
			})}
		</ul>
	);
}

module.exports = FriendsList;
```

Rewrite above with a `private` component for modularity

```jsx
var React = require('react');

function FriendItem(props) {
	return (
		<li>{ props.friend }</li>
	);
}

function FriendsList(props) {
	return (
		<h1>Friends:</h1>
		<ul>
			{ prop.friends.map((friend, index) => <FriendItem friend={ friend } key={ Friend } />)}
		</ul>
	);
}

module.exports = FriendsList;
```


## Section 11 - Building a Highly Reusable React Component ##

### `getDefaultProps` ###

When creating a reusable `<Loading />` component, you want the user to specify their own styles and properties. But what is some users don't want to specify custom styles and properties? You use `getDefaultProps` to specify default props in a component.

```jsx
varLoading = React.createClass({
	getDefaultProps: function() {
		return {
			text: 'loading',
			styles: { color: 'red' }
		}
	},
	render: function() { ... }
});

<Loading /> //default properties i.e. this.props.text = 'loading' and this.props.styles = { color: 'red' }

<Loading text='One second' styles={ color: 'green' } /> //this.props.text = 'One second' and this.props.styles = { color: 'green' }
```

