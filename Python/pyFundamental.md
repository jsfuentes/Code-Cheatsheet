# Python
## `and` and `or`
- 0, '', [], (), {}, and None are false

- Actually return one of the values being computed, so can do
- `'a' and 'b'` returns `'b'`
- '' and 'b' return ''
- So, 1 and a or b is basically the trinary operator(unless a is false)
- (1 and [a] or [b])[0] is the safe way

## '' vs ""
They are the same

## Iterables
`len(iterable)`

## Dictionaries
d.get('key', 'defaultValue')
d.pop(k, None) #get and pop, allows you to remove without checking for existence

## Strings
`chr(ord('a')+1)` to add one to 'a' and get 'b'
