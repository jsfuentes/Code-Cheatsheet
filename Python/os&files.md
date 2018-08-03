# Os

```python
import os

os.chdir(path) #cd
```

## Get all files in subdirs
```python
for root, dirs, files in os.walk(PATH_TO_NOTES):
  for file in files:
    curFile = os.path.join(root, file)
```
# Files
```python
#f is file object
 f = open('workfile', 'w')
 f.close()
```

Modes
- `'r'` read; DEFAULT
- `'w'` writing(erase existing file)
- `'a'` appending to the end
- `'r+'` both reading and writing

## With
Automatically close for ya
```python
with open('workfile', 'r') as f:
  read_data = f.read() #all datadddddd
```

## Pickle
```python
with open(r"categorizationModel.pickle", "wb") as output_file:
    cPickle.dump(rf, output_file)

with open(r"categorizationModel.pickle", "r") as model:
    rfLoaded = cPickle.load(model)
```

#### CPickle
- optimized cousin cPickle written in C, 1000x faster
- just doesn't support subclassing of the Pickler() and Unpickler() classes
- usually better
- same interface
