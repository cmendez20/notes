# JavaScript Principles

### Thread of Execution

When JavaScript code runs, it:

- Goes through the code line-by-line and runs/'executes' each line - known as the **thread of execution**

- Saves 'data' like strings and arrays so we can use that data later - in its **memory**
  
  - We can even save code ('functions')

### Functions

Functions are code we save ('define') functions & can use (call/invoke/execute/run) later with the function's name & ( )

- **Execution content** : Created to run the code of a function - has 2 parts.
  
  - Thread of execution (where JS goes line-by-line to run the code)
  
  - local Memory  

### Call Stack

- JavaScript keeps track of what function is currently running (where's the thread of execution)

- Run a function - add to call stack

- Finish running the function - JS removes it from call stack

- Whatever is top of the call stack - that's the function we're currently running

### Generalized Functions

**Why do we even have functions?** ()Let's see why....)

- Create a function 10 squared 
  
  - takes no input
  
  - returns 10 * 10
  
  ```javascript
  function beSquared () {
    return 10 & 10;
  }
  ```

- DRY (Don't Repeat Yourself)

- *We can generalize the function to make it reusable*

```javascript
function squareNum(num) {
  return num * num;
}
```

  


