# Other

Can have set position for scroll 

```css
.container {  scroll-snap-type: y mandatory; } .child {  scroll-snap-align: start; }
```

## Painting

### -webkit-filter

Can do blur, grayscalle, invert, hue-rotate, etc

### background-blend-mode

Sick stuff color-dodge;

## CSS Shapes

### Crop

Clip-path can even do it with a url to do like heart shape

### Curve around clip-path

shape-outside

```css
clip-path: circle(30% at 48% 36%);
shape-outside: circle(30% at 48% 36%);
```

Sick polygon shape with like curved line on one side that text follows

Chrome extension called shape editor to help ya out with complex shapes like polygons

## Calc

+, -, *, /, mod, min, max

Width: calc(50%-1em);

## Content Editable

```css
-webkit-user-modify: read-only | read-write-plaintext-only;
-moz-user-modify: ;
```

## Appearance

Can change appearance of things with -webkit-appearance. Like make an element appear like another one

## Screen Readr

If you want something to be read, but no display. Postion absolute off the page, display:none will not be read so not sol

## Font Save Space

Go to font squirrel and make font with just hte things you want

Can get only certain letters from font and have rest of font fall back

# Resize

 There is a CSS property to have resizing like a textarea, but you have to hover the bottom right which is jank

If you want it on the bottom left you can do this:

```jsx
<div className="w-full h-full flex flex-col lg:flex-row justify-center items-center overflow-hidden">
  <div className="w-full flex-1 h-full bg-pureBlack  ">
  	{innerContent}
  </div>
  <div
  className="flex flex-none h-full bg-white hidden lg:block overflow-auto resize-x"
  style={{ direction: "rtl", maxWidth: "26rem", minWidth: "20rem" }}
  >
    <div style={{ direction: "ltr" }} className="w-full h-full">
    	<EventSidebar />
    </div>
  </div>
</div>
```

