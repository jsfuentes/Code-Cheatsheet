# [Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)

### SWR

The team behind Next.js has created a React hook for data fetching called [**SWR**](https://swr.now.sh/). We highly recommend it if you’re fetching data on the client side. It handles caching, revalidation, focus tracking, refetching on interval, and more. We won’t cover the details here, but here’s an example usage:

```jsx
import useSWR from 'swr'

function Profile() {
  const { data, error } = useSWR('/api/user', fetch)

  if (error) return <div>failed to load</div>
  if (!data) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

