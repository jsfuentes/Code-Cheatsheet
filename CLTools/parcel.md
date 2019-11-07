# Parcel

Simple building

```json
  "scripts": {
    "build": "parcel build src/js/main.js -d src/build/ -o main.js",
    "watch": "parcel watch src/js/main.js -d src/build/ -o main.js",
```

If using inside a chrome plugin, use` --no-hmr` flag to not do hot module replacement b/c you cant so will have error

