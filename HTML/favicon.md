# Favicon

## Finding a urls favicon

Simplest, google internal service

https://www.google.com/s2/favicons?domain=www.stackoverflow.com

[Manual solution](https://stackoverflow.com/questions/5119041/how-can-i-get-a-web-sites-favicon)

1. Look for the `favicon.ico` at the root of the domain

   `www.domain.com/favicon.ico`

2. Look for a `<link>` tag with the `rel="shortcut icon"` attribute

   `<link rel="shortcut icon" href="/favicon.ico" />`

3. Look for a `<link>` tag with the `rel="icon"` attribute

   `<link rel="icon" href="/favicon.png" />`

