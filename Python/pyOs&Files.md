# Os

```py
import os

os.chdir(path) #cd
```

## Get all files in subdirs
```py
for root, dirs, files in os.walk(PATH_TO_NOTES):
  for file in files:
    curFile = os.path.join(root, file)
```
dd 
# Files
```py
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
```py
with open('workfile', 'r') as f:
  read_data = f.read() #all datadddddd
```
