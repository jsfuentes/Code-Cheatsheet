# Os

```python
import os

os.chdir(path) #cd
cwd = os.getcwd() #pwd
```

## Get all files in subdirs
```python
for root, dirs, files in os.walk(PATH_TO_NOTES):
  for file in files:
    curFile = os.path.join(root, file)
```
### Get Environment

```python
os.environ.get('SECRET_KEY')
```

## Files

Underlying open is from `io` library

```python
#f is file object
f = open('workfile', 'w')
f.write("Now the file has one more line!")
f.close()
  
#To write bytes
with open(filename, 'wb') as f: 
  f.write(filebytes)
```

Modes
- `'r'` read; DEFAULT
- `'w'` writing(erase existing file)
- `'w+'` writing(create new file if it doesn't exist)
- `'a'` appending to the end
- `'a+'` appending to the end(create new file if needed)
- `'r+'` both reading and writing

## Reading Data

```python
for line in f:
    print(line)
    
f.readline()#leaves \n and '' when done
```

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

#### Advanced OS*

- could bypass system caches, more metadata/permissions access

```python
import os, fcntl


fd = os.open("file.txt", os.O_WRONLY | os.O_CREAT | os.O_EXCL, 0o644) #This creates a new file with specific permissions, failing if the file already exists

#Lock file
fd = os.open("file.txt", os.O_RDWR)
fcntl.flock(fd, fcntl.LOCK_EX)
# Perform operations...
fcntl.flock(fd, fcntl.LOCK_UN)
os.close(fd)
```

## Play Audio Files

```python
os.system("afplay Endgame.mp3")
```

