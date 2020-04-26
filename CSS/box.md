# HTML Content Box

### Padding

```css
/* Apply to all four sides*/
padding: 1em;
/* vertical | horizontal*/
padding: 5% 10%;
/* top | horizontal | bottom*/
padding: 1em 2em 2em;
/* top | right | bottom | left*/
padding: 5px 1em 0 2em;
```

By default, padding ADDS to the declared dimensions(see below)

Can have negative margin, but not negative padding

### Margin

```css
/* Same as padding */
margin: -3px;
margin: 5% auto;
margin: 1em auto 2em; 
margin: 2px 1em 0 auto;
```

Margin is collapsable. So if divs stacked and top has margin-bottom: 40px and bottom one has margin-top 30px. Space between them will be 40px

Margin-auto horizontal centers div if it has set width

### Border

See own section

## Overview

![Box model with margin border and padding](https://mdn.mozillademos.org/files/13647/box-model-standard-small.png)

Margin and Padding can be negative :0

### Box-sizing

(Padding and Border within or outside declared width/height?

**content-box**  => outside

**border-box**  => Within

### Box-Shadow

```css
box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 50px;
```

## Center a Div 

https://www.w3schools.com/css/css_align.asp

