# SQL Alchemy

ORM for SQL python

## Models

```python
from typing import Optional
from sqlalchemy import ForeignKey
from sqlalchemy import String
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column
from sqlalchemy.orm import relationship

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "user_account"

    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(30))
    fullname: Mapped[Optional[str]]

    addresses: Mapped[list["Address"]] = relationship(
        back_populates="user", cascade="all, delete-orphan"
    )

    def __repr__(self) -> str:
        return f"User(id={self.id!r}, name={self.name!r}, fullname={self.fullname!r})"

class Address(Base):
    __tablename__ = "address"

    id: Mapped[int] = mapped_column(primary_key=True)
    email_address: Mapped[str]
    user_id: Mapped[int] = mapped_column(ForeignKey("user_account.id"))

    user: Mapped["User"] = relationship(back_populates="addresses")

    def __repr__(self) -> str:
        return f"Address(id={self.id!r}, email_address={self.email_address!r})"
```

## Usage

#### Session

**Must use session for all transactions and `session.commit` if you write data**

```python
# Option 1 Session Maker
Session = sessionmaker(engine)

with Session() as session:
  session.add(object)
  session.commit()
  
# Option 2 
from sqlalchemy.orm import Session

engine = create_engine("postgresql://scott:tiger@localhost/")

with Session(engine) as session:
    session.add(some_object)
    session.add(some_other_object)
    session.commit()
```

#### Querying

v2

```python
# query from a class
statement = select(User).filter_by(name="ed")

# list of first element of each row (i.e. User objects)
result = session.execute(statement).scalars().all()

# query with multiple classes
statement = select(User, Address).join("addresses").filter_by(name="ed")

# list of tuples
result = session.execute(statement).all()

# query with ORM columns
statement = select(User.name, User.fullname)

# list of tuples
result = session.execute(statement).all()
```

V1

```python
# query from a class
results = session.query(User).filter_by(name="ed").all()

# query with multiple classes, returns tuples
results = session.query(User, Address).join("addresses").filter_by(name="ed").all()

# query using orm-columns, also returns tuples
results = session.query(User.name, User.fullname).all()
```

#### Insert

```python
patrick = User(name="patrick", fullname="Patrick Star")
session.add_all([spongebob, sandy, patrick])
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



## Relationships

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

