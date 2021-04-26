# ExRated

```elixir
      {:ex_rated, "~> 2.0"},

```

## Usage

Can have as many buckets as you want

```elixir
#bucket_name, bucket time existence, limit in time existence
ExRated.check_rate("my-rate-limited-api", 10_000, 5)
# either {:ok, 1}
# or {:error, 5}
```



## Plug Ratelimiter

https://blog.danielberkompas.com/2015/06/16/rate-limiting-a-phoenix-api/

```elixir
defmodule MyApp.RateLimit do
  import Phoenix.Controller, only: [json: 2]
  import Plug.Conn, only: [put_status: 2]

  def rate_limit(conn, options \\ []) do
    case check_rate(conn, options) do
      {:ok, _count}   -> conn # Do nothing, allow execution to continue
      {:fail, _count} -> render_error(conn)
    end
  end

  defp check_rate(conn, options) do
    interval_milliseconds = options[:interval_seconds] * 1000
    max_requests = options[:max_requests]
    ExRated.check_rate(bucket_name(conn), interval_milliseconds, max_requests)
  end

  # Bucket name should be a combination of ip address and request path, like so:
  #
  # "127.0.0.1:/api/v1/authorizations"
  defp bucket_name(conn) do
    path = Enum.join(conn.path_info, "/")
    ip   = conn.remote_ip |> Tuple.to_list |> Enum.join(".")
    "#{ip}:#{path}"
  end

  defp render_error(conn) do
    conn
    |> put_status(:forbidden)
    |> json(%{error: "Rate limit exceeded."})
    |> halt # Stop execution of further plugs, return response now
  end
end
```

```elixir
plug :rate_limit, max_requests: 5, interval_seconds: 60 when action in [:create]
```

