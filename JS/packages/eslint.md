# Eslint

`npm install -g eslint`

Without running code, find errors and potential errors

Vscode has an eslint plugin that allows you see potential errors

## Setup In Project

```bash
yarn add -D eslint
./node_modules/.bin/eslint --init
```

## Setup In Project With Prettier

In root of project:

```bash
yarn add -D eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks prettier
```

.eslintrc

```json
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "node": true
  },
  "plugins": ["react", "react-hooks"],
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "sourceType": "module",
    "ecmaVersion": 2018
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "rules": {
    "linebreak-style": ["error", "unix"],
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn"
  }
}
```

Can add additional config in prettier

## Rules

[No-unescaped-entities](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-unescaped-entities.md)

- The preferred way to include one of these characters is to use the HTML escape code.
  - `>` can be replaced with `>`
  - `"` can be replaced with &ldquo;, &quot;
  - `'` can be replaced with &lsquo;, &apos;
  - `}` can be replaced with &#125;