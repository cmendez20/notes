# Selectors 

##### Selector specificity 

(Inline, IDs, Classes, Elements)

Goes through selector and see what it has from left to right. 

(0, 0, 0, 0)

`nav#nav div.pull-right .button {`

`	background-color: green;`

`}` 

has a specificity of (0, 1, 2, 2)

`#nav a.button:hover {`

`	background-color: yellow;`

`}` 

has a specificity of (0, 1, 2, 1). Therefore, the button's background color will be green since it wins out at the elements specificity. 

##### Reminders

- a selector that contains 1 ID is more specific than one with 1000 classes
- a selector that contains 1 class is more specific than one with 1000 elements
- The universal selector * has no specificity value (0, 0, 0, 0)
- rely more on specificity than on the order of selectors
  - allows you to rearrange things in the future, thus, scalable 
- But, rely on order when using 3rd-party stylesheets - always put your author stylesheet last. 