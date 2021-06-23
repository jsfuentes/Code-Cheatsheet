# [Relations](https://hexdocs.pm/ecto/Ecto.Changeset.html#module-associations-embeds-and-on-replace)

- Has_many
- Belongs_to

### Usage

- [`cast_assoc`](https://hexdocs.pm/ecto/Ecto.Changeset.html#cast_assoc/3)

This function should be used when working with the entire association at once (and not a single element of a many-style association) and receiving data external to the application.

It compares each of param to preloaded

- No id or id not in db => insert
- if id and in db => update
- If no id, but id in db => delete/on_replace

In changes

```elixir
def changeset(subevent, attrs) do
  subevent
    |> cast(attrs, [
    :event_id,
    :start_time
    ])
    |> cast_assoc(:subevent_breakout_groups,
    with: &ReactPhoenix.Subevents.SubeventBreakoutGroup.changeset/2
    )
    |> validate_required([:title, :type, :start_time, :end_time])
end
```

In Repo

```elixir
event
|> Event.changeset(attrs)
|> Ecto.Changeset.cast_assoc(:subevents, with: &Subevent.changeset/2)
|> Ecto.Changeset.cast_assoc(:registration_event_questions,
with: &RegistrationEventQuestion.changeset/2
)
|> Repo.update()
```



## Example Schema

```elixir
  schema "subevents" do
    field :title, :string
    # text 
    field :description, :string
    field :type, :string
    field :type_data, :map
    field :link, :string
    field :start_time, :utc_datetime
    field :end_time, :utc_datetime
    belongs_to :event, ReactPhoenix.Events.Event, type: :string
    has_many :calls, ReactPhoenix.Calls.Call, on_replace: :delete

    has_many :subevent_breakout_groups, ReactPhoenix.Subevents.SubeventBreakoutGroup,
      on_replace: :delete

    timestamps()
  end
```

