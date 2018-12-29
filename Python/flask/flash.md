# Flash

.py

```python
from flask import flash

@app.route('/login', methods=['GET', 'POST'])
def login():
	#...
	flash('You were successfully logged in')
```

.html

```jinja2
{% with messages = get_flashed_messages() %}
  {% if messages %}
    <ul class=flashes>
    {% for message in messages %}
      <li>{{ message }}</li>
    {% endfor %}
    </ul>
  {% endif %}
{% endwith %}
```



