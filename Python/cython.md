# Cython

A superset of python with c data types that compiles to c code

The c code it compiles to is long as fuck :(

## Basic Setup

1. Name python file to compile `.pyx`

2. In a `setup.py`, 

   ```python
   from distutils.core import setup
   from Cython.Build import cythonize
   
   setup(
       ext_modules = cythonize("<FILENAME>.pyx")
   )
   ```

3. Run this on the command line: `python setup.py build_ext --inplace`

   1. This creates a .so and .c file

4. To use this in python just `import test` 

## Variables

```python
cdef int n, i, len_p
```