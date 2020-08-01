# Transitions

Can do drop down menus, flip card

Simplest

```css
a {
    color : green;
    transition: 1s;
}
a:hover { 
    color: orange;
}
```

- Transition-property: props that transition
- Transition-duration: time it takes, s or ms
- Transition-timing-function: bezier curve 
- Transition delay: time until starts (good for hover if someone just moves past it)
- Transition: shorthand for 4

## Example

```css
code {
   color: black;
   font-size: 85%;
   background-color: rgba(255,255,255,0.9);
   transition: all 2s ease-in 50ms;
}

code:hover {
   color: red;
   font-size: 120%;
   background-color: rgba(255,255,255,0.8);
}
```

50ms delay good b/c if someone drag their mouse across screen

Could also

```css
code {
   color: black;
   font-size: 85%;
   background-color: rgba(255,255,255,0.9);
   transition: all 2s ease-in 50ms;
}
code:hover {
   color: red;
   transform: scale(1.4);
   transform-origin: 0 0;
   background-color: rgba(255,255,255,0.8);
}
```

But transform change z so stuff below doesnt move

### Transition Usage

- Can transition between anything you can have a midpoint with i.e gradient values not discrete i.e font-size/opacity vs display/height auto
- Order can matter if multiple style blocks have same specificity(i.e valid/invalid and hover which applies when you hover and are valid)

### Transitionend event

Event thrown only when transition completes for every property 