# Templating

Jinja2 is the [flask templating language](http://jinja.pocoo.org/docs/2.10/templates/#defined); heavily inspired by Python and Django

Template Variables are passed in as named parameters by the render_template ft

## Basics

`{{ to insert }}`

`{% control %}`

`{# comment #}`

### Control

```jinja2
{% for topic in NAVBAR_LIST %}
    <div> {{topic}} </div>
    <div> {{topic}} </div>
{% endfor %}
```

```jinja2
{% if variable is defined %}
    value of variable: {{ variable }}
{% else %}
    variable is not defined
{% endif %}
```

## Filters

Basically pipes like helpers in handlebars

`{{ companies|tojson }}` #turn companies into json

## BLOCKS

Extend to leave common elements

 You can override and fill in blocks

**layout.html**

```jinja2
<!doctype html>
<html>
    <head>
        {% block head %}
            <link rel="stylesheet" href="{{ url_for('static', filename='base.css') }}">
        {% endblock %}
    </head>
    <body>
        <div id="content">
            {% block content %}{% endblock %}		</div>
	</body>
</html>
```

**index.html**

```jinja2
{% extends "layout.html" %}
{% block head %}
    <link rel="stylesheet" href="{{ url_for('static', filename='admin.css') }}">
{% endblock %}
{% block body %}
  <h1>Overview</h1>
  <p>Do you want to <a href="{{ url_for('login') }}">log in?</a>
{% endblock %}
```

## Macros

```jinja2
{% macro input(name, value='', type='text', size=20) -%}
    <input type="{{ type }}" name="{{ name }}" value="{{
        value|e }}" size="{{ size }}">
{%- endmacro %}
```

The macro can then be called like a function in the namespace:

```jinja2
<p>{{ input('username') }}</p>
<p>{{ input('password', type='password') }}</p>
```

### Linking with url_for

##### No Blueprint

```python
@app.route('/login')
def login():
    return 'login'

@app.route('/user/<username>')
def profile(username):
    return '{}\'s profile'.format(username)
    
print(url_for('profile', username='John Doe'))
```

```jinja2
{{ url_for('static', filename='bootstrap/bootstrap.min.css') }}
{{url_for('login')}} 
/login
{{url_for('profile', username='John Doe')}} #/user/John%20Doe
```

If there was a blueprint named main, us`'main.login'`