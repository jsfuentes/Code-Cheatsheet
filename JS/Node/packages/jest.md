# Jest

Delightful javascript testing

```bash
npm install --save-dev jest #must then run in package.json scripts
npm install jest --global
```

## Most Basic

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

Will find any tests in subdirectories

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

#### Blocks

toplevel before each done first and after each done last compared to blocks

inside describes blocks run first, then tests

```js
describe('matching cities to foods', () => {
  // Applies only to tests in this describe block
  beforeEach(() => {
    return initializeFoodDatabase();
  });
  
  test(
  //...
```

### Async

Can't just expect in callback because test will finish, instead add done argument and test will wait until called or timeout and fail

The ways for using async also work for setup and teardown

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
//return fetchData().catch(e=>expect(e).toMatch('error'));
});
```

##### Async/Await

```js
test('the data is peanut butter', async () => {
  const data = await fetchData();
  expect(data).toBe('peanut butter');
});
```

### Setup

```js
beforeEach(() => {
  initializeCityDatabase();
});

afterEach(() => {
  clearCityDatabase();
});

beforeAll(() => {
  return initializeCityDatabase(); //return for promise
}); 

afterAll(() => {
  return clearCityDatabase();
});
```

## CLI Options

```bash
jest my-test --notify --config=config.json
```

files matching `my-test`, native OS notification on completion, and config.json as config

### Other

##### To only run one test

change `test(` to `test.only(`

```js
test.only('this will be the only test that runs', () => {
  expect(true).toBe(false);
});
```

#### Mock

Pretty cool, always you to specify different returns per time called, check arguments and call count

##### More Plugins

#### API Routes

```js
const request = require('supertest');
const server = require('../app.js');

describe('basic route tests', () => {
 test('get home route GET /', async () => {
 const response = await request(server).get('/');
 expect(response.status).toEqual(200);
 expect(response.text).toContain('Hello World!');
 });
});
```