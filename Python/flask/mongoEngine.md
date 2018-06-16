# flask_mongoengine
```py
from mongoengine import Document, EmbeddedDocument, StringField, IntField, FileField, EmbeddedDocumentField, ListField, BooleanField, SortedListField, DateTimeField, ReferenceField

class Image(Document):
    img = FileField() #GridGS

class User(UserMixin, Document): # UserMixin for flask_login
    email = EmailField(required=True)
    password_hash = StringField()
    username = StringField()
    imgs = ListField(EmbeddedDocumentField(Image))
```

```py
db = MongoEngine() #Database connection data in config
db.init_app(app)
```


In config file
```py
class DevelopmentConfig(Config):
    DEBUG=True
    #Mongoengine Variables
    MONGODB_HOST='mongodb://admin:admin@ds014648.mlab.com:14648/wissen'
    MONGODB_DB='wissen'

app.config.from_object(config[config_name])
config[config_name].init_app(app)
```

```py
profile = Profile(first=form['first'], last=form['last'], gender=form['gender'][0], age=form['age'],
                        bio=form['bio'], location=form['location']) #need photo

file = request.files['profile_image']

print file.filename
```

### Images Filename

```py
profile.photo.new_file()
profile.photo.write(file)
profile.photo.close()
profile.photo = current_user.profile.photo

current_user.profile = profile
current_user.save()
```

# Retrieve Img
img = Image.objects()[0].img.read()
