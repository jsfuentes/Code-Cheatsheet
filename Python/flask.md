# Flask

## GET VS POST
Get should be idempotent and appended things to a querystring
Post is for data to be processed

## SIMPLE GET ROUTES
```python
@app.route('/users/<userid>', methods = ['GET'])
def api_users(userid):
    users = {'1':'john', '2':'steve', '3':'bill'}

    if userid in users:
        return jsonify({userid:users[userid]})
    else:
        return not_found()
```

## SIMPLE REQUEST READING
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

## RESPONSES
```python
resp = Response(js, status=200, mimetype='application/json')
## ORRRR
resp = jsonify(data)
resp.status_code = 200
```

## TEMPLATING
### BLOCKS

```html
//layout.html
<!doctype html>
<title>My Application</title>
{% with messages = get_flashed_messages() %}
  {% if messages %}
    <ul class=flashes>
    {% for message in messages %}
      <li>{{ message }}</li>
    {% endfor %}
    </ul>
  {% endif %}
{% endwith %}
{% block body %}{% endblock %}

//index.html
{% extends "layout.html" %}
{% block body %}
  <h1>Overview</h1>
  <p>Do you want to <a href="{{ url_for('login') }}">log in?</a>
{% endblock %}
```

## FLASH
```python
From flask import flash
@app.route('/login', methods=['GET', 'POST'])
def login():
	…..
flash('You were successfully logged in')
```
