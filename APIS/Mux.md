# Mux

Throw video at an endpoint and get a url that will allow a great viewing experience

1) Get API Token and Secret

2) Send file to Mux

```
curl https://api.mux.com/video/v1/assets \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{ "input": "http://movietrailers.apple.com/movies/wb/the-lego-ninjago-movie/the-lego-ninjago-movie-trailer-2_h720p.mov", "playback_policy": "public" }' \
  -u cb3d37fc-1583-4883-94b4-b04577044c54:9aLDt17JBT7pKeeLIE2ox5rkJt0IjfXsNCP/GD+0RMTU+PKlPZD7aCuFJ4DYOgvzBVQ7mCqhkPD | json_pp
```

Response

```
{
   "data" : {
   		//asset id
      "id" : "ymDhKE00YZ12XxJLFo76DIVqCzL15bVf2", 
      "created_at" : "1517531451",
      "playback_ids" : [
         {
            "id" : "EsxKJmzkfLvGV01cbThYHDcEz7TKcbR31",
            "policy" : "public"
         }
      ],
      "status" : "preparing"
   }
}
```

3) Wait for ready with a webhook or polling with asset_id

```
curl -X GET https://api.mux.com/video/v1/assets/ymDhKE00YZ12XxJLFo76DIVqCzL15bVf2 \
  -u cb3d37fc-1583-4883-94b4-b04577044c54:9aLDt17JBT7pKeeLIE2ox5rkJt0IjfXsNCP/GD+0RMTU+PKlPZD7aCuFJ4DYOgvzBVQ7mCqhkPD | json_pp
```

4) Use the playback_id you got when creating the asset for the playback url

```
https://stream.mux.com/EsxKJmzkfLvGV01cbThYHDcEz7TKcbR31.m3u8
```

