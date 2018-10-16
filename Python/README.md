# Python

## Only function scoping
So

```py
if y > threshold:
  x = 1
print(x)
```

## run if not modules
`if __name__ == "__main__":`

## `and` and `or`
- 0, '', [], (), {}, and None are false

- Actually return one of the values being computed, so can do
- `'a' and 'b'` returns `'b'`
- '' and 'b' return ''
- So, 1 and a or b is basically the trinary operator(unless a is false)
- (1 and [a] or [b])[0] is the safe way

## Math
```py
round(5.0000, 3) #3 is number of decimal points
```

## '' vs ""
They are the same

## Checking Packages
dir(nltk) - lists all functions in package

## Functions

### KArgs & Args

he `*args` will give you all function parameters as a tuple

`**kwargs` will give you all **keyword arguments** as a dictionary expect acutal args

### Lambdas

`lambda x, y: x[1] + y`

## Input

- PYTHON 2: `input("Enter number")` interprets user input so if int, int will be returned
- `raw_input("Enter Your Name: ")` takes exactly what user typed 
- PYTHON 3: `input` is `raw_input`

## Exceptions

```python
try:
    x = int(input("Please enter a number: "))
    break
except ValueError:
    print("Oops!  That was no valid number.  Try again...")
```
