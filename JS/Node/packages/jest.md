# Jest

Delightful javascript testing

```bash
npm install --save-dev jest #must then run in package.json scripts
npm install jest --global
```

## Most Basic

 sum.js

```javascript
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

sum.test.js

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
})
```

package.json

```json
"scripts": {
	"test": "jest"
}
```

`npm run test`

### Matchers

`expect(2 + 2)` - produces expectation object you call matchers on

- `.toBe(4)` => Object.is
- `.toEqual(4)` => recursively checks fields of object or array, `toBe` for numbers
- `.not.toBe(0)` => negate matcher
- `.toBeNull` => null
- `.toBeUndefined` => undefined
- `.toBeDefined` => opp of `toBeUndefined`
- `.toBeTruthy` =>`if` statement treats as true
- `.toBeFalsy` => `if` statement treats as false
- `.toBeGreaterThan(3)`
- `.toBeGreaterThanOrEqual(3.5)`
- `.toBeLessThan(5)`
- `.toBeLessThanOrEqual(4.5)`
- `.toBeCloseTo`  => use instead of equals for jank floating pt
- `.toMatch(/I/)` => String regular expressions
- `.toContain('beer')` => check array for in 
- `.toThrow()` => throws errors

### Async

Can't just expect in callback because test will finish, instead add done argument and test will wait until called or timeout and fail

##### Callback

```js
test('the data is peanut butter', done => {
  function callback(data) {
    expect(data).toBe('peanut butter');
    done();
  }

  fetchData(callback);
});
```

##### Promises

Just return a promise

```js
test('the data is peanut butter', () => {
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});
```

## CLI Options

```bash
jest my-test --notify --config=config.json
```

files matching `my-test`, native OS notification on completion, and config.json as config