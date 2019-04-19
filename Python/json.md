# JSON

```python
import json
```

## Dump vs Dumps

`dumps`: returns a string

`dump`: for printing out to file

```python
someJson = {'x': 1, 'y': 57}
print(json.dumps(someJson))

f1=open("test.txt", 'w')
json.dump(someJson, f1)
```

## Loads

json.loads(str)

json.load(file)

## Object ID

```python
import json
from bson import ObjectId

class JSONEncoder(json.JSONEncoder):
    def default(self, o):
        if isinstance(o, ObjectId):
            return str(o)
        return json.JSONEncoder.default(self, o)

JSONEncoder().encode(analytics)
```