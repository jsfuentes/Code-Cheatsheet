# MongoDB

Use mongoose if you want ORM 

```js
const MongoClient = require('mongodb').MongoClient,
```

### Basic

```js
async function connectToCollection(db_uri) {
  console.log(db_uri);
  const db = await MongoClient.connect(db_uri);

  const dbo = db.db("companies");
  return dbo.collection("data");
}

const dbData = await connectToCollection(secrets['db_uri']);
dbData.insertOne({"TEST": 3});
```

## Query

find returns a cursor, if you want to load data can do toArray()

```js
await dbData.find({"company": company}).toArray();
```

## Iterate over Collection

```js
let companyDoc = await dbData.find().toArray();
companyDoc.forEach((d) => {
    console.log(d['company']);
    dbSanitizedData.
});
```

