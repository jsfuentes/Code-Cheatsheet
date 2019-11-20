# Mongoose

```bash
npm install mongoose
```

1. Connect mongoose as in setup
2. Create a model in ./models/somemodel.js
3. Import model in routes and use model fts


## Setup
```js
const mongoose = require('mongoose');

const mongoDB = 'mongodb://127.0.0.1/my_database';
mongoose.connect(mongoDB);
//usually mongoose uses pseudo promises, this tells it to use real ones
mongoose.Promise = global.Promise;

//Get the default connection
const db = mongoose.connection;
//Bind connection to error event (to get notification of connection errors)
db.on('error', console.error.bind(console, 'MongoDB connection error:'));
```

## Defining Models

Models are defined using the Schema interface.

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//1. Define a schema
const TestSchema = new Schema({
  name: String,
  binary: Buffer,
  living: Boolean,
  updated: { type: Date, default: Date.now },
  age: { type: Number, min: 18, max: 65, required: true },
  mixed: Schema.Types.Mixed,
  _someId: Schema.Types.ObjectId,
  array: [],
  ofString: [String], // You can also have an array of each of the other types too.
  nested: { stuff: { type: String, lowercase: true, trim: true } }
});

//2. Compile model from schema
const Test = mongoose.model("Test", TestSchema);
//will use collection called Tests adding the s

module.exports = Test;
```

#### Schema [Types](http://mongoosejs.com/docs/schematypes.html)

- ObjectId: reference to unique db instance. Use `populate()` method to get info
- Mixed: An arbitrary schema type.
- []: Can perform JavaScript array operations on these models
- Can also have instance methods, static methods, and speciality queries
##### Virtual

Fields that dont exist in db

```js
AuthorSchema
.virtual('url')
.get(function () {
  return '/catalog/author/' + this._id;
});
```
Can now do Author.name

## Using Models

#### Creating

```js
const SomeModel = require("../models/SomeModel.js");

const awesome_instance = new SomeModel({ name: 'awesome' });
const newInstance = await awesome_instance.save();
```

#### Querying

Use `.exec()` to give you a promise, make sure to have set `mongoose.Promise` in setup

Returns `null` if not found

```js
const allTests = await Test.find().exec();
const users = await User.find({ 'sport': 'Tennis' }, 'name age').exec();
const athletes = await Athlete.
  find().
  where('sport').equals('Tennis').
  where('age').gt(17).lt(50).  //Additional where query
  limit(5).
  sort({ age: -1 }). //1 asc
  select('name age').
  exec();
```
- [`Model.deleteMany()`](https://mongoosejs.com/docs/api.html#model_Model.deleteMany)
- [`Model.deleteOne()`](https://mongoosejs.com/docs/api.html#model_Model.deleteOne)
- [`Model.find()`](https://mongoosejs.com/docs/api.html#model_Model.find)
- [`Model.findById()`](https://mongoosejs.com/docs/api.html#model_Model.findById)
- [`Model.findByIdAndDelete()`](https://mongoosejs.com/docs/api.html#model_Model.findByIdAndDelete)
- [`Model.findByIdAndRemove()`](https://mongoosejs.com/docs/api.html#model_Model.findByIdAndRemove)
- [`Model.findByIdAndUpdate()`](https://mongoosejs.com/docs/api.html#model_Model.findByIdAndUpdate)
- [`Model.findOne()`](https://mongoosejs.com/docs/api.html#model_Model.findOne)
- [`Model.findOneAndDelete()`](https://mongoosejs.com/docs/api.html#model_Model.findOneAndDelete)
- [`Model.findOneAndRemove()`](https://mongoosejs.com/docs/api.html#model_Model.findOneAndRemove)
- [`Model.findOneAndReplace()`](https://mongoosejs.com/docs/api.html#model_Model.findOneAndReplace)
- [`Model.findOneAndUpdate()`](https://mongoosejs.com/docs/api.html#model_Model.findOneAndUpdate)
- [`Model.replaceOne()`](https://mongoosejs.com/docs/api.html#model_Model.replaceOne)
- [`Model.updateMany()`](https://mongoosejs.com/docs/api.html#model_Model.updateMany)
- [`Model.updateOne()`](https://mongoosejs.com/docs/api.html#model_Model.updateOne)

#### Count

returns number >= 0

```js
const showCount = await Show.countDocuments({ _id: show_id });
const showExists = (await Show.countDocuments({ _id: show_id })) > 0;
```

#### Callback Style

Callback Style

```js
awesome_instance.save(function (err) {
  if (err) return handleError(err);
  // saved!
});

User.find({}, function(err, users) {});
// find all athletes who play tennis, selecting the 'name' and 'age' fields
Athlete.find({ 'sport': 'Tennis' }, 'name age', function (err, athletes) {
  if (err) return handleError(err);
  // 'athletes' contains the list of athletes that match the criteria.
})
```

### References

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const authorSchema = Schema({
  name    : String,
  stories : [{ type: Schema.Types.ObjectId, ref: 'Story' }] //model saved as
});
```
To get all stories authored, have to do a find of bob._id
```js
Story
.find({ author : bob._id })...
```

Can also fill in the field with the right model

```js
Story
.findOne({ title: 'Bob goes sledding' })
.populate('author');

story.author.name;
```
