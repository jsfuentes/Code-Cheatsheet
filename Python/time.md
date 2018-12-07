# Datetime

Higher precision then time maybe

## GETTING NOW
```python
import datetime
now = datetime.datetime.now()
today = now.date()
moment = now.time()
```
## ADDING TIME
```python
a = datetime.datetime(100,1,1,11,34,59)
b = a + datetime.timedelta(0,3) # days, seconds, then other fields.
## of just replace what you want 
time.replace(hour, minute, second, microsecond, tzinfo, fold)
```

# Time

#### Sleep

```python
import time
time.sleep(5)  	# 5 seconds
```

#### Time Elapsed

```python
import time

start = time.time()
print("hello")
end = time.time()
print(end - start)
```