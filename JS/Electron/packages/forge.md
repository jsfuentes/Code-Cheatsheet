# [Electron-Forge](https://www.electronforge.io/)

Add webpack to get hotreloading

There is a [react template](https://github.com/electron-userland/electron-forge-templates), but for some reason it is deprecated or something..

```bash
npx create-electron-app electron --template=webpack
cd electron #preinstalled to yarn.lock
rm -rf yarn.lock node_modules
npm install
npm start
```

#### Building

```bash
npm run make #=> electron-forge make
```

### Config

example.forge.config.js

```js
{
  packagerConfig: { ... },
  electronRebuildConfig: { ... },
  makers: [ ... ],
  publishers: [ ... ],
  plugins: [ ... ],
  hooks: { ... },
  buildIdentifier: 'my-build'
}
```

