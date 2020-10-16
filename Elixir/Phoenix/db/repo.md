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
MyRepo.get_by(Post, title: "My post") #error if not one result


Repo.all(User)
Repo.all(from u in User, select: u.email, where: u.age == ^age)

Repo.one(from u in User, where: ilike(u.email, "%1%"), select: count(u.id))  # of users with 1 in their email
Repo.one(from ea in EventAnalytics, where: ea.email == "j@g" and ea.type == "RSVP") #will error if > one response, nil if none
```

See query for more complex stuff

*If variable is nil, don't just compare use is_nil*

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
query = from u in User, where: u.age == ^age and u.height > ^(height_ft * 3.28), order_by: u.city, preload: [:company]

#Can explicitly cast type
query = from u in "users", where: u.age > type(^age, :integer), select: u.name

#List of map from id to email
query = from u in User, select: %{u.id => u.email}), where: not is_nil(u.birthday) 

query = "users"
|> where([u], u.age > 18)
|> select([u], u.name)

#Complex child query stuff idk
child_query = from c in Comment, where: parent_as(:posts).id == c.post_id
query = from p in Post, as: :posts, join: c in subquery(child_query)

Repo.all(query)
Repo.one(query) #will error if >1 response
```

Testing in IEX

```elixir
import Ecto.Query
uid = "34547f91-ffaa-4f03-8a0f-e63daaeced0b"
ReactPhoenix.Repo.all(from m in ReactPhoenix.Events.Meeting, where: m.user1_id == ^uid) # use pin to use external var
```

### Join

```elixir
counts_and_events =
  from ea in subquery(count_types),
  join: e in Event,
  on: ea.event_id == e.id,
  where: e.user_id == ^user_id,
  order_by: [desc: e.start_time], 
  #order_by: e.start_time would be asc
  select: %{
    id: ea.event_id,
    title: e.title,
    start_time: e.start_time,
	}
```

#### Update

```elixir
call
|> Call.changeset(attrs)
|> Repo.update()
    
MyRepo.update_all(Post, set: [title: "New title"])

MyRepo.update_all(Post, inc: [visits: 1])

from(p in Post, where: p.id < 10, select: p.visits)
|> MyRepo.update_all(set: [title: "New title"])
```

### Advanced

Composing queries

```elixir
# Create a query
query = from u in User, where: u.age > 18

# Extend the query
query = from u in query, select: u.name
```

##### Fragments

Allow you to define raw SQL

```elixir
  from p in Post,
    where: is_nil(p.published_at) and
           fragment("lower(?)", p.title) == ^title
```

##### Custom Macros

```elixir
defmodule ReactPhoenix.Helpers.QueryMacros do
  defmacro filter(agg, condition) do
    quote do
      fragment("? FILTER(WHERE ?)", unquote(agg), unquote(condition))
    end
  end

  defmacro type_count(id, condition) do
    quote do
      filter(count(unquote(id)), unquote(condition))
    end
  end
end
```

```elixir
  import ReactPhoenix.Helpers.QueryMacros
```

