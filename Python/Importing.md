## Python3
Must specify you want a relative path, cuz was confusing before
```py
from .user import User
from ..model import model
```

## Python2
#### Importing from Same Dir
Make an empty file called __init__.py in the same directory as the files. That will signify to Python that it's "ok to import from this directory". Then just:
```py
from user import User
from dir import Dir
```

The same holds true if the files are in a subdirectory - put an __init__.py in the subdirectory as well.

bin/
    main.py
    classes/
        user.py
        dir.py
So if the directory was named "classes", then you'd do this:
```py
from classes.user import User
from classes.dir import Dir
```
