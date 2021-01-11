# Geolix

With geolix you can do ip address to location mapping

## Setup

1) Get links to mmbd2 database [here](https://www.maxmind.com/en/geolite2/thank-you), you will have to make an account and generate a license link

2) Install deps

```elixir
      {:geolix, "~> 2.0"},
      {:geolix_adapter_mmdb2, "~> 0.6.0"},
```

3) Config

```elixir
config :geolix, databases: [
  %{
    id: :city,
    adapter: Geolix.Adapter.MMDB2,
    source: "https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-City&license_key=LICEN_SEKY&suffix=tar.gz"
  },
  %{
    id: :country,
    adapter: Geolix.Adapter.MMDB2,
    source: "https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-Country&license_key=LICEN_SEKY&suffix=tar.gz"
  }
]
```

## Usage

```elixir
Geolix.lookup("45.50.161.38")
```

