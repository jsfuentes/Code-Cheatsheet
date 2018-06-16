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

## Lambdas
lambda x, y: x[1] + y
