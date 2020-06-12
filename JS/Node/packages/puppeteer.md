# Puppeteer

```bash
yarn add puppeteer
```

https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md

## Usage

## Selector

```javascript
page.$(selector); //querySelector
page.$$(selector); //querySelectorAll return array
```

#### Type

```javascript
await page.type('#mytextarea', 'World', {delay: 100}); // delay opt
```

#Element Handle

- .click() 
- .$$eval( () => )

```javascript
const html = await page.evaluate(body => body.innerHTML, bodyHandle);
```