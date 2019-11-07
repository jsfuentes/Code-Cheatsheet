# Intersection Observers

detecting visibility of an element, or the relative visibility of two elements in relation to each other

Allows you to register callback when element eneters or exits another element/viewport, doesn't tell you exact # of pixels or which ones but more if they intersect

```js
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0 //100% target is visible
}

let callback = (entries, observer) => { 
  entries.forEach(entry => {
    // Each entry describes an intersection change for one observed
    // target element:
    //   entry.boundingClientRect
    //   entry.intersectionRatio
    //   entry.intersectionRect
    //   entry.isIntersecting
    //   entry.rootBounds
    //   entry.target
    //   entry.time
  });
}

let observer = new IntersectionObserver(callback, options);

let target = document.querySelector('#listItem');
observer.observe(target);
```

**root** - viewport/element for checking visiblity of the target. Must be the ancestor of the target. Defaults to the browser viewport

**rootMargin** - Margin around the root before computing intersections. CSS margin values. Defaults to all zeros.

**threshold** -  what percentage visible before fired, can specify array to have multiple triggers

