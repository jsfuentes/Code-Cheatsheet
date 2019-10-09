# Mongoose

## Usage

1. Connect mongoose as in setup
2. Create a model in ./models/somemodel.js
3. Import model in routes and use model fts


## Setup
```js
const mongoose = require('mongoose');

//Set up default mongoose connection
var mongoDB = 'mongodb://127.0.0.1/my_database';
mongoose.connect(mongoDB);
mongoose.Promise = global.Promise;

//Get the default connection
var db = mongoose.connection;
//Bind connection to error event (to get notification of connection errors)
db.on('error', console.error.bind(console, 'MongoDB connection error:'));
```

## Models

Models are defined using the Schema interface.

```js
const mongoose = require('mongoose');

const Schema = mongoose.Schema;
const SomeModelSchema = new Schema({
    a_string: String,
    a_date: Date
});

// Compile model from schema
const SomeModel = mongoose.model('SomeModel', SomeModelSchema );

module.exporst = SomeModel;
```

In mongoose.model, 'SomeModel' will be the collection created for the schema

### Schema [Types](http://mongoosejs.com/docs/schematypes.html)

```js
var schema = new Schema(
{
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
})
```

- ObjectId: reference to unique db instance. Use populate() method to get info
- Mixed: An arbitrary schema type.
- []: Can perform JavaScript array operations on these models
- Can also have isntance methods, static methods, and speciality queries
#### Virtual
```js
AuthorSchema
.virtual('url')
.get(function () {
  return '/catalog/author/' + this._id;
});
```
Can now do Author.name

## Model Functions

#### Creating

```js
// Create an instance of model SomeModel
var awesome_instance = new SomeModel({ name: 'awesome' });

// Save the new model instance, passing a callback
awesome_instance.save(function (err) {
  if (err) return handleError(err);
  // saved!
});
```

#### Updating

`save()` or `date()` to store modified values

#### Querying

```js
// find all athletes who play tennis, selecting the 'name' and 'age' fields
User.find({}, function(err, users) {});
Athlete.find({ 'sport': 'Tennis' }, 'name age', function (err, athletes) {
  if (err) return handleError(err);
  // 'athletes' contains the list of athletes that match the criteria.
})
```
- `.exec()` gives you a fully-fledged promise

```js
Athlete.
  find().
  where('sport').equals('Tennis').
  where('age').gt(17).lt(50).  //Additional where query
  limit(5).
  sort({ age: -1 }).
  select('name age').
  exec(callback);
```

- findById()
- findByIdAndRemove()
- findByIdAndUpdate()
- findOneAndRemove()
- findOneAndUpdate()

### References

```js
const mongoose = require('mongoose')
  , Schema = mongoose.Schema

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
