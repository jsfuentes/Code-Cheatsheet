# Dictionaries

```python
d= {}
d[k] = v
del d[k]
# Will error if doesn't exist
d["key"]
d.get('key', 'defaultValue')
d.pop(k, None) #get and pop, allows you to remove without checking for existence
```

### Iteration

```python
#For Python 2.x
for key, value in d.iteritems():

#For Python 3.x:
for k, v in d.items():
for v in d.values():
for k in d.keys():
 
lambda x: x.values()[0]
```



