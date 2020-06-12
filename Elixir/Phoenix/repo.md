# Repo

Interact with DB/schemas usually in public context like Accounts

```elixir
alias ReactPhoenix.Repo
```

## [Commands]([Repo commands](https://hexdocs.pm/ecto/Ecto.Repo.html))

##### Get

```elixir
Repo.get(User, id) #nil or %User{}
Repo.get!(User, id) #error or %User
MyRepo.get_by(Post, title: "My post") #get


Repo.all(User)
Repo.all(from u in User, select: u.email, where: u.age == ^age)

Repo.one(from u in User, where: ilike(u.email, "%1%"), select: count(u.id))  # # of users with 1 in their email
```

See query for more complex stuff

##### Insert

```elixir
Repo.insert(%User{email: "user1@example.com"}) 
#{:ok, [new User object...]}
```

##### Preload

```elixir
def get_event!(id) do
  Repo.get!(Event, id)
  |> Repo.preload(:subevents)
end
```

### [Query](https://hexdocs.pm/ecto/Ecto.Query.html#content)

Supports literal Integers, Floats, Bools, Binary(<<1, 2 >>), Strings, and arrays, other external variables must be pinned`^`. Using with Schema(`User` instead of `"users"`) lets it know what type to cast to and automatically retrieves all fields

```elixir
query = from u in User, where: u.age == ^age and u.height > ^(height_ft * 3.28)

#Can explicitly cast type
query = from u in "users", where: u.age > type(^age, :integer), select: u.name

#List of map from id to email
query = from u in User, select: %{u.id => u.email}) 

query = "users"
|> where([u], u.age > 18)
|> select([u], u.name)

#Complex child query stuff idk
child_query = from c in Comment, where: parent_as(:posts).id == c.post_id
query = from p in Post, as: :posts, join: c in subquery(child_query)

Repo.all(query)
```

Testing in IEX

```elixir
import Ecto.Query
uid = "34547f91-ffaa-4f03-8a0f-e63daaeced0b"
ReactPhoenix.Repo.all(from m in ReactPhoenix.Events.Meeting, where: m.user1_id == ^uid) # use pin to use external var
```

### Advanced

Composing queries

```elixir
# Create a query
query = from u in User, where: u.age > 18

# Extend the query
query = from u in query, select: u.name
```

