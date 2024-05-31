# Pyppetter

Python implementation of puppeteer

Async innately so can have multiple browsers running!

## Basic

```python
import asyncio
from pyppeteer import launch

async def main():
    browser = await launch(headless=False)
    page = await browser.newPage()
    await page.goto('http://example.com')
    await page.screenshot({'path': 'example.png'})
    await browser.close()

asyncio.ensure_future(main())
```

## Page Functions To Know

- .goto('example.com')

- .screenshot({path: 'filename.png'})
- .type('#searchbox input', 'Headless Chrome', {delay: 100});
- .waitForSelector(*[someSelector]*)
- .click(*[someSelector]*)

## Use DOM Manipulation

```python
textContent = await page.evaluate('''() => document.querySelector('p').textContent''');
```

```python
element = await page.querySelector('h1')
title = await page.evaluate('(element) => element.textContent', element)
```

## Differences From Puppeteer

`Page.querySelector()`/`Page.querySelectorAll()`/`Page.xpath()` instead of`Page.$()`/`Page.$$()`/`Page.$x()`. Pyppeteer also has shorthands for these methods, `Page.J()`, `Page.JJ()`, and `Page.Jx()`.

## Other Example

```python
import asyncio
from pyppeteer import launch

async def main():
    browser = await launch()
    page = await browser.newPage()
    await page.goto('http://example.com')
    await page.screenshot({'path': 'example.png'})

    dimensions = await page.evaluate('''() => {
        return {
            width: document.documentElement.clientWidth,
            height: document.documentElement.clientHeight,
            deviceScaleFactor: window.devicePixelRatio,
        }
    }''')

    print(dimensions)
    # >>> {'width': 800, 'height': 600, 'deviceScaleFactor': 1}
    await browser.close()

asyncio.get_event_loop().run_until_complete(main())
```

