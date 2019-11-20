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

- Can put any selector in string for jsss

```js
document.getElementById().getElementByTagname("input")
document.querySelector('.class')//return first
document.querySelectorAll('.class')
```

#### Get Forms

```js
document.forms
document.forms.myform
document.theform([name of form])
```

#### Doc Info

```js
window.location.href //full url
```

## Modifying Elements

#### Attributes

Can retrieve or set any attribute

```js
document.getElementById("myname").type="radio"
document.getElementById("myname").value="Jorge"
elem.style.display = 'none';
```

## Creating/Removing Elements

#### Creating

```js
const container = document.createElement("div");
container.setAttribute("id", containerId);
document.body.appendChild(container);
```

#### Deleting

```js
const container = document.getElementById(containerId);
if (container === null) return;
container.parentNode.removeChild(container);
```

## Other DOM Stuff

#### Scrolling 

```html
window.scrollBy(x-coord, y-coord);
window.scrollBy(options)
```

Options is a dict of 

- `top` i,e `y-coord`
- `left` i.e `x-coord`
- `behavior` =  `smooth`| `instant`| `auto`

