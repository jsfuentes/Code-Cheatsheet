# Puppeteer

https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md

## Usage

## Selector

```javascript
page.$$(selector); //querySelector
page.$(selector); //querySelectorAll
```



#### Type

```javascript
await page.type('#mytextarea', 'Hello'); // Types instantly
await page.type('#mytextarea', 'World', {delay: 100}); // Types slower, like a user
```

