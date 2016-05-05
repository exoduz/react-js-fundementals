# React.js Fundementals #
##### http://courses.reactjsprogram.com/courses/reactjsfundamentals #####

## Section 1 - Intro to the React Ecosystem ##

### Lecture 2 - Video ###
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
