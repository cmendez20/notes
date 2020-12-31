# JavaScript

### The Conditional (Ternary) Operator

The conditional operator, also called the ternary operator, can be used as a one line if-else expression.

The syntax is:

```javascript
condition ? statement-if-true : statement-if-false;
```

The following function uses an if-else statement to check a condition:

```js
function findGreater(a, b) {
  if(a > b) {
    return "a is greater";
  }
  else {
    return "b is greater";
  }
}
```

This can be re-written using the `conditional operator`:

```js
function findGreater(a, b) {
  return a > b ? "a is greater" : "b is greater";
}
```

### Closures

Closures are the ability for an inner function to access variables from a higher level scope even after the functions have been called or closed over. 

### Event Listeners

> Go get something, listen for something, then go do something.

```js
btn.addEventListener('click', function() {
   console.log('IT GOT CLICKED!!!'); 
});
```

### Object Reference vs Values

Objects & arrays are copied by ***reference***. 

``` js
const person1 = {
	first: 'chris',
    last: 'mendez'
};
const person2 = {
	first: 'chris',
    last: 'mendez'
}

const person3 = person1;
```

**Reference** - we are not taking a copy, we are simply creating a variable that references / points to the original variable instead of making a copy of it. person3 was never its own object, it just points to the original object. 

### How to "Shallow" Copy an Object

- only copies one level deep.

``` javascript
const person1 = {
	first: 'chris',
    last: 'mendez'
};
const person2 = {
	first: 'chris',
    last: 'mendez'
}

// use the spread operator - it spreads (like a knife) the contents from the person1 object into the new person3 object
const person3 = { ...person1 };
```

### Functional Programming

Two distinct principles for functional programming: 

1) Don't alter a variable or object - create new variables and objects and return them if need be from a function.

2) Declare function arguments - any computation inside a function  depends only on the arguments, and not on any global object or variable.

### Arrays 

- Some methods will mutate (modify) the original array and others will leave the original array intact. 
- anytime you want to use a mutation method and NOT mutate the original array, we need to take a copy of the array using the spread operator

```javascript
const numbersReversed = [...numbers].reverse();
```

- **slice()** *does not* mutate the original array
- **splice()** *will* mutate the original array

Using an arrow function shorthand and want to return an object literal? Remember to wrap your object literal in parenthesis! 

```javascript
const ratings = watchList.map(movie => ({title: movie.Title, rating: movie.imdbRating}));
```

If you don't include parenthesis, then JavaScript looks at the brackets and thinks you're just using a regular function block.

### Nested For Loops

A nested for loop for creating a 2D array is like the formula for finding the area of a 2D shape: 

`area = length * width`

### What is the DOM?

**DOCUMENT OBJECT MODEL**: Structured representation of HTML documents. Allows JavaScript to access HTML elements and styles to manipulate them (change text, HTML attributes, and even CSS styles).

- Anything that has to be in the HTML document also has to be in the DOM tree. Thus, accessible with JavaScript.

- DOM !== JAVASCRIPT

DOM Methods and Properties for DOM Manipulation are apart of WEB APIs - libraries that browsers implement and that we can interact through JavaScript code.