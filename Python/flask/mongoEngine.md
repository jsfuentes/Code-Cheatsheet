# flask_mongoengine

## Setup

```python
db = MongoEngine() #Database connection data in config

db.init_app(app)
```

### Config

```python
class DevelopmentConfig(Config):
    DEBUG=True
    #Mongoengine Variables
    MONGODB_HOST='mongodb://admin:admin@ds014648.mlab.com:14648/wissen'
    MONGODB_DB='wissen'

app.config.from_object(config[config_name])
config[config_name].init_app(app)
```

## Making Models

### Schema

```python
from mongoengine import Document, EmbeddedDocument, StringField, IntField, FileField, EmbeddedDocumentField, ListField, BooleanField, SortedListField, DateTimeField, ReferenceField

class Image(Document):
    img = FileField() #GridGS

class User(UserMixin, Document): # UserMixin for flask_login
    email = EmailField(required=True)
    password_hash = StringField()
    username = StringField()
    imgs = ListField(EmbeddedDocumentField(Image))
```

### Creation

```python
profile = Profile(first=form['first'], last=form['last'], gender=form['gender'][0], age=form['age'], bio=form['bio'], location=form['location']) 
```

### Images Add Photo

```python
file = request.files['profile_image']
profile.photo.new_file()
profile.photo.write(file)
profile.photo.close()
profile.photo = current_user.profile.photo
current_user.profile = profile

#Save to DB
current_user.save()
```

####Retrieve Img

img = Image.objects()[0].img.read()

## Access

```python
for user in User.objects(username='jfuentes'):
	print(user.email)
```



