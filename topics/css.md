# Selectors 

## Selector specificity  

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

## Reminders

- a selector that contains 1 ID is more specific than one with 1000 classes
- a selector that contains 1 class is more specific than one with 1000 elements
- The universal selector * has no specificity value (0, 0, 0, 0)
- rely more on specificity than on the order of selectors
  - allows you to rearrange things in the future, thus, scalable 
- But, rely on order when using 3rd-party stylesheets - always put your author stylesheet last. 

## Padding

the parent's width is always the reference for percentage-based calculations  

length w/ em unites uses the current element for computed font-size, reference is current element. 

## CSS Value Processing: What You Need To Know

- Browsers specify a root font-size for each page (usually 16px)
- Percentages and relative values are always converted to pixels
- Percentages are measured relative to their parent's font-size, if used to specify font-size
- Percentages are measured relative to their parent's width, if used to specify lengths
- em are measured relative to their parent font-size, if used to specify font-size
- em are measured relative to current font-size, if used to specify lengths 
- rem are always measured relative to the document's root for *font-size*
- vh and vw are simply percentage measurements of the viewport's *height* and *width*

## Inheritance: What You Need To Know

- inheritance passes the values for some specific properties from parents to children - more maintainable code
- properties related to text are inherited: *font-family*, *color*, etc.
- the computed value of a property is what gets inherited, not the declared value
- Inheritance of a property only works if no one declares a value for that property
- The *inherit* keyword forces inheritance on a certain property
- The *initial* keyword resets a property to its initial value

## The Box Model

- Content: text, images, etc.
- Padding: transparent area around the content, inside of the box
- Border: goes around the padding and the content
- Margin: space between boxes;
- Fill Area: area that gets filled with background color or background image

## The Box Model: Heights and Widths

**total width** = right border + right padding + specified width + left padding + left border

**total height** = top border + top padding + specified height + bottom padding + bottom border 

**example**: height = 0 + 20px + 100px + 20px + 0 = 140px

Box-sizing: border-box fixes this by just going by our specified height/width.

## Think, Build, Architect

- Think
  - Layout, Atomic Design
- Build
  - BEM
