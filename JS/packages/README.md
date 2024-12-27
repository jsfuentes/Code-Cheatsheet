# Packages

This is the general npm package list for JS, the individual folders have more specific packages for them, but this is the general ones that can be used anywhere.

To use core nodeJS modules you need some extra bundler configuration

Compare package trends with [npmtrends](https://npmtrends.com/react-redux-vs-zustand)

## Package Managers

**2024 Rec: pnpm for small projects, npm for large projects**

**2022 Rec**: npm, as it adopted many of yarn's features and has more commands like --force or --legacy-deps

### Choosing a Manager

npm vs pnpm vs yarn

- All use a package.json, run scripts
- Main diff is lockfiles: pnpm-lock.yaml, yarn.lock, package-lock.json
- [Trends](https://npmtrends.com/npm-vs-pnpm-vs-yarn) show npm 4000x installs of pnpm, and 2024 pnpm gaining relative market share 5x in last 2 years vs 2x of others
- Choose yarn for emojis! 
  - confusing future versions

- Pnpm
  - pnpm lock files use yaml are easier to diff/merge conflicts :)
  - very space efficient: pnpm use global node modules instead of installing per project, and only stores files that changed
  - faster install than rpm


### [Corepak](https://nodejs.org/api/corepack.html) manages package managers (Experimental)

- uses  new field in package.json "packageManager": "pnpm@8.15.8", avoids package manager problems by downloading and using specific version
- Seems too weird, try using asdf instead 

```bash
corepack enable pnpm #didnt work had to brew install pnpm
corepack enable yarn

corepack use yarn@* #sets packageManager value to latest
```

## Pnpm

| npm command     | pnpm equivalent                               |
| --------------- | --------------------------------------------- |
| `npm install`   | [`pnpm install`](https://pnpm.io/cli/install) |
| `npm i <pkg>`   | [`pnpm add `](https://pnpm.io/cli/add)        |
| `npm run <cmd>` | [`pnpm `](https://pnpm.io/cli/run)            |

```bash
pnpm outdated
```



## Npm

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

## Yarn

```bash
yarn #install dependencies
yarn add
yarn add -D #add as dev dependecies
yarn [script]
yarn upgrade #upgrade all packages to latest version of specified range
yarn upgrade --latest #upgrade across major versions too, potentially changing package.json
```

#### Upgrading packages

```bash
yarn upgrade #upgrade all minor version
yarn outdated #to see all major version outdates
# For each major version update, check the update to see what the breaking changes are and make sure you fix any issues
yarn add * * #to upgrade in package.json
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

### Fields

Just use the special pre and post prefix to run things before and after command

```json
    "postinstall": "prisma generate && husky install",
```

