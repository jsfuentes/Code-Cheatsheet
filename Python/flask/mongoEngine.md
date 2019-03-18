# flask_mongoengine

`from flask_mongoengine import MongoEngine`

Mongoengine is a Document-Object Mapper (think ORM, but for document databases)

Easy access to database collections and enforced schema 

Uses pymongo under the surface

## Setup

```python
db = MongoEngine() #Database connection data in config

db.init_app(app) # In create app factory
```

### Config

You need to define the host, the /after the url can say the db name

```python
class DevelopmentConfig(Config):
    DEBUG=True
    #Mongoengine Variables
    MONGODB_HOST='mongodb://[username]:[password]@ds014648.mlab.com:14648/wissen'

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
    friends = ListField(ReferenceField(User))
```

EmbeddedDocumentField includes the object in the model

ReferenceField can be used to include reference ids that are lazily dereferenced on access

### Creation

```python
profile = Profile(first=form['first'], last=form['last'], gender=form['gender'][0], age=form['age'], bio=form['bio'], location=form['location']) 
```

## Access

You need to define and import the model

`User.objects` => return all objects 

`Page.objects(author__country='uk')` => Query in embedded docs

` Users.objects(age__lte=18)`=>  Query users with age less or equal

`User.objects[:5]` => only first 5 people(??throw error if not exist??)

`User.objects.first()` => retrieve first result or None if it doesnt exist

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

