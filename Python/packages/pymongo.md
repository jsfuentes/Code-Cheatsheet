# Pymongo

`pip install pymongo`

Python package to manage interaction with mongoldb

Three levels: client, db, and collection

```python
from pymongo import MongoClient
client = MongoClient('mongodb://localhost:27017/')
db = client.test_database
posts = db.test_collection
post_id = posts.insert_one(post).inserted_id
```

#### Connecting to Mongo Atlas

To make up for their shitty documentation, their stupid `mongodb+srv://`... requires pymongo 3.5+ and `openssl version` must return 1.1 or more. And you must use the following extra code

```python
import ssl
client = pymongo.MongoClient('[atlas...uri]', ssl=True, ssl_cert_reqs=ssl.CERT_NONE)
```

## QUERYING

Returns a cursor which is iterable, use .count to get the number in the cursor for empty checking

```python
db.student.find({}, {roll:1, _id:0}) #Projection: find all students and return their roll and not their id(id returned by default
dbClasses.find({"location": { '$regex': '.*' + building + '.*'}, "day": WEEKDAYS[weekday]})
```

## Inserting
```py
post_id = posts.insert_one(post).inserted_id
```
- post is a dict
- "_id", is automatically added if the document doesn’t already contain an "_id" key
- use insert_many to insert list of dicts
-
## DELETING
```python
dbClasses.remove({"time": "scheduled"})
```
