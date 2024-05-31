# RESPONSES

```python
from flask import Flask, jsonify, make_response

def index():
  #auto sets status code to 200
	return jsonify(data)
	#return 'hi'
  #return make_response("Wrong password", 401)

```

ORRRR

```python
resp = Response(js, status=200, mimetype='application/json')
```

### Render Template

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

response = jsonify({'message': message})
response.status_code = 400
return response
```