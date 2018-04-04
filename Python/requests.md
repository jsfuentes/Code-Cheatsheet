# Python Requests
```python
import requests
```

### Types of requests
```python
r = requests.post(
r = requests.put(
r = requests.delete(
r = requests.head(
r = requests.options(
```

```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('http://httpbin.org/get', params=payload)
#You can see that the URL has been correctly encoded by printing the URL:
print(r.url)
http://httpbin.org/get?key2=value2&key1=value1
```

### Responses
Builtin json decoder `r.json()`
To get bit representation(turn into Image) `i = Image.open(BytesIO(r.content))`

Checking response r.headers
