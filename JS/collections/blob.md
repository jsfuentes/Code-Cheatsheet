# Blob (Binary Large Object)

a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)so its methods can be used for processing the data. Blobs can represent data that isn't necessarily in a JavaScript-native format. 

 [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File)interface is based on `Blob`

```jsx
const blob = new Blob(recordedChunks, { type: recordedChunks[0].type });
const blobURL = URL.createObjectURL(blob);

//....
	<video src={blobURL} />
```

## Transfering Into Node Buffer

```js
export async function storeVideo(blob, filepath) {
  const write = util.promisify(fs.writeFile);

  const data = await blob.arrayBuffer();
  const buf = Buffer.from(data);
  console.log("Storing", buf);
  await write(filePath, buf);
  console.log(`Blob stored at ${filePath}`);
}
```

