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
  render: function(){
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
