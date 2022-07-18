# Storage Options

[Good Medium article](https://medium.com/cameron-nokes/how-to-store-user-data-in-electron-3ba6bf66bc1e)

- electron-store in packages/
- HTML5 Storage APIs
- Raw nodejs fs file system 

## Raw FS

Store

```js
const electron = require("electron");
const path = require("path");
const fs = require("fs");
const util = require("util");

import { store } from "./ext.js";

const userDataPath = (electron.app || electron.remote.app).getPath("userData");

//Media Storage writes everything to file with electron-store and fs except localChunks so its current state is the same across instances
class MediaStorage {
  constructor(filename) {
    this.filename = filename;
    this.path = path.join(userDataPath, filename);
    this.curFile = null;
    this.localChunks = [];
  }

  get curFile() {
    const v = store.get(this.filename);
    console.log("Got curFile", v);
    return v;
  }

  //file not considered readable until this filename is set
  set curFile(v) {
    console.log("Setting curFile to", v);
    store.set(this.filename, v);
  }

  async clear() {
    const unlink = util.promisify(fs.unlink);
    if (fs.existsSync(this.path)) {
      await unlink(this.path);
    }
    this.curFile = null; //TODO: check store reads this as null not 'null'
    this.localChunks = [];
    this.localChunksBytes = 0;
  }

  async append(blob) {
    this.localChunks.push(blob);
    const append = util.promisify(fs.appendFile);

    const data = await blob.arrayBuffer();
    const buf = Buffer.from(data);
    console.log(`Added: ${buf.length}`);
    await append(this.path, buf);
    fs.stat(this.path, (err, stats) => {
      console.log(`${this.filename} totals ${stats.size}`);
    });
  }
}

export const VideoStorage = new MediaStorage("curVideo.webm");
export const AudioStorage = new MediaStorage("curAudio.webm");
```



