# HTML Content Box

![Box model with margin border and padding](https://mdn.mozillademos.org/files/13647/box-model-standard-small.png)

### Padding

```css
/* Apply to all four sides */
padding: 1em;

/* vertical | horizontal */
padding: 5% 10%;

/* top | horizontal | bottom */
padding: 1em 2em 2em;

/* top | right | bottom | left */
padding: 5px 1em 0 2em;
```

### Margin

```css
/* Apply to all four sides */
margin: 1em;
margin: -3px;

/* vertical | horizontal */
margin: 5% auto;

/* top | horizontal | bottom */
margin: 1em auto 2em; 

/* top | right | bottom | left */
margin: 2px 1em 0 auto;
```

### Border

See own section

## More

Margin and Padding can be negative :0

#### Box-Shadow

```css
box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 50px;
```

#### Box-sizing

**Content-box** | border-box

- Does the width you declare about the content or the content with padding? 
- So does padding add to width or within width. Border-box would say within, default is content-box