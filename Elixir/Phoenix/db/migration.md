# [Migration](https://hexdocs.pm/ecto_sql/Ecto.Migration.html)

DB schema_migration table used to know which migrations have yet to run 

### Usage

1) `mix ecto.gen.migration [action_name]`

2)  Edit in priv/repo/migrations

```elixir
defmodule ReactPhoenix.Repo.Migrations.ChangeGid do
  use Ecto.Migration

  def change do
    alter table(:users) do
      add :address, :string
      add :usertype_id, references(:usertypes, on_delete: :nothing)
      add :event_id, references(:usertypes, on_delete: :delete_all, type: :string)
      add :my_array, {:array, inner_type}
      modify :title, :text
  		remove :views
    end
    
    #rename is outside alter statement
    rename table(:subevents), :parent, to: :event_id
    
    #order matters, if another column depends should remove before dropping
    drop table(:registration_question_options)
  end
end
```

3) `mix ecto.migrate`

*Can undo with `mix ecto.rollback`*

## UUID 

Creating (will be uuid in table)

```elixir
defmodule ReactPhoenix.Repo.Migrations.CreateUsers do
  use Ecto.Migration

  def change do
    create table(:users, primary_key: false) do
      add :id, :binary_id, primary_key: true
```

Referencing

```elixir
defmodule ReactPhoenix.Repo.Migrations.CreateEvents do
  use Ecto.Migration

  def change do
    create table(:events) do
      add :user_id, references(:users, [on_delete: :nothing, type: :binary_id])
```

Then you have to generate it when you create it, `Ecto.UUID.generate()`

### On delete

```elixir
add :user_id, references(:users, on_delete: :nothing)
```

- `:nothing` - if any referencing rows still exist when the constraint is checked, an error is raised; this is the default behavior if you do not specify anything.
- `:delete_all` - specifies that when a referenced row is deleted, row(s) referencing it should be automatically deleted as well
- `:nilify_all` - causes the referencing column(s) in the referencing row(s) to be set to `nil` when the referenced row is deleted
- `:restrict` - prevents deletion of a referenced row. It will fail if there is a referenced object.

### More Example File

Change defines an up and down allowing rollback of db changes

```elixir
defmodule ReactPhoenix.Repo.Migrations.CreateUsers do
  use Ecto.Migration

  def change do
    create table(:users, primary_key: false) do
      add :id, :string, primary_key: true
      add :name, :string
      add :picture, :string
      add :email, :string
      add :locale, :string
      add :gid, :string
      add :gaccess_token, :string
      add :type, :string

      timestamps()
    end
    
    create unique_index(:users, [:email])
  end
end
```

