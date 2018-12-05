## Python3

Similar to python2 except you don't need an init.py

## Python2
#### Importing from Same Dir
Make an empty file called __init__.py in the same directory as the files. That will signify to Python that it's "ok to import from this directory". Then just:
```py
from user import User
from dir import Dir
```

#### Importing from Subdirectory

The same holds true if the files are in a subdirectory - put an __init__.py in the subdirectory as well.

```
bin/
    main.py
    classes/
        user.py
        dir.py
```


main.py

```python
from classes.user import User
from classes.dir import Dir
```

#### Importing from Sister Directory

```python
bin/
    mary/
        walk.py
	kate/
		run.py
```

Yea.., you need to add the root directory to `PYTHON_PATH` 

could also pip install -e 

## File IO In Imported Files

Are you trying to open a file in a package that you then import? Well that means you are getting an error because the path will be different if you run the script and import the script

```python
__location__ = os.path.realpath(
    os.path.join(os.getcwd(), os.path.dirname(__file__)))
```

- `join()` prepends current working directory, but the documentation says that if some path is absolute, all other paths left of it are dropped. Therefore, getcwd() is dropped when dirname(__file__) returns an absolute path. Also, the `realpath` call resolves symbolic links if any are found

Then 

```python
f = open(os.path.join(__location__, 'bundled-resource.jpg'))

```

