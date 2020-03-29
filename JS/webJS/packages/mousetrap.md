# MouseTrap Key Bindings

Small 4.5kb minified lib

```bash
yarn add mousetrap
```

## Usage

```js
// single keys
Mousetrap.bind('4', function() { highlight(2); });
Mousetrap.bind('x', function() { highlight(3); }, 'keyup');

// combinations
Mousetrap.bind('command+shift+k', function(e) {
    highlight([6, 7, 8, 9]);
    return false;
});

Mousetrap.bind(['command+k', 'ctrl+k'], function(e) {
    highlight([11, 12, 13, 14]);
    return false;
});

// gmail style sequences
Mousetrap.bind('g i', function() { highlight(17); });
Mousetrap.bind('* a', function() { highlight(18); });

// konami code!
Mousetrap.bind('up up down down left right left right b a enter', function() {
    highlight([21, 22, 23]);
});
```

##### React

```js
useEffect(() => {
  Mousetrap.bind(OPEN_SHORTCUT, toggleSpotlight);
  () => Mousetrap.unbind(OPEN_SHORTCUT)
}, []);
```

#### Text fields

By default all keyboard events will **not** fire if you are inside of a `textarea`, `input`, or `select` to prevent undesirable things from happening.

If you want them to fire you can add the class `mousetrap` to the element.

```
<textarea name="message" class="mousetrap"></textarea>
```

