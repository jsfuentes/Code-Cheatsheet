# [ChangeSets](https://hexdocs.pm/ecto/Ecto.Changeset.html) and validations

Changesets define data transformations(type casting, filtering, validation)

```elixir
def changeset(%User{} = user, attrs) do
  user
  #mark new data(attrs) and columns to update
  |> cast(attrs, [:name, :email, :bio, :age]) 
  #ensure fields present
  |> validate_required([:name, :email, :bio])
  |> validate_length(:bio, min: 2)
  |> validate_format(:email, ~r/@/)
  |> validate_inclusion(:age, 18..100)
  |> unique_constraint(:email)

end
```

```elixir
changeset = Ecto.Changeset.cast(%User{}, %{"age" => "0"}, [:age])
user = Repo.insert!(changeset)
```

### Validations vs Constraints

Most validations(expect ones marked unsafe) don't require the db

Constraints rely on the db and are always safe

## Advanced

Conditionally validate_required

```elixir
def changeset(chat_channel, attrs) do
  chat_channel
  |> cast(attrs, [:type, :user_id, :event_id, :subevent_id, :group_id])
  |> validate_required([:type])
  |> (fn cs ->
  case get_field(cs, :type) do
      "event" -> cs |> validate_required([:event_id])
      "group" -> cs |> validate_required([:subevent_id, :group_id])
      "user" -> cs |> validate_required([:user_id])
      _ -> cs
    end
    end).()
end
```

