# Grid

## Basic

CSS

```css
.app {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 4em 1fr 1fr 1fr 4em;
  grid-template-areas:
    "header header header"
    ". top ."
    ". main ."
    ". bottom ."
    ". . .";
  width: 100vw;
  height: 100vh;
}

/* Give every child element its grid name */
.header {
  grid-area: header;
  background-color: white;
  box-shadow: 0px 0.5px 2px rgba(0, 0, 0, 0.05);
}

.main {
  grid-area: main;
  background-color: gray;
  display: flex;
  justify-content: center;
  align-items: center;
}

.top {
  grid-area: top;
}

.bottom {
  grid-area: bottom;
}
```

HTML

```react
<div className="app">
  <div className="header">
    <div> Header </div>
  </div>
  <div className="top">Top</div>
  <div className="main">
    <div> Dashboard </div>
  </div>
  <div className="bottom">Bottom</div>
</div>
```

## Comparison to Grid

Flexbox is 2D layout, all the rows are independent, would be hacky if you want all the elements in each row to line up 

Basically in every browser now

Grid also much **more powerful** and can specify an item can take up more rows/columns across multi rows/columns

i.e in flex box 

1 | 2 | 3

4 | 5 | 6

7    |    8

Vs. grid 

1 | 2 | 3

4 | 5 | 6

7 | 8

## Vocab

- **Grid lines**: line at left and right of grid and between each row, so 3*3 has 4 horizontal grid lines & 4 vertical grid lines; 1-4 
- **Grid cell**: any cell
- **Gutter**: Grid Gap
- **Grid Track**: Either row or col

## Setting Up the Grid

### Properties on Parent

- display

- grid-template-columsn

- Grid-template-rows

- Grid-template-areas

- grid-template(shorthand)

- Grid-column-gap

- Grid-row-gap

- Grid-gap

- --------------------------------

- Justify-items

- align-items

- justify-content

- align-content

- grid-auto-columns: none | <track-list> | <auto-track-list>

- grid-auto-rows: none | <track-list> | <auto-track-list>

- grid-auto-flow

- Grid

Track List is that `1fr 1fr 1fr 1fr` thing

### Creation

Default is one cell on each row, all children of display grid are grid elements

```css
div {
    display: grid | inline-grid; 
    // inline-grid just how long it needs to be, basically width: auto according to content
}
```

```css
ol {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    list-style-type: none;
}
```

`repeat(4, 1fr)` == `1fr 1fr 1fr 1fr` : gives 4 columns and give every item 1 unit of free space(fraction unit)

## Grid-template-Columns & rows

```css
grid-template-columns: 
	150px 150px 150px;
	repeat(3, 8em);
	100px repeat(2, 1 fr) 2fr;
	2fr 125px minmax(300px, 3fr);
```

#### Values

- length or percentage
- flex: fr
- max-content
- min-content
- minmax(min, max)
- auto
- Fit-content

Number of entries is number or rows/columns; mix units at will

Row is the dynamic one that often goes beyond/under the expected amount

Use auto if you want it to fill up available space(like if you want articles to be their size and footer to be small)

#### Naming Grid Lines

Grid-template-columns: [start] 150px 150px 150px [end];

Basically putting brackets between col width definitions

Can then use these names in propereties like grid-area

```css
ol {
    Grid-template-columns: [start] 150px 150px 150px [end];
}

.myItem {
    grid-area: 2 / start/ 4 / mid;
}
```

Can use the same name multiple times, then the closest gridline is used(start every 3rd and does closest)

## Gutters

- Grid-column-gap: between each col
- grid-row-gap: between each row
- grid-gap(shorthand): <row> <col>; or <row and col>;

Only a single size for each axis, margin/padding still works for each list element and change entire grid layout

## Positioning

To place item, say where grid-line starts and which gridline it ends

If you want empty grid boxes, position everything

```css
.myItem {
    grid-row-start: 2;
    grid-row-end: 4;
    grid-column-start: 2;
    grid-column-end: 5;
}
.myItem {
    grid-row: 2 / 4;
    grid-column: 2 / 5; 
    /*could also do 5 / 2 
    2 would be 1 col wide*/
}
.myItem {
    grid-area: 2 / 2 / 4 / 5;
    /*grid-row-start / grid-col-start / grid-row-end / grid-col-end*/
}
```

### grid-template-areas

Describe grid with named areas instead of numbers 

```css
body {
    "header header header"
    "nav article aside"
    "footer footer footer"
}

header {
    grid-area: header;
}

nav {
    grid-area: nav;
}
/*etc....*/
```

## Alignment

Parent

- justify-items
- align-items
- justify-content
- align-content
- grid-auto-columns
- grid-auto-rows
- Grid-auto-flow: shorthand of two above
- grid

Item

- justify-self
- Align-self

### Justify-Items

legacy | safe | unsafe| same as flexbox too i.e left| center| flex-start

- align items in inline direction(horizontal), along columns
- Safe: if it overflows still show 
- Unsafe: even if overflows, listens to grid

### Align-Items

Align along row track, vertical alignment

### PlaceItems: <align-items> <justify-items>

### Justify & Align Content

- Only matters if you have extra space within grid
- Same values as flex-box, aligns entire rows and columns within grander grid
- Align again is row spacing, justify is col spacing

### Grid-auto-****

```css
grid-auto-columns: 100px;
```

Any col that is added is 100px 

#### Advanced

If you use 1fr, content that is too big will make the content bigger than the grid. Use minmax(0, 1fr) instead, something about how the min and max are both 1fr which is auto so content size. 