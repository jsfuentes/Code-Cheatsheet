# Setup

```bash
npx create-next-app@latest
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



