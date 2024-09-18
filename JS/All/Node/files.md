# Files*

## Importing the fs module
```javascript
const fs = require('fs');
const fsPromises = require('fs').promises;  // For promise-based API
```

## Reading Files
```javascript
// Asynchronous
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Synchronous
const data = fs.readFileSync('file.txt', 'utf8');

// Promises
fsPromises.readFile('file.txt', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

## Writing Files
```javascript
// Asynchronous
fs.writeFile('file.txt', 'Hello, World!', (err) => {
  if (err) throw err;
  console.log('File written');
});

// Synchronous
fs.writeFileSync('file.txt', 'Hello, World!');

// Promises
fsPromises.writeFile('file.txt', 'Hello, World!')
  .then(() => console.log('File written'))
  .catch(err => console.error(err));
```

## Appending to Files
```javascript
// Asynchronous
fs.appendFile('file.txt', 'More content', (err) => {
  if (err) throw err;
  console.log('Content appended');
});

// Synchronous
fs.appendFileSync('file.txt', 'More content');

// Promises
fsPromises.appendFile('file.txt', 'More content')
  .then(() => console.log('Content appended'))
  .catch(err => console.error(err));
```

## Checking if File Exists
```javascript
// Asynchronous
fs.access('file.txt', fs.constants.F_OK, (err) => {
  console.log(`${err ? 'does not exist' : 'exists'}`);
});

// Synchronous
try {
  fs.accessSync('file.txt', fs.constants.F_OK);
  console.log('exists');
} catch (err) {
  console.log('does not exist');
}
```

## Deleting Files
```javascript
// Asynchronous
fs.unlink('file.txt', (err) => {
  if (err) throw err;
  console.log('File deleted');
});

// Synchronous
fs.unlinkSync('file.txt');

// Promises
fsPromises.unlink('file.txt')
  .then(() => console.log('File deleted'))
  .catch(err => console.error(err));
```

## Renaming Files
```javascript
// Asynchronous
fs.rename('oldFile.txt', 'newFile.txt', (err) => {
  if (err) throw err;
  console.log('File renamed');
});

// Synchronous
fs.renameSync('oldFile.txt', 'newFile.txt');

// Promises
fsPromises.rename('oldFile.txt', 'newFile.txt')
  .then(() => console.log('File renamed'))
  .catch(err => console.error(err));
```

## Getting File Information
```javascript
// Asynchronous
fs.stat('file.txt', (err, stats) => {
  if (err) throw err;
  console.log(stats);
});

// Synchronous
const stats = fs.statSync('file.txt');

// Promises
fsPromises.stat('file.txt')
  .then(stats => console.log(stats))
  .catch(err => console.error(err));
```

## Creating Directories
```javascript
// Asynchronous
fs.mkdir('newDir', { recursive: true }, (err) => {
  if (err) throw err;
  console.log('Directory created');
});

// Synchronous
fs.mkdirSync('newDir', { recursive: true });

// Promises
fsPromises.mkdir('newDir', { recursive: true })
  .then(() => console.log('Directory created'))
  .catch(err => console.error(err));
```

## Reading Directories
```javascript
// Asynchronous
fs.readdir('dir', (err, files) => {
  if (err) throw err;
  console.log(files);
});

// Synchronous
const files = fs.readdirSync('dir');

// Promises
fsPromises.readdir('dir')
  .then(files => console.log(files))
  .catch(err => console.error(err));
```

## Watching Files/Directories
```javascript
fs.watch('file.txt', (eventType, filename) => {
  console.log(`Event type is: ${eventType}`);
  if (filename) {
    console.log(`Filename provided: ${filename}`);
  }
});
```

## Streams
```javascript
// Read Stream
const readStream = fs.createReadStream('file.txt');
readStream.on('data', (chunk) => {
  console.log(chunk);
});

// Write Stream
const writeStream = fs.createWriteStream('file.txt');
writeStream.write('Hello, World!');
writeStream.end();
```

