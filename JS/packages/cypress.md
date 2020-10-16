# Cypress

```bash
yarn add -D cypress
```

## Usage

Based off [jQuery](https://docs.cypress.io/guides/references/bundled-tools.html#Other-Library-Utilities),  [Mocha](https://docs.cypress.io/guides/references/bundled-tools.html#Mocha) and [Chai](https://docs.cypress.io/guides/references/bundled-tools.html#Chai) with many of the same selector and test interfaces

Queues all the commands async so use .then() and such to handle conditionals

Supports ES6 and importing packages out of the box

```js
// Each method is equivalent to its jQuery counterpart. Use what you know!
cy.get('#main-content')
  .find('.article')
  .children('img[src^="/static"]')
  .first()
```

```bash
./node_modules/.bin/cypress open
```

Yup no imports or anything needed

```javascript
/* global describe it cy */
describe('My First Test', () => {
  it('finds the content "type"', () => {
    cy.visit('https://example.cypress.io')
    
		cy.get('.main').contains('New Post')
    cy.contains('Like article')

    cy.url().should('include', '/commands/actions')
    
    cy.get('.action-email')
      .type('fake@email.com')
      .should('have.value', 'fake@email.com')
  })
})
```

### Commands

```javascript
cy.get('.my-slow-selector', { timeout: 10000 }).type("HI")
```

Cy will retry most commands until it finds the element or timeouts(default 4 secs) 

- [`.blur()`](https://docs.cypress.io/api/commands/blur.html) - Make a focused DOM element blur.
- [`.focus()`](https://docs.cypress.io/api/commands/focus.html) - Focus on a DOM element.
- [`.clear()`](https://docs.cypress.io/api/commands/clear.html) - Clear the value of an input or textarea.
- [`.check()`](https://docs.cypress.io/api/commands/check.html) - Check checkbox(es) or radio(s).
- [`.uncheck()`](https://docs.cypress.io/api/commands/uncheck.html) - Uncheck checkbox(es).
- [`.select()`](https://docs.cypress.io/api/commands/select.html) - Select an `<option>` within a `<select>`.
- [`.dblclick()`](https://docs.cypress.io/api/commands/dblclick.html) - Double-click a DOM element.
- [`.rightclick()`](https://docs.cypress.io/api/commands/rightclick.html) - Right-click a DOM element.

### Should

```javascript
cy.get(':checkbox').should('be.disabled')

cy.get('form').should('have.class', 'form-horizontal')

cy.get('input').should('not.have.value', 'US')

cy
  // Find the el with id 'some-link'
  .get('#some-link')
  .then(($myElement) => {
    // ...massage the subject with some arbitrary code, grab its href property
    const href = $myElement.prop('href')
    // strip out the 'hash' character and everything after it
    return href.replace(/(#.*)/, '')
  })
  .then((href) => {
    // href is now the new subject which we can work with now
  })
```

## Advanced

- [`cy.exec()`](https://docs.cypress.io/api/commands/exec.html) - to run system commands
- [`cy.task()`](https://docs.cypress.io/api/commands/task.html) - to run code in Node via the [`pluginsFile`](https://docs.cypress.io/guides/references/configuration.html#Folders-Files)
- [`cy.request()`](https://docs.cypress.io/api/commands/request.html) - to make HTTP requests

#### Hooks(Lifecycle?)

```js
describe('Hooks', () => {
  before(() => {
    // runs once before all tests in the block
  })

  beforeEach(() => {
    // runs before each test in the block
  })

  afterEach(() => {
    // runs after each test in the block
  })

  after(() => {
    // runs once after all tests in the block
  })
})
```

#### Act on A Subject Sync with .then()

```js
cy
  // Find the el with id 'some-link'
  .get('#some-link')

  .then(($myElement) => {
    // ...massage the subject with some arbitrary code

    // grab its href property
    const href = $myElement.prop('href')

    // strip out the 'hash' character and everything after it
    return href.replace(/(#.*)/, '')
  })
  .then((href) => {
    // href is now the new subject
    // which we can work with now
  })
```

#### Assertions

1. **Implicit Subjects:** Using [`.should()`](https://docs.cypress.io/api/commands/should.html) or [`.and()`](https://docs.cypress.io/api/commands/and.html).

```js
cy.get('#header a')
  .should('have.class', 'active')
  .and('have.attr', 'href', '/users')
```

2. **Explicit Subjects:** Using `expect`, harder not recommended

#### Other 

```js
cy.setCookie("_react_phoenix_key", "SFMyNTS....");
```