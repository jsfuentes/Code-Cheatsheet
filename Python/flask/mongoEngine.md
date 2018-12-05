# flask_mongoengine

Mongoengine is a Document-Object Mapper (think ORM, but for document databases)

Easy access to database collections and enforced schema 

## Setup

```python
db = MongoEngine() #Database connection data in config

db.init_app(app) # In create app factory
```

### Config

You need to define host and db 

```python
class DevelopmentConfig(Config):
    DEBUG=True
    #Mongoengine Variables
    MONGODB_HOST='mongodb://[username]:[password]@ds014648.mlab.com:14648/wissen'
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

## Access

You need to define and import a models called User

```python
for user in User.objects(username='jfuentes'):
	print(user.email)
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

