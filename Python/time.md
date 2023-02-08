# Datetime

Higher precision then time maybe

## GETTING NOW
```python
import datetime
now = datetime.datetime.now()
today = now.date()
moment = now.time()
```
## Parsing

POSIX/UTC using a local time zone

```python
datetime.fromtimestamp(1553236529) #POSIX/UTC local
datetime.utcfromtimestamp(1553236529) #UTC local
```

Strptime lets you specify arbitrary formats: see [here](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior) for all the meanings

```python
datetime.datetime.strptime(date_time_str, '%Y-%m-%d %H:%M:%S.%f')
```

## Delta

```python
a = datetime.datetime(100,1,1,11,34,59)
b = a + datetime.timedelta(0,3) # days, seconds, then other fields.
## of just replace what you want 
time.replace(hour, minute, second, microsecond, tzinfo, fold)
```

## Date

```python
datetime.date(2007, 12, 25)
```

# Timer

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