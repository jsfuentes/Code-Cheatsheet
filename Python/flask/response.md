# RESPONSES

```python
def index():
	return 'hi'
```

### JSON Response

```python
resp = Response(js, status=200, mimetype='application/json')
```

ORRRRRRR

```python
resp = jsonify(data)
```

## Render Template

```python
from flask import render_template

@app.route('/hello/')
@app.route('/hello/<name>')
def hello(name=None):
    return render_template('hello.html', name=name)
```

Default is template folder

#### Send File

```python
	return send_file('/var/www/PythonProgramming/PythonProgramming/static/images/python.jpg', attachment_filename='python.jpg')

```

## End Early Status Code

```python
from flask import abort
abort(404)
```