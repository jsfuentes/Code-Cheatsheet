# Placing Common Tasks

### Centering Div in Another Div

https://www.w3schools.com/css/css_align.asp

##### Way 1

Margin-auto & position absolute with top, bottom, left, and right  0

##### Way 2

flex justify-center items-center

## Keeping Img/Video Aspect Ratio

#### Based on width

```jsx
<div
  className="bg-blue-300 relative"
  style={{ width: "100%", paddingBottom: "100%" }}
  /* 56.25% for 9/16 ratio */
  >
  <img
    src={img}
    className="absolute object-cover w-full h-full"
  />
</div>
```

*Can set w-64 on outer div or make it adapt*

Max Img/Video based on height with cutting off?

```jsx
<div className="h-24">
	<img 
    className="object-cover w-full h-full" src={...}
  />
</div>
```

