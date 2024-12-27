# MongoDB

Use mongoose if you want ORM 

```js
const MongoClient = require('mongodb').MongoClient,
const ObjectID = require('mongodb').ObjectID,
```

### Basic

```js
async function connectToCollection(db_uri) {
  const db = await MongoClient.connect(db_uri);
  const dbo = db.db("companies"); //database
  return dbo.collection("data"); //collection
}

const dbData = await connectToCollection(secrets['db_uri']);
await dbData.insertOne({"TEST": 3});
```

## Query

find returns a cursor, if you want to load data can do toArray()

```js
await dbData.find({"company": company}).toArray();
companyDoc.forEach((d) => {
    console.log(d['company']);
});
await dbData.findOne({_id: cls.id});
```

#### Cursor

##### Count

```js
collection.find().count(function(err, count) {
    //........
});
```

##### Iterate

```js
cursor.each(function(err, item) {
    // If the item is null then the cursor is exhausted/empty and closed
    if(item == null) {
```

## One to One

Just combine them 

## Many to One

Could just embed the many into the one array

OR

Store reference

```json
//PUBLISHER:
{
   _id: "oreilly",
   name: "O'Reilly Media",
   founded: 1980,
   location: "CA"
}

//BOOK:
{
   _id: 123456789,
   title: "MongoDB: The Definitive Guide",
   author: [ "Kristina Chodorow", "Mike Dirolf" ],
   published_date: ISODate("2010-09-24"),
   pages: 216,
   language: "English",
   publisher_id: "oreilly"
}
```

