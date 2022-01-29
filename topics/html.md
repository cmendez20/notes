# HTML Notes

## Semantic HTML Structure

- Both the `<article>` and `<section>` elements contribute to a document’s structure and help to outline a  document. If the content is being grouped solely for styling purposes  and doesn’t provide value to the outline of a document, use the `<div>` element.

- If the content adds to the document outline and it can be independently redistributed or syndicated, use the `<article>` element.

- If the content adds to the document outline and represents a thematic group of content, use the `<section>` element.'

### Headings

- Based on importance, not size

## Accessibility

-  if an image doesn’t have a meaningful value—perhaps it is part of the  user interface, for example—it should be included as a CSS background  image if at all possible, not as an `<img>` element.

## Navbar HTML Structure

- Can place `index.html` into a folder titled based on the name of the url you want. It makes the url slug look cleaner. 

```html
<nav role = "navigation" aria-label="main menu">
	<ul class="navbar">
        <li><a href="/">Home</a></li>
        <li><a href="/people">People</a></li>
        <li><a href="/prices">Prices</a></li>
        <li><a href="/contact">Contact</a></a></li>
    </ul>
</nav>
```

## The Box Model Fix

```css
/* border box fix */
html {
	box-sizing: border-box;
}

*, *:before, *:after {
    box-sizing: inherit;
}
```

## Clearing Floats

### The Clear Property

Used to return elements to the normal flow after an element has been floated

### "Clearfix" Hack

```css
/* Add this class to the parent of the floated element html" */

.clearfix:after {
	content: "";
	display: table;
	clear: both;
}
```

```html
<div class=".clearfix">
    <img src="pictures.jpg" alt="floated image">
    <p>lorem ipsum</p>
</div>
```

### display: flow-root

```css
/* only supported on newer browsers, add this css property to the parent of the floated element */
display: flow-root;
```

> Depending on where your element is floated, you may need to clear the float on the next element if one exists in the layout. If one doesn't exist, then self-clear the float on the parent element.

## Styling Forms

### The input tag

- A label’s `for` attribute must match the `id` attribute of its associated `<input/>` element.
  - this helps for 
- When styling input tags, be very specific by targeting the input's attribute using the attribute selector:

```css
.form-row input[type='text'],
.form-row input[type='email'] {
  background-color: #FFFFFF;
```

- Again, we don’t want to use a plain old `input` type selector here because that would style *all* of our `<input/>` elements, including our upcoming radio buttons and checkbox. This is part of what makes styling forms tricky. Understanding the CSS to pluck out exactly the elements you want is a crucial skill.

### Radio Buttons

Every radio button group you create should:

- Be wrapped in a `<fieldset>`, which is labeled with a    `<legend>`.
- Associate a `<label>` element with each radio button.
- Use the same `name` attribute for each radio button in the    group.
- Use different `value` attributes for each radio button.

```html
<fieldset class='legacy-form-row'>
  <legend>Type of Talk</legend>
  <input id='talk-type-1'
         name='talk-type'
         type='radio'
         value='main-stage' />
  <label for='talk-type-1' class='radio-label'>Main Stage</label>
  <input id='talk-type-2'
         name='talk-type'
         type='radio'
         value='workshop'
         checked />
  <label for='talk-type-2' class='radio-label'>Workshop</label>
</fieldset>
```

- Cannot use flexbox or grid to position/style radio buttons. Must use float.

### Checkboxes

- Checkboxes are sort of like radio buttons, but instead of selecting only one option, they let the user pick as many as they want. 
  - This simplifies things, since the browser doesn’t need to know which checkboxes are part of the same group. 
- In other words, we don’t need a `<fieldset>` wrapper or shared `name` attributes.