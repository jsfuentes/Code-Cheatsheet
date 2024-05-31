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

#### Setting Headers

```python
headers = {'Authorization': 'Bearer ' + auth_token}
r = requests.get(url, headers=headers)
```

#### Using URL Parametes

```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('http://httpbin.org/get', params=payload)

print(r.url)
#http://httpbin.org/get?key2=value2&key1=value1
```

#### Post Payloads

Form-encoded

```python
payload = {'key1': 'value1', 'key2': 'value2'}

r = requests.post("https://httpbin.org/post", data=payload) #form-encoded
r = requests.post(url, data=json.dumps(payload))#raw string
```

#### Cookies

```python
cookies = {"hi": 'there'}
r = requests.get(url, cookies=cookies)
```

### Responses

```python
r.text #u'[{"repository":{"open_issues":0,"url":"https://github.com/...
r.encoding #'utf-8'
r.status_code == requests.codes.ok
r.headers
r.json() #builtin json decoder
```

To get bit representation(turn into Image) `i = Image.open(BytesIO(r.content))`

Checking response r.headers
