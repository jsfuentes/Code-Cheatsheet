# SQL Alchemy

- ORM for SQL python
- 2.0 released 1/26/23 which recommends usage of `select` instead of `query`, so most guides are out of date

**See flask/sqlalchemy for more**

```bash
pip install sqlalchemy
# For PostgreSQL
pip install psycopg2
# For MySQL
pip install pymysql
```

## Usage

#### Querying

```python
from sqlalchemy import select

user = db.session.scalars(select(User).where(User.email == email)).first()


# query with multiple classes, returns list of tuples
result = session.execute(select(User, Address).join("addresses").filter_by(name="ed")).all()

# query with ORM columns, returns list of tuples
result = session.execute(select(User.name, User.fullname)).all()

# Joins, infers the on statement
users = db.session.scalars(select(User).join(Cohort).join(School).where(School.id == school_id)).all()
```

#### Insert

```python
newUser = User(name="patrick", fullname="Patrick Star")
db.session.add(newUser)
#session.add_all([spongebob, sandy, patrick])
session.commit()
```

Insert parent and children

```python
parent = Person(name='Homer')
child = Person(name='Bart')
parent.children.append(child)
child = Person(name='Lisa')
parent.children.append(child)

session.add(parent)
session.commit()
```

## Models

```python
from app.extensions import db, login_manager
from flask_login import UserMixin
from sqlalchemy.sql import func

class User(UserMixin, db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String, nullable=False)
    email = db.Column(db.String, nullable=False)
    password_hash = db.Column(db.String, nullable=True)
    picture = db.Column(db.String, nullable=True)

    inserted_at = db.Column(db.DateTime(timezone=True), server_default=func.now())
    updated_at = db.Column(db.DateTime(timezone=True), onupdate=func.now())
    
    def as_dict(self):
        return {"id": self.id, "password_hash": self.password_hash, "email": self.email, "name": self.name, "picture": self.picture}
      
      
def db_get_user(id):
    user = db.session.scalars(
        select(User).where(User.id == id)).first()
    # print("USER", user)
    return user

## Using UUID
from sqlalchemy.dialects.postgresql import UUID
import uuid

class ResetToken(db.Model):
    id = db.Column(UUID(as_uuid=True), primary_key=True, default=uuid.uuid4)
```

### Relationships

One to many

```python
from sqlalchemy.orm import relationship
from sqlalchemy import Column, String, Integer, Sequence, ForeignKey

class Parent(Base):
    __tablename__ = "parent_table"
    id = Column(Integer, primary_key=True)

    # one-to-many collection
    children = relationship("Child", back_populates="parent")


class Child(Base):
    __tablename__ = "child_table"
    id = Column(Integer, primary_key=True)
    parent_id = Column(Integer, ForeignKey("parent_table.id"))

    # many-to-one scalar
    parent = relationship("Parent", back_populates="children")
    # Note the names of the variables 
```

- "Child" and "Parent" are the names of the table not type of relation
- back_populates uses the variable inside the class as the thing in strings

## Migrating/Creating Tables

Very Rough Code that creates table

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base

db_url = "aldsfjklasvk;lvas;klasdf;klj"
engine = create_engine(db_url)
base = declarative_base()

base.metadata.create_all(engine)
```

Recommended to use `flask-migrate` or 

## Outside of Flask

#### Session

**Must use session for all transactions and `session.commit` if you write data**

```python
# Option 1 Session Maker
Session = sessionmaker(engine)

with Session() as session:
  session.add(object)
  session.commit()
  
# Option 2 
from sqlalchemy import create_engine
from sqlalchemy.orm import Session

engine = create_engine("postgresql://scott:tiger@localhost/")

with Session(engine) as session:
    session.add(some_object)
    session.add(some_other_object)
    session.commit()
```
