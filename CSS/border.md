#Border

Borders can down into triangle of top part, so height & width of 0 and border width of 10px and only top red would create triangle. 

Border

- -color: 
- -style
- -width
- -radius
- border

## Border-color

currentcolor default, any color you want

## border-style

dotted | dashed | solid | double | groove | ridge | inset | outset | hidden | none

default is none 

## border-width

(length) | thin | medium | thick

TRouBLe order(top right bottom left)

## border shorthand

```css
border: width style color;
/* style is required, width is medium, color is currentcolor */
border-left: 5px dashed rgba(217, 68, 11, 0.5);
```

## border-radius

Adds rounded corners, color lines will stay  pointing to corner

```css
Border-radius: 20px;
Border-radius: 50%;
/* circle(if equal h&w) */
border-radius: 10px 20px; 
/* upper left and lower right have 10px radius, upper right and lower right have 20px; */
border-radius: 10px / 20px; 
/*horizontal 10px, vertical 20px*/
```

## border-image

Must have border

```css
border-image: source || slice / width / outset || repeat;
border-image: url(gradient.png 32 / 12px stretch)
```

The corners are put in the corners and the center is stretched