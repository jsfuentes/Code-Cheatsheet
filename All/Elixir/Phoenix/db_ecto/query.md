# Query With Repo

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
query = from u in User, select: %{u.id => u.email}, where: not is_nil(u.birthday) 

#Complex child query stuff idk
child_query = from c in Comment, where: parent_as(:posts).id == c.post_id
query = from p in Post, as: :posts, join: c in subquery(child_query)

Repo.all(query)
Repo.one(query) #will error if >1 response
```

Alt syntax

```elixir
query = "users"
|> where([u], u.age > 18)
|> select([u], u.name)
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
  # order_by: e.start_time would be asc
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

## Aggregate

```
from cm in ChatMessages,
group_by: [cm.to],
select: %{}
```



```elixir
anon_activity =
  from ea in EventAnalytics,
    where: ea.event_id == ^event_id and not is_nil(ea.email),
    where:
      ea.type == "RSVP" or ea.type == "IMPORT" or ea.type == "PREADMIT" or ea.type == "BLOCK",
    group_by: [ea.email],
    select: %{
      email: ea.email,
      name: max(ea.name),
      rsvp: type_count(ea.user_id, ea.type == "RSVP"),
      impt: type_count(ea.user_id, ea.type == "IMPORT"),
      preadmit: type_count(ea.user_id, ea.type == "PREADMIT"),
      block: type_count(ea.user_id, ea.type == "BLOCK"),
      inserted_at: min(ea.inserted_at),
      location: min(ea.location),
      timezone: max(ea.timezone)
    }

user_activity =
  from ea in EventAnalytics,
    where: ea.event_id == ^event_id and not is_nil(ea.email),
    where: ea.type == "JOIN",
    join: u in User,
    on: u.id == ea.user_id,
    group_by: [u.email],
    select: %{
      email: u.email,
      name: max(u.name),
      picture: max(u.picture),
      join: type_count(ea.user_id, ea.type == "JOIN"),
      inserted_at: min(ea.inserted_at),
      location: max(ea.location),
      timezone: max(ea.timezone),
      social_links: max(u.social_links)
    }

query =
  from ua in subquery(user_activity),
    full_join: aa in subquery(anon_activity),
    on: ua.email == aa.email,
    order_by: [asc: ua.join, desc: coalesce(aa.inserted_at, ua.inserted_at)],
    select: %{
      email: coalesce(ua.email, aa.email),
      name: coalesce(ua.name, aa.name),
      social_links: ua.social_links,
      RSVP: aa.rsvp,
      IMPORT: aa.impt,
      PREADMIT: aa.preadmit,
      BLOCK: aa.block,
      JOIN: ua.join,
      location: coalesce(ua.location, aa.location),
      timezone: coalesce(ua.timezone, aa.timezone)
    }

event_users = Repo.all(query)
```



