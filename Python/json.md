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

