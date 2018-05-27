#### Cool Counters
Note counter has to be after it incremented
```css
body {counter-reset: sections; } // resets at section hit
:invalid { counter-increment: invalidCount; }
header h1.sectiontitle:before {
    content: "part" counter(sections) ": ";
    counter-increment: sections;
}
counter(invalidCount) " invalid entries"; }


```

## PSUEDO ELEMENTS

2 FREE Stylable Faux(Fake) Elements

```css
p:before { content: "Dogs ";}
<p>are</p>
p:after {
    content: 'cuter.'; 
}
```

Content can be:

- attr
- counter
- text
- Unicode(Emojis for example)
- Can do bottom: 10px;  and top:10px; in psuedo to add spacing and stuff outside the content

Uses:

- urls after
- depends on size of screen add content
- Ribbons, tooltips, css only icons



### Material Icons

Google made some icons that have words too, so when you make the content the icon name, it changes on the website

Shouldn't make generated content requirement of user features cuz accessibility

![PseudoElements](/Users/jfuentes/Documents/CodeCheatsheet/CSS/imgs/pseudoElements.png)

Can generate a shit ton of shapes, Im talking yin yang, diamonds, shields, everything 

