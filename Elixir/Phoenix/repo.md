# Repo

Controller interactions will use changesets and Repo should be from a public context like Accounts

```elixir
alias Hello.{Repo, User}
Repo.insert(%User{email: "user1@example.com"}) 
#{:ok, [new User object...]}
```

[Query](https://hexdocs.pm/ecto/Ecto.Query.html#content)

```elixir
Repo.all(User) #[User1..., User2...]
Repo.all(from u in User, select: u.email)
Repo.one(from u in User, where: ilike(u.email, "%1%"), select: count(u.id))  # # of users with 1 in their email
Repo.all(from u in User, select: %{u.id => u.email}) #List of map from id to email
```

```elixir
MyRepo.get_by(Post, title: "My post") #get
MyRepo.get(Post, 14238905128) #get by id
```

### 