# DOM Control

## Selecting elements

#### JQuery

```js
$( '#header' ); // select the element with an ID of 'header'
$( 'li' );      // select all list items on the page
$( 'ul li' );   // select list items that are in unordered lists
$( '.person' ); // select all elements with a class of 'person'
```

#### Document

```js
document.getElementById().getElementByTagname("input")
document.querySelector('.class')
document.querySelectorAll('.class')
```

## Get Forms

```js
document.forms
document.forms.myform
document.theform([name of form])
```

## Attributes
Can retrieve or set any attribute

```js
document.getElementById("myname").type="radio"
document.getElementById("myname").value="Jorge"
```

### Other stuff

#### Scrolling 

```html
window.scrollBy(x-coord, y-coord);
window.scrollBy(options)
```

Options is a dict of 

- `top` i,e `y-coord`
- `left` i.e `x-coord`
- `behavior` =  `smooth`| `instant`| `auto`

