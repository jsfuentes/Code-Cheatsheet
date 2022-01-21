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
Repo.all(from u in User, select: u.email, where: u.age == ^age) #[...]

Repo.one(from u in User, where: ilike(u.email, "%1%"), select: count(u.id))  # of users with 1 in their email
Repo.one(from ea in EventAnalytics, where: ea.email == "j@g" and ea.type == "RSVP") #will error if > one response, nil if none
```

See query for more complex stuff

*If variable is nil, don't just compare use is_nil*

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

`:inner_join`, `:left_join`, `:right_join`, `:cross_join`, `:full_join`, `:inner_lateral_join` or `:left_lateral_join`. `:join` is equivalent to `:inner_join`(match both returned)

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

```elixir
Repo.all(
  from q in Question,
  where: q.subevent_id == ^subevent_id,
  preload: [:user],
  left_join: qu in QuestionUpvote,
  on: qu.question_id == q.id,
  group_by: [q.id],
  select: %{question: q, upvotes: count(qu.id)}
)
```

##### Preload

Can be used very similarly to a join, and keeps proper select and structure

```elixir
def get_event!(id) do
  Repo.get!(Event, id)
  |> Repo.preload(:subevents)
end

Repo.all(from q in Question, where: q.subevent_id == ^subevent_id,  preload: [user])

# seperating ra_query first gets all the reqs then fills in the association(if joined with where it wouldn't return reqs without ra with the right email)
ra_query = from ra in RegistrationAnswer, where: ra.email == ^email

Repo.all(from req in RegistrationEventQuestion,
  where: req.event_id == ^event_id,
  preload: [registration_answers: ^ra_query],
  select: req)
 
```

I think both do two queries: [in query](https://hexdocs.pm/ecto/Ecto.Query.html#preload/3)

#### Insert

```elixir
Repo.insert(%User{email: "user1@example.com"}) 
#{:ok, [new User object...]}
```

#### Update

Unlike insert, get, or delete, update NEEDS a changeset

```elixir
user
|> User.changeset(attrs)
|> Repo.update()
# {:ok, %User{} = user}
    
MyRepo.update_all(Post, set: [title: "New title"])

MyRepo.update_all(Post, inc: [visits: 1])

from(p in Post, where: p.id < 10, select: p.visits)
|> MyRepo.update_all(set: [title: "New title"])
```

### Advanced

#### Insert or Update, [Upsert](https://hexdocs.pm/ecto/constraints-and-upserts.html)

Works most of the time:

```elixir
result =
  case MyRepo.get(Post, id) do
    nil  -> %Post{id: id}
    post -> post
  end
  |> Post.changeset(changes)
  |> MyRepo.insert_or_update

# {:ok, struct} or {:error, changeset}
```

##### Race condition immune

Method 1:

*note a unique index must be on daily_recording_id

```elixir
    %Recording{}
    |> Recording.changeset(attrs)
    |> Repo.insert(on_conflict: :nothing, conflict_target: :daily_recording_id)
```

Method 2, reget on changeset error:

```elixir
case get_chat_channel(attrs) do
  %ChatChannel{} = cc -> cc

  nil ->
  	case create_chat_channel(attrs) do
  		{:ok, cc} -> cc

  		{:error,
  			%Ecto.Changeset{
  				errors: [
  					unique_constraint:
  					{"has already been taken",
  						[constraint: :unique, constraint_name: "chat_channels_unique_index"]}
  				]
  			}} ->
  			%ChatChannel{} = cc = get_chat_channel(attrs)
end
```

#### Composing queries

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

