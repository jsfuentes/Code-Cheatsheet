# electron-store [![Build Status](https://camo.githubusercontent.com/e7c2aa3be728b4e8bb11ed7a5b2052754486ff7b/68747470733a2f2f7472617669732d63692e6f72672f73696e647265736f726875732f656c656374726f6e2d73746f72652e7376673f6272616e63683d6d6173746572)](https://travis-ci.org/sindresorhus/electron-store)

> Simple data persistence for your [Electron](https://electronjs.org/) app or module - Save and load user preferences, app state, cache, etc

Electron doesn't have a built-in way to persist user preferences and other data. This module handles that for you, so you can focus on building your app. The data is saved in a JSON file in [`app.getPath('userData')`](https://electronjs.org/docs/api/app#appgetpathname).

You can use this module directly in both the main and renderer process.

## Install

```
npm install electron-store
```

*Requires Electron 5 or later.*

## Usage

```javascript
const Store = require('electron-store');

const store = new Store();

store.set('unicorn', '🦄');
console.log(store.get('unicorn'));
//=> '🦄'

// Use dot-notation to access nested properties
store.set('foo.bar', true);
console.log(store.get('foo'));
//=> {bar: true}

store.delete('unicorn');
console.log(store.get('unicorn'));
//=> undefined
```

