# Iterables

## Lists
- Everything is a ptr, to make copy `copy = original[:]`
- sum([1,2,0]) => 2, great for checking for a property i.e [1 for c in t if ...]

## Iterables
`len(iterable)`

## Dictionaries
d.get('key', 'defaultValue')
d.pop(k, None) #get and pop, allows you to remove without checking for existence

## Sorting
sorted()
list.sort(key={function to call}, reverse=False) #ascending is default
.sort(key=lambda x: x[1], reverse=True)

## Get i/index
for counter, value in **enumerate**(some_list):
    print(counter, value)
