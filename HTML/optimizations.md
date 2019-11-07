# Optimizations

### Preconnect to Required Origins

`<link rel="preload">` informs the browser that a resource is needed as part of the current navigation, and that it should start getting fetched as soon as possible.

Edge cases b/c this isnt a hint it mandates the browser grabs it

```html
<link rel="preload" as="script" href="super-important.js">
<link rel="preload" as="style" href="critical.css">
```

Should be used within 3 seconds

##### Preconnect

Easy to manage

```html
<link rel="preconnect" href="https://example.com">
```

 pretty cheap; should be used within 10 seconds

Can save like .3ms