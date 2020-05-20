# Spotify

https://developer.spotify.com/dashboard/applications

Does not allow you to get friend info, must give ids and then you can see if they follow those specific ids. 

Builtin API to get the top songs for the user

```elixir
        types = ["artists", "tracks"]
        ranges = ["short_term", "medium_term", "long_term"]

        all_results =
          Enum.map(types, fn type ->
            range_results =
              Enum.map(ranges, fn range ->
                url =
                  "https://api.spotify.com/v1/me/top/#{type}?time_range=#{range}&limit=#{limit}"

                %HTTPoison.Response{status_code: 200, body: rawBody} =
                  HTTPoison.get!(url, headers)

                body = Jason.decode!(rawBody)
                {range, body["items"]}
              end)
              |> Map.new()

            {type, range_results}
          end)
          |> Map.new()
          |> IO.inspect()

        json(conn, all_results)
```

## Elixir

https://github.com/jsncmgs1/spotify_ex

