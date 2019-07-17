# Packages

npm packages particuarly for the server

## Some packages

- cheerio - Fast, flexible & lean implementation of core jQuery designed specifically for the server.

  ```js
  const cheerio = require('cheerio')
  const $ = cheerio.load('<h2 class="title">Hello world</h2>')
   
  $('h2.title').text('Hello there!')
  $('h2').addClass('welcome')
   
  $.html()
  ```

  

- 