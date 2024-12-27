# [Prisma*](https://prisma-client-py.readthedocs.io/)

Uses async-io, dont forget to add client generator

```
generator client_py {
  provider             = "prisma-client-py"
  recursive_type_depth = 5
}
```

## Setup

```bash
pip install prisma
```

## Usage

```python
from prisma import Prisma

db = Prisma()
await db.connect()

# CRUD operations
user = await db.user.create(data={"name": "Alice"})
users = await db.user.find_many()
updated = await db.user.update(where={"id": 1}, data={"name": "Bob"})
deleted = await db.user.delete(where={"id": 1})

await db.disconnect()
```