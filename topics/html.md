# HTML

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