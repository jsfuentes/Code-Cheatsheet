# Python
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

## Iterables
`len(iterable)`

## Dictionaries
d.get('key', 'defaultValue')
d.pop(k, None) #get and pop, allows you to remove without checking for existence

## Lists
- Everything is a ptr, to make copy `copy = original[:]`
- sum([1,2,0]) => 2, great for checking for a property i.e [1 for c in t if ...]

## Checking Packages
dir(nltk) - lists all functions in package

## Sorting
sorted()
list.sort(key={function to call})

## Lambdas

lambda x, y: x[1] + y
