# Forms

## Access data
- `req.body` is JSON of data
- `req.body.name`

## Images
```HTML
<input type="file"> </input>
```

## Multer
Adds support for `enctype="multipart/form-data"`
```js
var multer = require('multer');

router.post('/create', upload.any(), eventsController.event_create);

//in event_create
var fileInfo = req.files;
```

## Mongoose Object
var Item = new ItemSchema(
  { img:
      { data: Buffer, contentType: String }
  }
);

## Access Data
newItem.img.data = fs.readFileSync(req.files.userPhoto.path)
newItem.img.contentType = ‘image/png’;
