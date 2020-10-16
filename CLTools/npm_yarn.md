# Overview

Both use a package.json to record packages 

You can add scripts to your package.json and run them with both

# Yarn

```bash
yarn #install dependencies
yarn add
yarn add -D #add as dev dependecies
yarn [script]
yarn upgrade #upgrade all packages to latest version of specified range
yarn upgrade --latest #upgrade across major versions too, potentially changing package.json
```

# Npm

```bash
npm i #Install all dependencies
npm i [package name]
npm i node-sass --save-dev #install as dev-dependencies
npm i lodash@4.17.4 #specify version
npm i lodash@^4.0.0 #specify version with syntax
npm run [script]
```

#### Npx

npx makes it easy to use CLI tools and other executables hosted on the registry

Easy way to keep it updated

```
npx create-react-app my-app
npx cmatrix
```

## Package.json Syntax

or example, to specify acceptable version ranges up to 1.0.4, use the following syntax:

- Patch releases: `1.0` or `1.0.x` or `~1.0.4`
- Minor releases: `1` or `1.x` or `^1.0.4`
- Major releases: `*` or `x`

`~1.0.2` = latest patch version like `1.0.4`

 `^1.0.2` = latest minor/patch version like `1.1.0`.

#### Dev Dependencies

Things only used in dev like testing frameworks, bundling, or checking code style

 if `NODE_ENV` is set to `production` npm will skip `devDependencies`