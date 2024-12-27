# Jotai

- Simple global use and setState that optimizes by usage of use and setState
- a `jotai/utils` bundle includs functions for persisting in localStorage, hydrating during SSR, and Redux-like reducers and actions

Create atoms

```js
const countryAtom = atom('Japan')

const citiesAtom = atom(['Tokyo', 'Kyoto', 'Osaka'])
```

```ts
const progressAtom = atom((get) => {
  const anime = get(animeAtom)
  return anime.filter((item) => item.watched).length / anime.length
})
```

Use atoms

```ts
import { useAtom } from 'jotai'

const AnimeApp = () => {
  const [anime, setAnime] = useAtom(animeAtom)
```

```ts
const ProgressTracker = () => {
  const progress = useAtomValue(progressAtom)
```

```ts
const AddAnime = () => {
  const setAnime = useSetAtom(animeAtom)
```

