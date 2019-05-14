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

```json
{
  "name": "Ecstatic",
  "version": "0.1.0",
  "description": "Ask students one question every day effortlessly, gain insights and make better data-driven decisions to increase attendance, performance & social-emotional wellbeing.",
  "main": "src/js/main.js",
  "scripts": {
    "build:content": "parcel build src/content_script/content.js -d src/build/ -o content.js",
    "watch:content": "parcel watch src/content_script/content.js -d src/build/ -o content.js",
    "build:background": "parcel build src/background_page/background.js -d src/build/ -o background.js",
    "watch:background": "parcel watch src/background_page/background.js -d src/build/ -o background.js",
    "build": "npm run build:background && npm run build:content",
    "watch": "concurrently \"npm run watch:content\" \"npm run watch:background\"",
    "package": "npm install && npm run build && npm run delete && npm run copy",
    "delete": "rm -rf node_modules && rm package-lock.json",
    "copy": "cd .. && mkdir -p extension-builds/build && cp -a chrome-ext extension-builds/build"
  },
  "author": "Atakan Goktepe",
  "dependencies": {
    "babel-preset-env": "^1.7.0",
    "babel-preset-react": "^6.24.1",
    "crypto-js": "^3.1.9-1",
    "moment": "^2.24.0",
    "parcel-bundler": "^1.12.3",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-load-script": "0.0.6"
  },
  "devDependencies": {
    "babel-core": "^6.26.3",
    "concurrently": "^4.1.0"
  }
}

```

Then change manifest.json to have the build scripts

Make sure all the files you want are imported in the one file you build