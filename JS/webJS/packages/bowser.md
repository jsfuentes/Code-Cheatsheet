# Bowser

Detect user-agent, [full list](https://github.com/lancedikson/bowser/blob/master/src/constants.js)

```js
const browser = Bowser.parse(window.navigator.userAgent);
const isValidBrowser = browser.satisfies({
  // declare browsers per OS
  windows: {
    "internet explorer": ">10",
  },
  macos: {
    safari: ">10.1"
  },
 
  // per platform (mobile, desktop or tablet)
  mobile: {
    safari: '>=9',
    'android browser': '>3.10'
  },
 
  // or in general
  chrome: "~20.1.1432",
  firefox: ">31",
  opera: ">=22",
 
  // also supports equality operator
  chrome: "=20.1.1432", // will match particular build only
 
  // and loose-equality operator
  chrome: "~20",        // will match any 20.* sub-version
  chrome: "~20.1"       // will match any 20.1.* sub-version (20.1.19 as well as 20.1.12.42-alpha.1)
});
```

