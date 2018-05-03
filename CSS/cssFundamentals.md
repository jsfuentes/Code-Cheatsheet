# CSS
- Mostly from frontend master by estelle.github.com/CSS-Workshop .
- CSS Level 1, 2, 3 broken in modules like 4
- Flexbox is Level 1

## Including css
external is ideal, allows reusability across site
```html
<link href="stylesheet" href="path/file.css" />`
<style>
  body {}
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

## Px vs Em
he `em` is a scalable unit that is used in web document media.
em is a unit that is relative to the currently chosen font size.
% is also a relative unit, in this case relative to either the height or width of a parent element. They are a good alternative to px units for things like the total width of a design, if your design does not rely on specific pixel sizes to set its size.

Using % units in your design allows your design to adapt to the width of the screen/device, whereas using an absolute unit such as px does not.
