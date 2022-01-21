# Overflow

Control what happens when content too big either scroll/clip

- `visible` - Default. The overflow is not clipped. The content renders outside the element's box
- `hidden` - The overflow is clipped, and the rest of the content will be invisible
- `scroll` - The overflow is clippgit ed, and a scrollbar is added to see the rest of the content
- `auto` - Similar to `scroll`, but it adds scrollbars only when necessary

Only happens if block display with height

The scrollbar actually takes up space in the div

**Make sure container is overflow hidden** so it constrains the inner divs, then you can add auto(scrollbar) to the child

## Text-Overflow

```css
overflow: hidden;
white-space:nowrap;
text-overflow: hidden;
```

## Advanced

On mobile, you can run into weird bouncing issues with the window scrolling instead of the content

Check out: https://developer.mozilla.org/en-US/docs/Web/CSS/overscroll-behavior