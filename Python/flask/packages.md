## Notable Packages

### MongoEngine
`from flask_mongoengine import MongoEngine`
- app.config['MONGODB_DB'] = 'project1'
- app.config['MONGODB_HOST'] = '192.168.1.35'
- app.config['MONGODB_PORT'] = 12345
- app.config['MONGODB_USERNAME'] = 'webapp'
- app.config['MONGODB_PASSWORD'] = 'pwd123'


## LoginManager
`from flask_login import LoginManager`
- [Great Docs](https://flask-login.readthedocs.io/en/latest/)

## Bootstrap
Basically provides macros, I would just use regular bootstrap as fun as abstracting away form creation is 
```py
from flask_bootstrap import Bootstrap
```

```html
{% extends "bootstrap/base.html" %}
{% block title %}This is an example page{% endblock %}

{% block navbar %}
<div class="navbar navbar-fixed-top">
  <!-- ... -->
</div>
{% endblock %}

{% block content %}
  <h1>Hello, Bootstrap</h1>
{% endblock %}
```
