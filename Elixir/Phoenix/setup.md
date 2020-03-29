#Setup

Supervisor is special process that monitors other process

Three main plugs

- Endpoint
- Router
  - scope and http verbs, module controller, function inside that module

#### Installation

Maybe dif version?

```bash
mix archive.install hex phx_new 1.4.16
```

#### Boilerplate

```bash
mix phx.new hello
```

Flags: 

- `--no-ecto` to not have database stuff

Follow steps it prompts you with, then start with:

```bash
mix phx.server 
iex -S mix phx.server #interactive run, `recompile()`
```

*Phoenix uses webpack for asset management and needs npm*

Main work will be in lib

