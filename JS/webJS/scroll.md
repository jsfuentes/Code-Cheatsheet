# Scroll

```typescript
element.scrollIntoView();
element.scrollIntoView(alignToTop); // Boolean parameter
element.scrollIntoView({
          behavior: "smooth",//auto or smooth
          block: "end",//vertical alignement: start, center, end, nearest
          inline: "nearest", //horizontal alignement: start, center, end, nearest
        });
```

## Scroll Into View Moves Entire Page

```js
        itemR.current.parentElement.scroll({
          top: itemR.current.offsetTop,
          behavior: "smooth",
        });
```

