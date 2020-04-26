# Prettier

An opinionated code formatter to enforce consistent style on save

Needs to be configured to work with eslint to get correct code, see eslint for info

## Other

Can set `prettier.require` in settings to only run in Vscode on save

## Config

Use `.prettierrc.yaml`

```yaml
trailingComma: "es5" #Trailing commas where valid in ES5 (objects, arrays, etc.)
tabWidth: 2
```

### Cli

Use yarn first in your project with prettier installed so you don't have to install globally

```bash
yarn prettier write .
```



