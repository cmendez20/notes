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