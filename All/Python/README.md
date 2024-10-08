# Python

`python [filename]` `python3 [filename]`

[Standard Library](https://docs.python.org/3/library/)

## run if not modules

`if __name__ == "__main__":`

## Loops

```python
for idx, x in enumerate(xs):
    print(idx, x)
    
from tqdm import tqdm
for i in tqdm(range(10000)):
  ...
```

## Exceptions

- Error Types: `Exception` (most general?)| `RuntimeError`|`TypeError`|`OSError` etc

```python
 try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
    except (RuntimeError, TypeError, NameError):
    		pass
```

Capture exception info

```python
try:
    raise Exception('spam', 'eggs')
    break
except OSError as err:
    print("OS error: {0}".format(err))
except Exception as inst:
    print(type(inst))   
    print(inst.args)    
    print(inst)    #Uses __str__
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise #reraise error
```

## Access Args

```python
import sys
sys.argv #the list of command-line arguments with [0] being the file name
```

Can also use [argparse](https://docs.python.org/3/library/argparse.html)

## Only function scoping

```py
if y > threshold:
  x = 1
print(x)
```

## `and` and `or`
- 0, '', [], (), {}, and None are false
- Actually return one of the values being computed
  -  `'a' and 'b'` returns `'b'`
  - `'' and 'b'` return `''`
- So, `1 and a or b` is basically the trinary operator(unless a is false)
- (1 and [a] or [b])[0] is the safe way

## Math
```py
round(5.0000, 3) #3 is number of decimal points
```

## '' vs ""
They are the same

### == vs is

` is` checks they point to the same thing i.e [1,2,3] is not [1,2,3] but [1,2,3] == [1,2,3]

Use `is None` because a class could define == to be different and is is faster

## Checking Packages
`dir(nltk)` - lists all functions in package

## Functions

### KArgs & Args

`*args` will give you all function parameters as a tuple

`**kwargs` will give you all **keyword arguments** as a dictionary expect acutal args

Pass in dict like `f(**dict)` to act as **kwargs

### Lambdas

`lambda x, y: x[1] + y`

### Generators

```python
def simpleGeneratorFun(): 
    yield 1
    yield 2
    yield 3
  
for value in simpleGeneratorFun():  
    print(value)
```

## Input

- PYTHON 2: `input("Enter number")` interprets user input so if int, int will be returned(Security bug, runs arbitrary code use raw_input)
- `raw_input("Enter Your Name: ")` takes exactly what user typed 
- PYTHON 3: `input` is `raw_input`

## Exceptions

```python
try:
    x = int(input("Please enter a number: "))
    raise ValueError("Hello")
except ValueError:
    print("Oops!  That was no valid number.  Try again...")
```

### types

```python
str(1) #'1'
```

## Other

```python
value_when_true if condition else value_when_false
```

### Pip

```bash
#Install specific version
pip install pandas==1.3.4
```

