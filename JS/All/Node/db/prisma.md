# Prisma

- ORM with typesafe client generation and UI
- works across db types including Postgres and MongoDB

## Setup*

```bash
npm install prisma --save-dev
npx prisma init #create a `schema.prisma` file
#edit schema
npx prisma generate
npx prisma migrate dev --name init #for dev, generates migrations and client
npx prisma deploy #for prod wont reset stuff, w/o protection
```

## Usage

```bash
 prisma studio #open explorer
```

### Schema

```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  name    String?
  role    Role     @default(USER)
  posts   Post[]
  profile Profile?
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  user   User   @relation(fields: [userId], references: [id])
  userId Int    @unique
}

model Post {
  id         Int        @id @default(autoincrement())
  createdAt  DateTime   @default(now())
  updatedAt  DateTime   @updatedAt
  title      String
  published  Boolean    @default(false)
  author     User       @relation(fields: [authorId], references: [id])
  authorId   Int
  categories Category[]
}

model Category {
  id    Int    @id @default(autoincrement())
  name  String
  posts Post[]
}

enum Role {
  USER
  ADMIN
}
```

### Client*

src/utils/prisma.ts

```ts
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export default prisma;
```

Query

```ts
const corpus = await prisma.corpus.findMany({
  where: { caseId: Number(caseId) },
  orderBy: { createdAt: "desc" },
});

const caseData = await prisma.case.findUnique({
  where: { id: parseInt(id as string) },
  include: { answers: true },
});
```

- .findUniqueOrThrow

Create

```ts
const newCase = await prisma.case.create({
  data: {
    form: { connect: { id: formId } },
    answers: {
      create: answers.map(
        (a: { value: string; formQuestionId: number }) => ({
          value: a.value,
          formQuestion: { connect: { id: a.formQuestionId } },
        })
      ),
    },
  },
});

const result = await prisma.user.createMany({
  data: [
    { name: 'Bob', email: 'bob@prisma.io' },
    { name: 'Yewande', email: 'yewande@prisma.io' },
    // ... more records
  ],
  skipDuplicates: true
})
```

Update

```ts
const updatedCase = await prisma.case.update({
        where: { id: parseInt(id) },
        data: {
          form: { connect: { id: formId } },
          answers: {
            deleteMany: {
              id: {
                notIn: answers
                  .map((a: { id?: number }) => a.id)
                  .filter((id): id is number => id !== undefined),
              },
            },
            upsert: answers.map(
              (a: { id?: number; value: string; formQuestionId: number }) => ({
                where: { id: a.id || -1 },
                update: { value: a.value },
                create: {
                  value: a.value,
                  formQuestion: { connect: { id: a.formQuestionId } },
                },
              })
            ),
          },
        },
      });
```

## Advanced

##### pg_vector?

````ts
await prisma.$executeRaw`
  ALTER TABLE "VectorizedItem"
  ADD COLUMN "embedding_512" vector(512);
`;
````

##### Transactions

Ensure all or none of operations succeed, commited when end of transaction reached

```ts
// sequential operations
const [posts, totalPosts] = await prisma.$transaction([
  prisma.post.findMany({ where: { title: { contains: 'prisma' } } }),
  prisma.post.count(),
])

//interactive transactions
function transfer(from: string, to: string, amount: number) {
  return prisma.$transaction(async (tx) => {
    // 1. Decrement amount from the sender.
    const sender = await tx.account.update({
      data: {
        balance: {
          decrement: amount,
        },
      },
      where: {
        email: from,
      },
    })

    // 2. Verify that the sender's balance didn't go below zero.
    if (sender.balance < 0) {
      throw new Error(`${from} doesn't have enough to send ${amount}`)
    }

    // 3. Increment the recipient's balance by amount
    const recipient = await tx.account.update({
      data: {
        balance: {
          increment: amount,
        },
      },
      where: {
        email: to,
      },
    })

    return recipient
  })
}
```

### Gotchas

hidden: {not: true} doesn't return null values, https://github.com/prisma/prisma/issues/24252, instead do below

```ts
return await prisma.priorAuth.findMany({
    where: {
       OR: [
         {
           hidden: {
              not: true,
           },
         },
         {
           hidden: null,
         },
      ],
   }
}
```



