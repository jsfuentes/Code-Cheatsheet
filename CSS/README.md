# CSS
- Mostly from frontend master by estelle.github.com/CSS-Workshop .
- CSS Level 1, 2, 3 broken in modules like 4
- Flexbox is Level 1
- Convention is top, bottom, left, right for ordering

## Including css
external is ideal, allows reusability across site
```html
<link rel="stylesheet" href="path/file.css" />`

<style>
  <!--body {}-->
</style>

<p style="color: black"> Lorem ipsum</p>
```

## Basic Selectors
Always use least specificity you need, so all li's instead of ids. Makes future use better


- #myID `<li id="myID">`
- .myClass `<li class="myClass">`
- li //element selector
- ul li //descendant selector
- ol > li //direct child selector
- li.myClass + li //adjacent sibling(closest/immediately after)
- li.myClass ~ li //matches all later siblings
- \* //all

## COLORS
3 ways

- p { color: #CCCCCC;}
- h1 { color: rgb(100,100,100);}
- div { color: rgb (20%, 50%,0);}

## Measurements

`1em` - Relative to parent's font-size(16px font-size => 1em) 

`1rem` - Relative to root html's font-size

`50%` - Relative to parent container

`50vh` - Relative to viewport height (100vh is max)

`50vw` - Relative to viewport width

`100px`  - Never really use, it doesn't adapt to screen size at all

## Prefixes

Browser add support for CSS features with prefixes like

Webkit-

Max-

## SASS

Got importing and variables with $ and modularity

