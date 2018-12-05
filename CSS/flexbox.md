# Flexbox

Flexbox can do stuff like same size box and pop things up and down and navigation changes position. Flexbox default has next line be longer and can have empty boxes, if you dont want that then grid

```css
body > div {
    height:200px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
div > div {
    flex: 10%;
}
```



## Components

1. Creation - display
2. Direction: flex-flow(row/column & wrapping) (flex-direction, flex-wrap)
3. Alignment: justify-content, align-items, align-self, align-content
4. Ordering: order
5. Flexibility: flex(flex-grow, flex-shrink, flex-basis) change proportional to other shit

## Steps

1. Add `display: flex;` to the parent of elements
2. Set `flex-direction`to horizontal or vertical
3. Set `flex-wrap` to control wrap direction

## Display

flex: (can it grow) (can it shrink)

## What is a Flex Item?

All none-absolute child of display: flex

#### Impacted CSS Properties

ignore column, float, clear, vertical-align

Change minwidth&height default is auto not 0

Change visibility to collapse

Change margin: 

## Flex Container

### Flex-direction

Row is like in 1 row:  a | b | c

```css
body > div {
    display: flex;
    flex-direction: row;
}
```

- row(default)
- row-reverse
- column
- Column-reverse 

Special Cases: 

- Reverse actually doesn't change order for screen readers
- Change languages to right to left changes order of columns or rows 

SO, have flex column of nav bar, main page, and footer, then in main page have flex row, in each flex row have flex columns etc etc...

**main axis** is like along one row is direciton is row

**cross axis** is perpedential to main axis

### Flex-wrap

- nowrap(default)
- wrap
- wrap-reverse(changes cross axis direction) 

### Flex-flow 

shorthand for warp&dir

```css
flex-flow: column-reverse wrap-reverse;
```

## Flex Item from Container

### Justify-content

Aligns flex items along the main axis if sum of flex items doesn't equal container

- Flex-start(group at main-start)
- Flex-end(group at main-end)
- center(group at center)
- space-between(put 1st and last in place and everything evently spaced)
- space-around(same margin of space around each item)
- Space-evenly(same amount of space between each item)

### Align-content

Only applies to organization of multiple-line stuff along cross axis, how each line is displayed

### Align-items

align flex items along cross axis within line

- flex-start(group at cross-start)
- flex-end(group at cross-end)
- center(center of max)
- baseline(header bottom all perfectly aligned)
- stretch(every item stretchs to max)

## Flex-Items Individual Properities

### Align-self

Override align item for an individual item, same properities

- auto is new prop that means what parents says to do

### Order

default value is 0, depending on given values organizes in ascending order -1 0 1 where 0 is done by markup

## Flexibility

Grow shrink and be the right size

Flex is shorthand, but made up of

- **flex-grow**: how to divide extra space, given to anything with value greater than 0 proportionally on this value(default: 1)
- **Flex-shrink**: how to shrink if there's not enough room, shrink based on this value(default: 1)
- **Flex-basis**: the starting size before free space is distributed; length value(px, em), content, or auto; 0 divides all space, auto depends on content

```css
.item:nth-of-type(odd) {
    flex: 1 0 220px; //220px base and grow if extra pixels
}
.a, .b {
    flex: 2; //2 0 0px; so a grows much
}
.c {
    flex: 1;
}
//if 1000px total, a&b would be 400px and c would be 200px
```

Will never shrink to less than longest word

