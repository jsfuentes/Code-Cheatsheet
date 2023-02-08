# Requests/Routing

GET should be idempotent and append things to a querystring
POST is for data to be processed

| Code                 | Contains                                                     |
| -------------------- | ------------------------------------------------------------ |
| `request.args`       | the key/value pairs in the **URL query string**              |
| `request.form`       | the key/value pairs in the **body**, from a HTML post form, or JavaScript request that isn't JSON encoded |
| `request.values`     | combined `args` and `form`, preferring `args` if keys overlap |
| `request.files`      | files in the body, which Flask keeps separate from `form`. HTML forms must use `enctype=multipart/form-data` or files will not be uploaded. |
| `request.data`       | mimetype Flask does not handle as string                     |
| `request.get_json()` | Get JSON body from a post request                            |

## SIMPLE GET ROUTES

Default methods is just get

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

## Combo

```python
@app.route('/login', methods=['POST', 'GET'])
def login():
    error = None
    if request.method == 'POST':
        if valid_login(request.form['username'],
                       request.form['password']):
            return log_the_user_in(request.form['username'])
        else:
            error = 'Invalid username/password'
    # the code below is executed if the request method
    # was GET or the credentials were invalid
    return render_template('login.html', error=error)
```

