# Setup for Nodejs/Express

`node` will work if you have node

## Using Generator
```bash
npm install express-generator -g
express [project name] --view=ejs
```
- `--view=ejs` adds ejs engine support
- `--no-view`
- `--git` adds a gitignore

## Running

Add the following to package.json

```json
  "scripts": {
    "start": "export NODE_ENV=production && node ./bin/www",
    "dev": "export NODE_ENV=development && export DEBUG=app* && nodemon ./bin/www"
  }
```

Debug is for debug library

Export works for config library