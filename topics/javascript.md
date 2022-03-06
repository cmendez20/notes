# JavaScript Notes

*JavaScript is a high-level, prototype-based, object-oriented, multi-paradigm, interpreted or just-in-time compiled, dynamic, single-threaded, garbage-collected programming language with first-class functions and a non-blocking event loop concurrency model.*

## Snippets

#### Smooth Scrolling to a Section

- not supported on ioS & Safari

```javascript
const section1 = document.querySelector('#section--1');
section1.scrollIntoView({behavior: 'smooth'});
```

#### Lazy Loading Images

**HTML**

```html
<img
    <!-- Use low-res image for src, then load high-res image with javascript using the data-src -->
	src="img/digital-lazy.jpg"
	data-src="img/digital.jpg"
	alt="Computer"
	class="features__img lazy-img"
/>
```

**JavaScript**

```javascript
// Lazy Loading Images - great for performance
const imgTargets = document.querySelectorAll('img[data-src]');

const loadImg = function (entries, observer) {
  const [entry] = entries;
  console.log(entry);

  if (!entry.isIntersecting) return;

  // Replace src with data-src
  entry.target.src = entry.target.dataset.src;
  entry.target.addEventListener('load', function () {
    entry.target.classList.remove('lazy-img');
  });

  observer.unobserve(entry.target);
};

const imgObserver = new IntersectionObserver(loadImg, {
  root: null,
  threshold: 0,
  rootMargin: '200px',
});

imgTargets.forEach(img => imgObserver.observe(img));
```

## Paradigms

- An approach and mindset of structuring code, which will direct your coding style and technique
1. Procedural programming
   - very simple, linear way to organize code with some functions
2. Object-oriented programming
3. Functional programming

## Primitive vs. Objects

- Primitive values cannot be changed - they are immutable, unchangeable, READ-ONLY
- **Variables are not values.**
  - thus, they can be changed.
- **Variables always point to values.**
  - primitive values cannot be changed.
  - we can change which value it points to by using the = assignment operator.

- You cannot pass a variable in JavaScript.

- ### Primitive values

  - undefined (undefined), used for unintentionally missing values
  - Null(null), used for intentionally missing values
  - Booleans (true and false), used for logical operations
  - Numbers (-100. 3.14, and other), used for math calculations
  - Strings ('hello', 'abracadabra'), used for text
  - Symbols (uncommon), used to hide implementation details
  - BigInts (uncommon and new), used for math on big numbers

- ### Objects and functions

  - Objects used to group related data and code
  - Functions used to refer to code

## First-Class Functions

In a language with **first-class functions**, functions are simply treated as **variables**. We can pass them into other functions, and return them from functions.

- i.e. passing a function into another function as an argument: First-class functions!
- functions are just another type of object

## Functions

- in javascript, we pass only by value. NOT REFERENCE

## The Concurrency Model

- how the JavaScript engine handles multiple tasks happening at the same time 
  - Why do we need that? 
- JavaScript runs in one **single thread**, so it can only do one thing at a time.
  - So what about a long-running task?
- Sounds like it would block the single thread. However, we want non-blocking behavior! 
  - How do we achieve that? 
- By using an **event loop**: takes long-running tasks, executes them in the "background", and puts them back in the  main thread once they are finished. 

## Hoisting in JavaScript

"Variables lifted to the top of their scope". Really, hoisting means: before execution, code is scanned for variable declarations, and for each variable, a new property is created in the variable enviornment object.

- Hoisting in JavaScript, with the `var` data type means JavaScript will declare variables first, and then give them a value later. 
  - So, to avoid weird issues, declare your variables before you use them
- With `let` and `const`, JavaScript does not hoist these
- Function statements and function declarations are hoisted.
  - Function expressions are not hoisted, treated as a let/const variable

## The Conditional (Ternary) Operator

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

## Closures

Closures are the ability for an inner function to access variables from a higher level scope even after the functions have been called or closed over. 

- closure gives our functions persistent memories and entirely new toolkit for writing professional code
- **Helper functions:** Everyday professional helper functions like 'once' and 'memoize'
- **Iterators and generators:** which use lexical scoping and closure to achieve the most contemporary patterns for handling data in JavaScript
- **Module pattern:** Preserve state for the life of an application without polluting the global namespace
- **Asynchronous JavaScript:** Callbacks and Promises rely on closure to persist state in an asynchronous environment

## THE DOM

- query selector finds children no matter how deep in the DOM tree
- the closest method finds parent no matter how far up the DOM tree

### Changing Styles

- `domElement.classList.toggle('class', condition)`
  - If the condition is included, turns the toggle into a one way-only operation.   If set to `false`, then `class` will *only* be removed, but not added. If set to `true`, then `class` will *only* be added, but not removed.    

### Event Listeners

> Go get something, listen for something, then go do something.

```js
btn.addEventListener('click', function() {
   console.log('IT GOT CLICKED!!!'); 
});
```

