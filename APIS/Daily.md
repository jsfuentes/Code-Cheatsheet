# Daily

```elixir
  def createDailyRoom() do
    nowUTC = DateTime.utc_now() |> DateTime.to_unix()
    rawPayload = %{
      privacy: "public",
      # properties: %{exp: nowUTC + 24 * 60 * 60}
      properties: %{exp: nowUTC + 5 * 60}
    }
    payload = Jason.encode!(rawPayload)
    url = "https://api.daily.co/v1/rooms"
    headers = [
      Accept: "Application/json; Charset=utf-8",
      "Content-Type": "Application/json; charset=utf-8",
      Authorization: "Bearer #{Application.fetch_env!(:react_phoenix, :daily_api)}"
    ]
    HTTPoison.post(url, payload, headers)!
    end
  end
```

Returns

```
{
  api_created: true
  config: {}
  created_at: "2020-05-07T06:00:48.720Z"
  id: "35820122-d98a-4885-a711-787d12c44d72"
  name: "7eGnQbZoUsbz7Pt649Tr"
  privacy: "public"
  url: "https://molecule.daily.co/7eGnQbZoUsbz7Pt649Tr"
  __proto__: Object
}
```

