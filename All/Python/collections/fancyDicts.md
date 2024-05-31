## OrderedDict

keeps order of insertion

```python
from collections import OrderedDict
```

## DefaultDict

Creates default, nonnull value for keys

```python
from collections import defaultdict
d = defaultdict(list)
for k, v in somePairs:
    d[k].append(v)
```

## Counter

Counts elements

```python
from collections import Counter
c = Counter("hell") #Counter({'l': 2, 'h': 1, 'e': 1})

#Add iterables of values
c.update([1, 3, 4])
c.most_common(10) # 10 most common
```

