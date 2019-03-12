# Requests/Routing

GET should be idempotent and append things to a querystring
POST is for data to be processed

| Code             | Contains                                                     |
| ---------------- | ------------------------------------------------------------ |
| `request.args`   | the key/value pairs in the **URL query string**              |
| `request.form`   | the key/value pairs in the **body**, from a HTML post form, or JavaScript request that isn't JSON encoded |
| `request.values` | combined `args` and `form`, preferring `args` if keys overlap |
| `request.files`  | files in the body, which Flask keeps separate from `form`. HTML forms must use `enctype=multipart/form-data` or files will not be uploaded. |
| `request.data`   | mimetype Flask does not handle as string                     |

##SIMPLE GET ROUTES

```python
@app.route('/users/<userid>', methods = ['GET'])
def api_users(userid):
    users = {'1':'john', '2':'steve', '3':'bill'}

    if userid in users:
        return jsonify({userid:users[userid]})
    else:
        return not_found()
```

## SIMPLE POST REQUESTS

Query String

```python
request.args.get('uid')
```

Data sent

```python
from flask import json

@app.route('/messages', methods = ['POST'])
def api_message():

    if request.headers['Content-Type'] == 'text/plain':
        return "Text Message: " + request.data

    elif request.headers['Content-Type'] == 'application/json':
        return "JSON Message: " + json.dumps(request.json)

    elif request.headers['Content-Type'] == 'application/octet-stream':
        f = open('./binary', 'wb')
        f.write(request.data)
                f.close()
        return "Binary message written!"

    else:
        return "415 Unsupported Media Type ;)"
```

## 