# SSR

Can make hybrid

- **Static Generation** is the pre-rendering method that generates the HTML at **build time**. The pre-rendered HTML is then *reused* on each request.
  - Whenever possible if not based on request because CDN

```bash
next build
```

- **Server-side Rendering** is the pre-rendering method that generates the HTML on **each request**.
  - frequently update data that changes on user request
- Can even just normal **clientside render**

## Static Generation

#### Static Generation With Data

Can't render page until you fetch external data(DB, api, file system)

Export async ft called [`getStaticProps`](https://nextjs.org/docs/basic-features/data-fetching) that will run **at build time server-side in prod** and **every request in dev** to pass as props

```jsx
export default function Home(props) { ... }

export async function getStaticProps() {
  // Get external data from the file system, API, DB, etc.
  const data = ...

  // The value of the `props` key will be
  //  passed to the `Home` component
  return {
    props: { data },
    revalidate: 60, // Optional: Changes to incremental static regeneration(after build) where it will background(stale data will be shown) regenerate on request at most every 60 seconds
  }
}
```

If you have *dynamic routes*([...slug].ts), then you need to `getStaticPaths` so it knows what to pregenerate

```ts
export const getStaticPaths = (async () => {
  return {
    paths: [
      {
        params: {
          name: 'next.js',
        },
      }, // See the "paths" section below
    ],
    fallback: true, // false or "blocking"
  }
}) satisfies GetStaticPaths
```





## Server-side Rendering

To use Server-side Rendering, you need to export [`getServerSideProps`](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering) instead of `getStaticProps` from your page.

Called at **request time** and context contains request specific parameters

```jsx
export async function getServerSideProps(context) {
const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page via props
  return { props: { data } }
}
```

## Clientside

### ReferenceError: window is not defined

If you configure Next.js to run in a SSR configuration and you’re using `window` in your code—or one of your packages does—then you’ll have to make Next aware that this package needs to be `dynamic`. The reason this error pops up is this: when html is rendered on the server (remember, SSR stands for server-side rendering), there’s no instance of `window`, because, well, there’s simply none. `window` is only accessible on the client-side.

I ran into this with a package called `react-json-view`. I use it to render beautiful json in html. Here’s how to make it work:

```
import dynamic from 'next/dynamic'
const DynamicReactJson = dynamic(import('react-json-view'), { ssr: false })
```

Now, simply proceed to use that import as you’ve done before.