# mapbox

### mapcreation
* Container is the id of the div in the code to put the map in
* All coords are [long, lat]

```ts
this.map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/trinakat/cjasrg0ui87hc2rmsomilefe3', // UCLA Campus Buildings (restricted by the border)
  // 'mapbox://styles/trinakat/cjashcgwq7rfo2srstatrxhyi', // UCLA Buildings
  // 'mapbox://styles/helarabawy/cj9tlpsgj339a2sojau0uv1f4',
  center: [this.lng, this.lat],
  maxBounds: [[-118.46, 34.056],[-118.428, 34.079]],
  zoom: 15,
  pitch: 60
});
```

### Events

`map.loaded()` return boolean is loaded
```ts
  on(type, listener)
  off(type, listener)
  once(type, listener)
  fire(type, data?)
  listens(type)
```


### Obscure Bug
Are you getting NO MAP GL JS found, but copied the link exactly like they had it. Well then, here is the real link from the example.

```ts
<link href='https://api.tiles.mapbox.com/mapbox-gl-js/v0.44.1/mapbox-gl.css' rel='stylesheet' />
```
