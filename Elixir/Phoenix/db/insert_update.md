# Insert/Update

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

