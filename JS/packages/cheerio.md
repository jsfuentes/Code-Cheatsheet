# [Cheerio](https://cheerio.js.org/)

Parsing and manipulating HTML and XML.

```bash
npm install cheerio
```

## Usage

```ts
const $ = cheerio.load(reviewHtml)
const hiddenText = $('span[style="display:none"]')
    .html()
    .replace(/<br\s*\/?>/g, '\n')
    .replace(/<[^>]*>/g, '')

return hiddenText
```

