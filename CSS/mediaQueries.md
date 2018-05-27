# Media Queries

Originally had 10 types of browsers that you can ask what is displaying this shit

Problem: Different Sizes

Solution: IF something is something has this size, use this css; If something is landscape, send this css

Don't think about devices, think about sizes that make sense for your design

###  Specifying Media Queries

```css
@media screen and (max-width: 600px) {
    selector {
        
    }
}
```

OR can put directly in linking tag

```html
<link rel='stylesheet' media='screen and (min-width: 320px) and (max-width: 480px)' href='css/smartphone.css' />
```

### Properties

Use min and max or it will just be for that one pixel

- (min/max)-width:
- (Min/max)-height:
- Orientation: potrait(h>w) | landscape(w>h)
- (min/max)-resolution: 72dpi | 100dpcm
- (min/max)-aspect-ratio: 
- …..
- **Media feature: hover** does the primary input mechanism allow the user to hover over elements

### Resolution Units

dpi: dots per inch(72, 96 serve higher rez images)

Dlcm: dots per centimeter(1dpcm = 2.54dpi)

Dppx: dots per pixel(1dppx=96dpi default image rez)

#### Syntax

New >= < > like @media (width > 600px)

Can use and, not, and ',' which is or

`media='only screen and (color)'

`media='print, not screen and (color)' //p or not (s & c)

```css
@supports (display: flex) {//(properties: value) 
    
}
```

## Viewport

**SUPER IMPORTANT** use this line of CODE at the top of all your files

```css
@viewport {
    width: device-width; zoom: 0.5;
}
```

