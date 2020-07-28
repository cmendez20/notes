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