# Datetime

Higher precision then time maybe

## GETTING NOW
```python
from datetime import datetime

#Create datetime objects
now = datetime.now()
today = now.date()
moment = now.time() 
```
## Printing

```python
#Print them
now.isoformat() #'2023-03-30T23:36:52.926931'
now.strftime('We are the %d, %b %Y')
```

## Parsing

POSIX/UTC using a local time zone

```python
from datetime import datetime

datetime.fromisoformat("2011-11-04T00:05:23Z")
datetime.fromtimestamp(1553236529) #POSIX/UTC local
datetime.utcfromtimestamp(1553236529) #UTC local
```

Strptime lets you parse arbitrary formats: see [here](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior) for all the meanings

```python
date_time_str = "2021-12-24 05:12:34.am"
datetime.datetime.strptime(date_time_str, '%Y-%m-%d %H:%M:%S.%f')
```

## Delta

```python
a = datetime.datetime(100,1,1,11,34,59)
b = a + datetime.timedelta(0,3) # days, seconds, then other fields.

## or just replace what you want 
now = now.replace(hour=5, minute=0, second=0, microsecond=0)
```

## Date

```python
datetime.date(2007, 12, 25)
```

## Timer

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