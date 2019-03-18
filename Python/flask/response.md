# RESPONSES

```python
resp = Response(js, status=200, mimetype='application/json')
## ORRRR
resp = jsonify(data)
resp.status_code = 200
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

## End Early Status Code

from flask import abort
abort(404)