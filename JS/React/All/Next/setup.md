# Setup

```bash
npx create-next-app

npm init next-app nextjs-blog --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"
```

## Usage

```bash
yarn dev
```

## Absolute Path Imports

### TS

```json
"compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "conf": ["conf/*"],
      "src": ["src/*"],
      "styles": ["styles/*"]
    },
    ...
```

### JS

Jsconfig.json

```js
{
  "compilerOptions": {
    "paths": {
      "src": ["src"]
    }
  }
}
```



