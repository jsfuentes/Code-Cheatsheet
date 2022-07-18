## Notable Packages

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
