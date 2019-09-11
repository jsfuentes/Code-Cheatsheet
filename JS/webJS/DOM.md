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
let container = document.createElement('div');
container.setAttribute("id", containerID);
let iframe = document.createElement('iframe');
iframe.setAttribute("id", "ecstatic-iframe");
iframe.src = iframeUrl;
container.appendChild(iframe);

document.body.appendChild(container);
```

#### Deleting

```js
var elem = document.querySelector('#some-element');
elem.parentNode.removeChild(elem);
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

