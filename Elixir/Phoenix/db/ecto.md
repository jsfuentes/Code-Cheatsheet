# Ecto

Data validation and db support for postgreSQL, mySQL, MSSQL

Natural Elixir DSL/query engine to query abs

Need to setup credentials in `config/dev.exs`

### Schema (Structs)

Default id of type integer and timestamps() creates inserted/updated at field. 

```elixir
defmodule User do
  use Ecto.Schema
  @derive {Jason.Encoder, only: [:name, :age, :company_id]} #for sending %User through HTTP requests

  schema "users" do #users is table name
    field :name, :string
    field :age, :integer, default: 0
    field :links, {:array, :string}
    has_many :posts, Post
    belongs_to :company, MyApp.Company
  end
end

defmodule Comment do
  use Ecto.Schema
  schema "comments" do
    field :content, :string
    field :parent_id, :integer
    belongs_to :parent, Comment, foreign_key: :id, references: :parent_id, define_field: false
    has_many :children, Comment, foreign_key: :parent_id, references: :id
  end
end
```

```elixir
user = %User{name: "jane"}
```

Finally, schemas can also have virtual fields by passing the `virtual: true` option.

### Example

Simple User

```elixir
defmodule Discuss.Accounts.User do
  use Ecto.Schema
  import Ecto.Changeset

  schema "users" do
    field :name, :string
    field :username, :string
    has_one :credential, Discuss.Accounts.Credential

    timestamps()
  end

  @doc false
  def changeset(user, attrs) do
    user
    |> cast(attrs, [:name, :username]) #requires both
    |> validate_required([:name, :username])
    |> unique_constraint(:username)
  end
end
```

Password Hash Example

```elixir
defmodule Discuss.Accounts.Credential do
  use Ecto.Schema
  import Ecto.Changeset
  alias Comeonin.Argon2

  schema "credentials" do
    field :email, :string
    field :password_hash, :string
    field :password, :string, virtual: true #Dont get saved
    field :password_confirmation, :string, virtual: true
    belongs_to :user, Discuss.Accounts.User

    timestamps()
  end

  @doc false
  def changeset(credential, attrs) do
    credential
    |> cast(attrs, [:email])
    |> validate_required([:email])
    |> validate_format(:email, ~r/@/ )
    |> unique_constraint(:email)
  end

  #if validation fails, will still pass to next changeset with valid: false
  def registration_changeset(struct, attrs \\ %{}) do
    struct 
    |> changeset(attrs)
    |> cast(attrs, [:password, :password_confirmation]) #cast is just the attrs you pay attention(throws away rest)
    |> validate_required([:password, :password_confirmation])
    |> validate_length(:password, min: 8)
    |> validate_confirmation(:password) #compares password and password_confirmation are equal, other arg assumed by f
    |> hash_password()
  end

  def hash_password(%{valid?: false} = changeset), do: changeset
  def hash_password(%{valid?: true, changes: %{password: pass}} = changeset) do 
    put_change(changeset, :password_hash, Argon2.hashpwsalt(pass))
  end
end

```

User Context with this Schema

```elixir
defmodule Discuss.Accounts do
  @moduledoc """
  The Accounts context.
  """

  import Ecto.Query, warn: false
  import Comeonin.Argon2, only: [checkpw: 2, dummy_checkpw: 0]
  alias Discuss.Repo

  alias Discuss.Accounts.{Credential, User}

  def list_users do
    Repo.all(User)
  end
  
  def get_user!(id) do
    Repo.get!(User, id)
    |> Repo.preload(:credential)
  end

  def create_user(attrs \\ %{}) do
    %User{}
    |> User.changeset(attrs)
    |> Ecto.Changeset.cast_assoc(:credential, with: &Credential.registration_changeset/2)
    |> Repo.insert()
  end

  def update_user(%User{} = user, attrs) do
    # Only way to update user now, for some reasons won't highlight in Typora correclty so commented out
    #cred_changeset = 
      #if attrs["credential"] ["password"] == "" do
        &Credential.changeset/2
      else
        &Credential.registration_changeset/2
      end

    user
    |> User.changeset(attrs)
    |> Ecto.Changeset.cast_assoc(:credential, with: cred_changeset)
    |> Repo.update()
  end

  def delete_user(%User{} = user) do
    Repo.delete(user)
  end

  def change_user(%User{} = user) do
    User.changeset(user, %{})
  end

  alias Discuss.Accounts.Credential

  def list_credentials do
    Repo.all(Credential)
  end

  def get_credential!(id), do: Repo.get!(Credential, id)

  def create_credential(attrs \\ %{}) do
    %Credential{}
    |> Credential.changeset(attrs)
    |> Repo.insert()
  end

  def update_credential(%Credential{} = credential, attrs) do
    credential
    |> Credential.changeset(attrs)
    |> Repo.update()
  end

  def delete_credential(%Credential{} = credential) do
    Repo.delete(credential)
  end

  def change_credential(%Credential{} = credential) do
    Credential.changeset(credential, %{})
  end
end
```

### Extra

lib/hello/repo.ex

```elixir
defmodule Hello.Repo do
  use Ecto.Repo, #import query functions
    otp_app: :hello, #set app name
    adapter: Ecto.Adapters.Postgres #setup adapter
end
```

Changeset

```elixir
changeset = User.changeset(%User{}, %{})
#Ecto.Changeset<action: nil, changes: %{}, errors: [name: {"can't be blank", [validation: :required]}, email: {"can't be blank", [validation: :required]}, bio: {"can't be blank", [validation: :required]},
 data: #Hello.User<>, valid?: false>
changeset.valid? # false
```

