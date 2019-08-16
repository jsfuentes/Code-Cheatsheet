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

## Measurements

`1em` - Relative to parent's font-size(16px font-size => 1em) 

`1rem` - Relative to root html's font-size

`50%` - Relative to parent container

`50vh` - Relative to viewport height (100vh is max)

`50vw` - Relative to viewport width

`100px`  - Never really use, it doesn't adapt to screen size at all

`calc(10% - 1em)` - Use calc for simple maths

## Prefixes

Browser add support for CSS features that are experimental with prefixes, used 

Webkit- (chrome/safari)

Max-
