# Jade/Pug

## Using File in node

```js
const pug = require('pug');

// Compile the source code
const compiledFunction = pug.compileFile('test.pug');

// Render a set of data in html
console.log(compiledFunction({"name": "Tim"}));
```

In 2015, jade was renamed to pug(by Timothy Gu)

```html
<div>
  <h1>Ocean's Eleven</h1>
  <ul>
    <li>Comedy</li>
    <li>Thriller</li>
  </ul>
  <p>Danny Ocean and his eleven accomplices plan to rob
     three Las Vegas casinos simultaneously.</p>
</div>
```

Becomes

```pug
div
  h1 Ocean's Eleven
  ul
    li Comedy
    li Thriller
  p.
    Danny Ocean and his eleven accomplices plan to rob
    three Las Vegas casinos simultaneously.
```

## Fundamentals

- handles `<>` and closing tag 
- spacing indicates nesting
- `.` after tag lets you add many lines of text
- Put | to just put more text

## Attributes

- ()

```pug
div(class="movie-card", id="oceans-11")
  h1(class="movie-title") Ocean's 11
  img(src="/img/oceans-11.png", class="movie-poster")
```

class shorthand

```pug
div.movie-card#oceans-11
  h1.movie-title Ocean's 11
  img.movie-poster(src="/img/oceans-11.png")
```

## JS

Can directly use javascript with jade with `-` beginning line if no output and `=` if you want output

Can easily do loops and more with this

```pug
- var x = 5;
div
  ul
    - for (var i=1; i<=x; i++) {
      li Hello
    - }
```

#### Jade also has loops

```pug
- var droids = ["R2D2", "C3PO", "BB8"];
div
  h1 Famous Droids from Star Wars
  for name in droids
    div.card
      h2= name
```

### Interpolation

```
- var profileName = "Danny Ocean";
div
  p Hi there, #{profileName}. How are you doing?
```

## Mixins

```
mixin thumbnail(imageName, caption)
  div.thumbnail
    img(src="/img/#{imageName}.jpg")
    h4.image-caption= caption
```

 Then call it with +

```pug
+thumbnail("oceans-eleven", "Danny Ocean makes an elevator pitch.")
```

