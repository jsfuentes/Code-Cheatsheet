# Puppeteer

Check out crossplatform [playwright](https://github.com/microsoft/playwright) (2020 Microsoft)

```bash
yarn add puppeteer
```

https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md

## Usage

```js
async function f() {
  const browser = await puppeteer.launch({
    headless: false,
    defaultViewport: { width: 1430, height: 670 },
    args: ["--use-fake-ui-for-media-stream"],
  });
  const page = await browser.newPage();
  //not sure if below works actually...
  await page.on("console", (msg) => {
    for (let i = 0; i < msg.args.length; ++i)
      console.log(`${i}: ${msg.args[i]}`);
  });
  page.setDefaultNavigationTimeout(60000); 
  
  await page.goto("http://localhost:4000");

  const ContinueToEventS = "body > div:nth-child(11) > div";
  await page.waitForSelector(ContinueToEventS);
  await page.click(ContinueToEventS);

  await browser.close();
}
```

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