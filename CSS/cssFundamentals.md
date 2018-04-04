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
