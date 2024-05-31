# [LoginManager](https://flask-login.readthedocs.io/en/latest/)

## Setup

```python
from flask_login import LoginManager`

login_manager = LoginManager()
login_manager.init_app(app)

@login_manager.user_loader
def load_user(user_id):
    user = db_get_user(user_id)
    if not user:
        print("Invalid user id in request. Has this user id been deleted?")
        # returning None deletes the session
        return None

    print("LOAD USER", user.get_id())
    return user

```

User object should implement some functions or inherit from `UserMixin`

## Usage

#### Make Login Required For Routes

`@login_required` decorator will make route reroute to route set by `login_manager.login_view = "users.login"` 

### Login

```python
from flask_login import login_user`

login_user(user)
login_user(user, remember=True)#store cookie to remember me
```

#### Logout

```python
@app.route("/logout")
@login_required
def logout():
    logout_user()
    return redirect(somewhere)
```

#### Use current_user to access

```python
@bp.route("/me", methods=["POST"])
def guess_user():
    if current_user.is_authenticated:
        return jsonify(current_user.as_dict())
```

#### Templates

Make current_user available in every template

```html
{% if current_user.is_authenticated %}
  Hi {{ current_user.name }}!
{% endif %}
```