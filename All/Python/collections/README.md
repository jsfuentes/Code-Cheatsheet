# General Iterables

`len(iterable)`

#### Loop Over Two Iteratables

```
for (f,b) in zip(foo, bar):
    print "f: ", f ,"; b: ", b
```

Stops at the shorter of the two and works for an arbitrary number of iterables

## Functional 

In python3, map makes an generator object. Wrap with list() to make a list again

Map

```python
outputs = map(function_to_apply, inputs)

list(outputs)
```

Filter

```python
number_list = range(-5, 5)
less_than_zero = list(filter(lambda x: x < 0, number_list))
```

Reduce

```python
from functools import reduce
product = reduce((lambda x, y: x * y), [1, 2, 3, 4])
```