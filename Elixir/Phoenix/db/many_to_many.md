# [Many to Many](https://hexdocs.pm/ecto/polymorphic-associations-with-many-to-many.html)

`many_to_many` [association](https://elixirschool.com/en/lessons/ecto/associations/#many-to-many) happens through a join schema or source, containing foreign keys to the associated schemas. For example, the association below:

```elixir
# from MyApp.Post
many_to_many :tags, MyApp.Tag, join_through: "posts_tags"
#is backed by relational databases through a join table as follows:
[Post] <-> [posts_tags] <-> [Tag]
  id   <--   post_id
              tag_id    -->  id
```

## Step by Step Guide

1)  Create Tables

```elixir
create table("todo_lists") do
  add :title
  timestamps()
end

create table("todo_items") do
  add :description
  timestamps()
end

create table("todo_list_x_items", primary_key: false) do
  add :todo_item_id, references(:todo_items)
  add :todo_list_id, references(:todo_lists)
  #timestamps()
end
```

[No id recommended for join tables](https://blog.jooq.org/2019/03/26/the-cost-of-useless-surrogate-keys-in-relationship-tables/), basically because it creates the a useless "primary" index tree in db data structure

2) Create Schemas

```elixir
defmodule MyApp.TodoList do
  use Ecto.Schema

  schema "todo_lists" do
    field :title
    many_to_many :todo_items, MyApp.TodoItem,
      join_through: MyApp.TodoListItem
    timestamps()
  end
end

defmodule MyApp.TodoListXItem do
  use Ecto.Schema

  schema "todo_list_items" do
    belongs_to :todo_list, MyApp.TodoList
    belongs_to :todo_item, MyApp.TodoItem
    timestamps()
  end
end

defmodule MyApp.TodoItem do
  use Ecto.Schema

  schema "todo_items" do
    field :description
    timestamps()
  end
end
```

3) Inserting Data

In this form

```elixir
%{"todo_list" => %{
  "title" => "shipping list",
  "todo_items" => %{
    0 => %{"description" => "bread"},
    1 => %{"description" => "eggs"},
  }
}}
```

With these changesets

```elixir
# In MyApp.TodoList
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:title])
  |> Ecto.Changeset.cast_assoc(:todo_items, required: true)
end

# And then in MyApp.TodoItem
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:description])
end
```