- Architect
  - The 7-1 Pattern
  - 7 different folders for partial Sass files, and 1 main Sass file to import all other files into a compiled CSS stylesheet. 
    - **base/** (where we put the basic product definitions)
    - **components/** (where we have one file for each component)
    - **layouts/** (where we define the overall layout of the project)
    - **pages/** (where we have styles for specific pages of the project)
    - **themes/** (if you want to implement different visual themes)
    - **abstracts/** (where we put code that doesn't output any CSS, such as variables or mix-ins)
    - **vendors/** (where all third-party CSS goes)

## BEM: Building with Meaningful Class Names

- Block Element Modifier
  - .block {}
  - .block__element {}
  - .block__element--modifier {}
- **BLOCK:** standalone component that is meaningful on its own. (btn)
- **ELEMENT:** part of a block that has no standalone meaning. (btn-description)
- **MODIFIER:** a different version of a block or an element. (btn-round)

## Node & NPM

- npm init
- npm install node-sass --save-dev
  - in order to save it as a development dependency here in our package .json file. Which means that it's a development tool that will just help us in building our project. 
  - We save it in the package.json file so that we can share our project without sharing the entire node modules
    - then if someone receives the json and does `npm install`, they can download all the necessary files to run our project. 

## SASS (SCSS)

- I will be using SCSS which stands for Sassy CSS, slight different syntax than SASS
- - variables: `$primary-color: #ddd;`
  - mix-ins
  - extends
- SCSS file extension
  - to write SCSS, Sassy CSS, you must use .scss files extensions, not SASS
  - **easy to convert CSS to SCSS because valid CSS is valid SCSS.**
- Compiling SASS
  - to compile sass, add a script to your package.json file.
  - the script looks something like this:
    - `"compile:sass": "node-sass sass/main.scss css/styles.css"`
    - then, run `npm run compile:sass` in your terminal and watch the magic unfold.
    - to explain the script a little bit, the second path is the location to your sass file, and the last is where you want the compile sass to output to.
  - to install live-server: only have to do it once, to run it just type `live-server` in the project home folder terminal. 
    - npm install live-server -g

## REVIEW: Basic Responsive Design Principles

1. Fluid Grids and Layouts

   To allow content to easily adapt to the current viewport width used to browse the website. Uses % rather than px for all layout-related lengths. 

2. Flexible/Responsive Images

   Images behave differently than text content, and so we need to ensure that they also adapt nicely to the current viewport.

3. Media Queries 

   To change styles on certain viewpoint widths

## Layout Types

- Float Layouts 
- Flexbox 
- CSS Grid

## Flexbox

- The main idea behind flexbox is to give the container the ability to expand and to shrink elements to elements to best use all the available space
- Flexbox replaces float layouts, using less, and more readable and logical code
- Flexbox completely changes the way that we build one-dimensional layouts 

## Main Flexbox Concepts

- the element that we use flexbox on is called the flex container 
- all the direct children in a flex container are called flex items
- the direction the flex items are laid out across is called the main axis (going across)
- perpendicular to that is called the cross axis (going down)

## Flexbox Properties Overview

- **Container**
  - **bold items is default value**
  - flex-direction: **row** | row-reverse | column | column-reverse 
  - flex-wrap: **nowrap** | wrap | wrap-reverse 
  - justify-content (main-axis): **flex-start** | flex-end | center | space-between | space-around | space-evenly 
  - align-items (cross-axis): **stretch** | flex-start | flex-end | center | baseline
  - align-content: **stretch** | flex-start | flex-end | center | space-between | space-around
    - only applies when there is more than one row of flex items
    - controls how the rows are align along the cross axis if there is some empty space
- **Item**
  - align-self: similar to align-items, but for one individual flex item 
  - order: defines the order in which one specific flex item should appear
  - flex-grow: how much an item can grow
  - flex-shrink: how much it can shrink
  - flex-basis : it's basically the width property for flex-items
  - flex-shrink: 1 (The flex-item is allowed to shrink as the viewport shrinks)
  - flex-shrink: 0 (The flex-item is not allowed to shrink down. )
  - flex-grow: 1 (allows element to take up as much space as it can)
  - flex-grow: 0 (does not allow element to grow)
  - flex: flex-grow flex-shrink flex-basis

## Responsive Images

- To make responsive images, format the img element. 
  - always declare a width and height in percentages so that the image is fluid.
  - image should be displayed as block, so that there is no small space beneath image.

## CSS Grid

- CSS Grid replaces float layouts, using less, and more readable and logical CSS and HTML
- CSS Grid works perfectly together with Flexbox, which is best to handle one-dimensional components and layouts 
- CSS Grid completely changes the way that we envision and build two-dimensional layouts 

![CSS Grid Properties Overview](../imgs/css/css-grid-overview.png)

## THE CALC FUNCTION TO THE RESCUE 

- use calc(100vh - whatever height of navbar to make a complete 100vh experience for landing page.
- ex: calc (100vh - 6 rem)

## Consistent Margins with Type

- for consistency, often we "turn off" the margin-top on typography related elements.
- That way we can use padding on the parent, and know the exact spacing that we'll have, and can keep all sides consistent.

## In-line & Block elements

#### Block Elements

Block level elements will create a new line of content, stacking on top of each other by default.

default width: 100%

default height: 0, but will grow to the height according to the content in them.

- paragraphs
- headings
- lists and list items
- div
- header
- footer
- main
- section
- etc.

#### Inline elements

Inline elements stay within the flow of what's around them.

- links
- strong
- em
- span
- Images (sort of)

There are some important things to know about inline elements:

- you can only nest other inline elements in them (such as putting a link inside a strong element) (you cannot put a div inside a span element)
- They will only respect margin, padding, and borders which are placed on the left or the right side, and not the top and bottom.
  - you CANNOT set a width or a height on an inline element

## The Span Element

There is a very useful inline element, called a span

- the span element is like strong and em, in that we use it to style text, but it has no default styling and no semantic meaning
- a span by itself is a little useless, normally we use a class on them to make it easy to target with class

## Styling Links

Links have different "states" that we can style as well

- default "link" state

  `a { color: yellow;}`

- Visited Links
- Focus (navigating a website by keyboard)
- Hover
- Active (the style while you're actively clicking on the link)

We can target these different states by using something called a pseudo-class

- a: link
- a:visited
- etc. 

Important to note specificity of a:psudo classes selectors. For instance, an active pseudo class will not work if above a:link. 

```
a:link,
a:visited {
  color: #FFE600;
}

a:focus {
  color: aquamarine;
}

a:hover {
  color: firebrick;
}

a:active {
  color: plum;
}
```

**if you do**

`a:hover { color: aqua; }`

**it controls all of your link states**

Finally, make sure to always include styles for :focus, it can be added to the hover pseudo class.

## Inline-block

Sometimes we need something which can stay inline, but which we can set margins and padding on.

`display: inline-block`

Mostly used for buttons.

### CSS Units

#### Absolute 

- pixels 

#### Percentages 

- When using percentages, that percentage is always relative to its parent. 
  
- A lot of the time, that parent is going to default to 100%
  
- responsive images: 

  `set width to 100%`

## Max & Min Width

- max-width
  - set to keep container size at a set size while on big screens, but allows the content to shrink in smaller screens
- min-width
  - minimum width were the container will never shrink below the smallest size
- max/min width are different values than width

## How to decide which CSS unit to use

General rule of thumb:

- Font-size = rem
- padding and margin = em
- Widths = em or percentage

## Media Queries

- Media queries let us add new styles that target only specific conditions

`@media media-type and (media-features) {...}`

- The media-type let's us target different types of media
  - Screen `@media screen {...}`
  - Print `@media print {...}`
  - Speech `@media speech {...}`

- The media condition let's us target specific conditions within that media type
  - Widths `@media (min-width: 600px) {...}`
  - Orientation `@media (orientation: landscape) {...}`
  - Specific features `@media (hover) {...}`
-  Both media types and conditions are optional
- We do need to either have a type or condition though
- For example, we can target only screens
  - `@media screen {...}`
-  You can combine a type with a condition by using and:
  - `@media screen and (min-width: 960px) {...}`

