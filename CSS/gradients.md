# Gradients

Anywhere an image can be use

- liner-gradient
- Radial-gradient
- Repeating-linear-gradient(stripes)
- Repeating-radial-gradient
- (experimental conic gradients- these are sicks)

## Syntax

### Linear

```css
linear-gradient([<angle> || to <side-or-corner>,]? |<color-stop>[, <color-hint>]?, ]# <color-stop>)

background: linear-gradient(purple, gold);
/*equivalent to*/
background: linear-gradient(to bottom, purple 0%, palegoldenrod 100%);
```

Rainbow

```css
background-image: linear-gradient(
	red 0%,
	orange 20%, 
	yellow 40%,
	green 60%,
	blue 80%,
	purple 100%
)
```

#### Color-Stop

<color> [<length || <percentage]?

- percent is relative to image size, can have it be >100% or negative
- If you have same colorstop for 2 colors it will be hard stops

#### Color-hint

where do you want the mid-point between two colors

```css
linear-gradient(purple, 20%, gold)
```

#### Direction

to top | bottom | left | right | top left | top right | bottom left | bottom right

0deg, 

### Radial Gradient

```css
Radial-gradient([<shape>] || <size> at <position>]? [<color-stop>[, <colot-hint>]?, ]# <color-stop>)

background-image:
	radial-gradient(ellipse at 25% 15%,
	black 1%, 1%,
	gold 1%,
	purple 100%)
```

Shape can be `ellipse` or `circle`

Size has 2 values for ellipse and use percentages only for ellipse

Can do various positioning of circle in background with sharp edges or gradual changes, can background repeat for like spotted pattern

#### Repeated Radial Gradient

Gradient repeats in circle outward, use `at 400px` to get base size