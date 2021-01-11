# [Phoenix.Token](https://hexdocs.pm/phoenix/Phoenix.Token.html)

Phoenix built-in generate and verify signed tokens(not encrypted, so can verify data was signed not hide data)

```elixir
user_id = 1
token = Phoenix.Token.sign(MyApp.Endpoint, "user auth", user_id)
Phoenix.Token.verify(MyApp.Endpoint, "user auth", token, max_age: 86400) #{:ok, 1}
```

Arg 1: Uses the secret key base configured in the endpoint

Arg 2: [cryptographic salt](https://en.wikipedia.org/wiki/Salt_(cryptography)), kinda like a namespace

^Must be same in sign and verify

Arg 3: What to codify in the string

## Extra

Also has `encrypt` and `decrypt`

