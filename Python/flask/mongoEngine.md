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

[Potential Field](<http://docs.mongoengine.org/guide/defining-documents.html#fields>)

#### Schema

Derive from EmbeddedDocument(embed in other docs), Document, or DynamicDocument(any fields will be saved)

```python
from mongoengine import Document, EmbeddedDocument, StringField, IntField, FileField, EmbeddedDocumentField, ListField, BooleanField, SortedListField, DateTimeField, ReferenceField

class Profile(EmbeddedDocument):
    first = StringField(max_length=50)
    last = StringField(max_length=50)
    gender = StringField(max_length=1, choices=GENDERS)
    age = IntField()
    photo = FileField() #GridGS
    bio = StringField()
    location = StringField()
```

#### Connecting Models

EmbeddedDocumentField includes the object in the model

ReferenceField can be used to include reference ids that are lazily dereferenced on access

```python
class User(UserMixin, Document):
    cid = ReferenceField('Connection')
    profile = EmbeddedDocumentField(Profile, required=True)
    #...
```

## Creation

```python
profile = Profile(first=form['first'], last=form['last'], gender=form['gender'][0], age=form['age'], bio=form['bio'], location=form['location']) 
profile.save()
```

An id is created automatically on save: `profile.id` , convert to string with `str(profile.id)`

Set id by adding `primary_key=True` to Field and it will be aliased to id

#### Images Add Photo

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

##### Retrieve Img

img = Image.objects()[0].img.read()

## Query

You need to define and import the model

```python
#return all objects 
User.objects 
#Query in embedded docs
Page.objects(author__country='uk') 
#only first 5 people(??throw error if not exist??)
User.objects[:5] 
# retrieve first result or None if it doesnt exist
User.objects.first()
for user in User.objects(username='jfuentes'):
	print(user.email)
```

#### Operators

Double underscore after field to do operator

- `in` – value is in list (a list of values should be provided)

```python
#Query users with age less or equal
Users.objects(age__lte=18)
```

#### Advanced

```python
Page.objects(__raw__={'tags': 'coding'})
```

```python
class Page(Document):
    tags = ListField(StringField())
# This will match all pages that have the word 'coding' as an item in the 'tags' list
Page.objects(tags='coding')
```



