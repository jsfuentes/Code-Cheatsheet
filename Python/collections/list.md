# List

```python
l = []
l = [x for x in range(10) if x%2 == 0]
l.append(1)
l.extend([1,2,3])
l.remove(2)
del l[0]
l.pop() #remove and return
```

## Iterate

```python
for v in l:
for i in range(len(l)):
for reverseI in range(len(l)-1, -1, -1):
for i, v in enumerate(l):
```

## Helpers

```python
l.reverse()
copyOfL = l[:]
```

### Sorting

ascending is default

```python
sorted(l) # return new
l.sort(key=[ft to call], reverse=False)  #in place
l.sort(key=lambda x: x[1], reverse=True)
```

