# Chrome Plugins

Just need a folder with a manifest.json

```json
{
  "manifest_version": 2,
  "name": "Blocker",
  "description": "The most popular movies and TV shows in your default tab. Includes ratings, summaries and the ability to watch trailers.",
  "version": "0.0.1",
  "author": "Jorge Fuentes",
  "content_scripts": [
    {
      "js": ["content.js"],
      "matches": [
        "facebook.com",
        "http://www.linkedin.com"
      ]
    }
  ],
  "background": {
  "scripts": ["background.js"]
  }
}
```

Then go to `chrome://extensions` and click load unpacked extensions and click the folder of you code.

Boom, chrome extension. Click reload on changes.

### Use React/Import/ES6 in Plugins

Use a bundler like webpack or parcel and output a single js file that you include as the script in some build folder