- `e.target` is what triggers the event dispatcher to trigger and `e.currentTarget` is what you assigned your listener to.

  #### Why you should care

  Suppose you're in a situation where you have access to an event object but not the DOM element. (In other words, no `$(this)`). If you want access to the DOM element that's associated with the event handler you defined, you should use currentTarget.

- - `target` is whatever you actually clicked on. It can vary, as this can be within an element that the event was bound to.
  - `currentTarget` is the element you actually bound the event to. This will never change.

- `this` also refers to the `e.current.target`

- `bind` method - creates a copy of the function that it is called on, and will set the `this` keyword in the function call to whatever value we pass into bind.

  ```javascript
  // Menu fade animation
  const handleHover = function (e) {
    console.log(this);
  
    if (e.target.classList.contains('nav__link')) {
      const link = e.target;
      const siblings = link.closest('.nav').querySelectorAll('.nav__link');
      const logo = link.closest('.nav').querySelector('img');
  
      siblings.forEach(el => {
        if (el !== link) el.style.opacity = this;
      });
      logo.style.opacity = this;
    }
  };
  
  // Passing "argument" into handler
  // Impossible to pass an argument to a event handler,
  // can only have one real value, the event.
  // If you want to pass more values, use the this keyword and array or object.
  nav.addEventListener('mouseover', handleHover.bind(0.5));
  nav.addEventListener('mouseout', handleHover.bind(1));
  ```

  

### The Intersection Observer API

``` javascript
const header = document.querySelector('.header');

const stickyNav = function (entries) {
  const [entry] = entries;
  console.log(entry);
  // if (!entry.isIntersecting) nav.classList.add('sticky');
  // else nav.classList.remove('sticky');
  nav.classList.toggle('sticky', !entry.isIntersecting);
};

const headerObserver = new IntersectionObserver(stickyNav, {
  root: null,
  // When 0% of the header is visible, then we want something to happen
  threshold: 0,
  rootMargin: '-90px',
});

headerObserver.observe(header);
```

#### Trying to break down what the heck is happening above for my future self.

1. In this case, we are observing the `header` element which ends up being our target element.
2. We created a new observer API when we declared the headerObserver variable and call the observe() method on it so that we can observe our target element - the header element.
   - Its first parameter is a callback function, the observer callback, the function we will call when the observer threshold is reached.
   - Its second parameter is an object known as observer options. 
     - `root` is the element that we want the target to intersect
       - We can select an element or write null (default) which means we will be able to observe our target element intersecting the entire viewport, the entire rectangle which shows the current portion of the page that is visible to the user. 
     - `threshold` is the percentage of intersection at which the observer callback will be called.
       - so if `threshold` was set to 0.1 (10%), the callback function would be called each time the observe element, the target element, is intersecting the root element (our viewport) at the threshold (10%) - no matter if we are scrolling up or down
       - The default is 0 (meaning as soon as even one pixel is visible, the callback will be run AND each time the target element moves completely out of the view
       - A threshold of 1.0 means that when 100% of the target is visible within the element specified by the `root` option, the callback is invoked.
     - `rootMargin` is used to offset the intersection root's bounding box to create the final intersection root bounds. 
       - in this case, we used the height of the navbar to move intersection root bounds up by `-90px`
3. Our observer callback function has two arguments.
   - entries
     - an array of the threshold entries (above we only have one, but sometimes could have multiple)
   - observer object 

## Object Reference vs Values

Objects & arrays are copied by ***reference***. 

```js
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

```javascript
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

## Functional Programming

Two distinct principles for functional programming: 

1) Don't alter a variable or object - create new variables and objects and return them if need be from a function.

2) Declare function arguments - any computation inside a function  depends only on the arguments, and not on any global object or variable.

## Arrays

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

![array-methods-overview](../imgs/js/array-methods-overview.png)

### Array Methods

- `pop()` method removes the last element from an array 
- `shift()` method removes the first array element and "shifts" all other elements to a lower index
- `push()` method adds a new element to an array (at the end) 
- `unshift()` method adds a new element to an array (at the beginning)
- `splice()` method can be used to add or delete elements from an array 
  - (defines the position where new elements should be added, defines how many elements should be removed, rest of the parameters are the elements you want to add (or leave blank to delete elements from an array))
- `concat()` method creates a new array by merging existing arrays

### Nested For Loops

A nested for loop for creating a 2D array is like the formula for finding the area of a 2D shape: 

`area = length * width`

## What is the DOM?

**DOCUMENT OBJECT MODEL**: Structured representation of HTML documents. Allows JavaScript to access HTML elements and styles to manipulate them (change text, HTML attributes, and even CSS styles).

- Anything that has to be in the HTML document also has to be in the DOM tree. Thus, accessible with JavaScript.

- DOM !== JAVASCRIPT

DOM Methods and Properties for DOM Manipulation are apart of WEB APIs - libraries that browsers implement and that we can interact through JavaScript code.
