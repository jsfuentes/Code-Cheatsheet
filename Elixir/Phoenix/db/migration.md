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
      modify :title, :text
  		remove :views
    end
    
    #rename is outside alter statement
    rename table(:subevents), :parent, to: :event_id
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

