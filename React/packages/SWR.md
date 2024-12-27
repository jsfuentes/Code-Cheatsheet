# [SWR](https://swr.vercel.app/)

### SWR

- **Fast**, **lightweight** and **reusable** data fetching
- Built-in **cache** and request deduplication
- **Real-time** experience
- Transport and protocol agnostic
- SSR / ISR / SSG support
- TypeScript ready
- React Native

```jsx
import useSWR from 'swr'

function Profile() {
  const { data, error } = useSWR('/api/user', fetch)

  if (error) return <div>failed to load</div>
  if (!data) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

