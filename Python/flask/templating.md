# Templating

## Basics

`{{ to insert }}`

`{% control %}`

### Linking

`url_for('static', filename='bootstrap/bootstrap.min.css') }}`

### BLOCKS

```pytho
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

