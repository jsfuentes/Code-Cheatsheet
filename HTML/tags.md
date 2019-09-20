# Tags

https://html.spec.whatwg.org/multipage/sections.html#the-section-element

## Div / P / Span

Could only use divs and then style as needed

A `<p>` should contain paragraghs of text, a `<div>` is to layout your page using divisions and a `<span>` allows markup to be styled slightly different, for example within a `<p>`

p and div elements are block level elements where span is an inline element and hence margin on span wont work. Alternatively you can make your span a block level element by using CSS display: block; or for span I would prefer display: inline-block;

