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

*Unhashable so can't be keys/in set, but tuples can be...*

## Iterate

```python
for v in l:
for reverseV in reversed(l): #reversed returns iterator  
for i in range(len(l)):
for x in range(len(s) - 1, -1, -1): #reversed is more clear
for reverseI in reversed(range(len(l))): 
for i, v in enumerate(l):
```

## Helpers

```python
l.reverse()
reversed(l) #returns an iterator over 
copyOfL = l[:]
```

### Sorting

ascending is default

```python
sorted(l) # return new
sorted(l, reverse=True) # return new
l.sort(key=[ft to call], reverse=False)  #in place
l.sort(key=lambda x: x[1], reverse=True)
```

