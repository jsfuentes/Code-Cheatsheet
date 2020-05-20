# Migration

When you run ecto.migration, it uses the db's schema_migration table to know which migrations have yet run

```
mix phx.gen.migration [file_name]
```

### Example File

Change defines an up and down allowing rollback of db changes

```elixir
defmodule ReactPhoenix.Repo.Migrations.ChangeGid do
  use Ecto.Migration

  def change do
    alter table(:users) do
      add :address, string
      add :usertype_id, references(:usertypes, on_delete: :nothing)
      modify :title, :text
  remove :views
    end
  end
end

```

