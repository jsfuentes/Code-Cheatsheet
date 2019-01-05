# SVG Graphics

XML language, style through CSS, images, scriptable(animatable)

## Primatives

- `<svg>`
- `rect`, `circle`, `line`, `text`, `polyline` all selfclosing except text i.e `<line ... />`
- `style` declarations
- `g` creates groups
- `xlink:href` copy instance

### Example

```html
<svg width="600" height="400" style="background: #93A1A1">
	<line x1="0" y1="200" x2="600" y2="200" style="stoke: #268BD2; stroke-width: 40px" />
    <g id="triangle">
    	<polyline
          points="10 35, 30 10, 50 35"
          style="fill: #F7B330" 
        />
    </g>
    <use xlink:href="#triangle" x="30" y="0" />
</svg>
```

