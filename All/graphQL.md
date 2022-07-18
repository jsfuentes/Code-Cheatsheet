# GraphQL

Declarative way to ask for data from server for any language, its a specification and has many different libs

Benefits:

- Insightful analytics by data accesses
- Uses strong type system to define capabilities of an API so **frontend and backend** work independently
- Frontend just asks for data they need, no interaction, knowledge of sources, or request needed allowing fast solo iteration

Use cases:

1) GraphQL with connected database, single web server that implements GraphQL server

2) GraphQL server weak layer infront of existing systems to unify and hide complexity, doesn't care about sources whether third-party apis, legacy systems, etc

3) Hybrid

## GraphQL vs REST for Frontend

#### REST

Rest has stateless servers & structured access and currently overused term

Rest would have:

```
/users/<id>
/users/<id>/posts
/users/<id>/followers
```

Could change api to be exactly what the page needs, but doesn't allow fast frontend iteration

#### GraphQL

One graphql url with a post request specifying what you want

## Schema Definition Language(SDL)

-! means required

Define a one to many relationship:

```graphql
type Person {
	id: ID!
	name: String! 
	age: Int!
	posts: [Post!]!
}

type Post {
	title: String!
	author: Person! 
}
```

### Root Types

This defines ALL queries, mutations, and subscriptions

```
type Query {
	allPersons(last: Int): [Person!]!
}

type Mutation {
	createPerson(name: String!, age: String!): Person!
	updatePerson(id: ID!, name: String!, age: String!): Person!
	deletePerson(id: ID!): Person!
}

type Subscription {
	newPerson: Person!
	updatedPerson: Person!
	deletePerson: Person!
}
```

## Define a Query

```
{
	allPersons {
		name
			posts {
				title
			}
	}
}
```

#### Modifiers

```
{
	allPersons(last: 2) {
		name
	}
}
```

## Writing Data with Mutations

Creating, updating, and deleting

```json
mutation {
	createPerson(name: "Bob", age: 36) {
    name
    age
  }
}
```

Server responds with information shaped by mutation send

```
{
	"createPerson": {
		"name": "Bob",
		"age": 36
	}
}
```

### Subscriptions

Continuous connection that will push data

```
subscription {
	newPerson {
		name
		age
	}
}
```

## Resolver

Graphql queries/mutations consists of set of fields 

Server have one resolver function per field to fetch data

If query is:

```
query {
	User(id: "er3txsa8jklf") {
		name
		friends(first: 5) {
			name age
		}
	}
}
```

Resolvers needed are:

```
User(id: String!): User
name(user: User!): String!
age(user: User!: Int!)
friends(first: Int, user: User!): [User!]
```

## Development Server

http://localhost:8000/___graphql

Press Ctrl + Space (or use Shift + Space as an alternate keyboard shortcut) to bring up the autocomplete window and Ctrl + Enter to run the GraphQL query. 