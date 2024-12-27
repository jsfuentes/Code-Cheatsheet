# [Pages](https://nextjs.org/docs/pages/building-your-application/routing/pages-and-layouts)

Pages are associated with a route based on their **file name**. For example, in development:

- `pages/index.js` is associated with the `/` route.
- `pages/posts/first-post.js` is associated with the `/posts/first-post` route.
- `pages/event/[id].js` for dynamic routes(see below)
- `pages/404.js` for custom 404 and [other errors]([Error Pages](https://nextjs.org/docs/advanced-features/custom-error-page#404-page))

### [Link](https://nextjs.org/docs/api-reference/next/link)

```jsx
import Link from 'next/link'; //must have a tag inside

export default function FirstPost() {
  return (
    <>
      <h1>First Post</h1>
      <h2>
        <Link
          href={{
            pathname: '/about',
            query: { name: 'test' },
          }}
        >
          About us
        </Link>
        <Link href={`/blog/${encodeURIComponent(post.slug)}`}>
           {post.title}
        </Link>
        <Link
          href={{
            pathname: '/about',
            query: { name: 'test' },
          }}
        >
          About us
        </Link>
      </h2>
    </>
  )
}
```

**Yes that is all you need no imports, it somehow auto imports React and such**

Next.js automatically **prefetches** the code for the linked page in the background.

#### Outer Component

Next.js specific top-level  `App` component 

Can keep state when navigating between pages, add global styles, etc

/pages/_app.js

```jsx
import "../styles/global.css";

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

*Must restart dev server after adding _app.js*

#### Layouts

Use regular react components

### [Head](https://nextjs.org/docs/api-reference/next/head)

```jsx
import Head from "next/head";

export default function Home() {
  return (
    <div className="container">
      <Head>
        <title>Create Next App</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>
    </div>)
}
```

### [Page Path Depends on External Data](https://nextjs.org/docs/routing/dynamic-routes)

Routes like `/post/[id]`

1. Create a  [] in the filename to indicate dynamic pages in Next.js
2. Create file with[ `getStaticPaths` ](https://nextjs.org/docs/basic-features/data-fetching#fallback-pages )and `getStaticProps`

pages/posts/[id].js

```jsx
import Layout from '../../components/layout'

export default function Post() {
  return <Layout>...</Layout>
}

//prod build time, dev every request
export async function getStaticPaths() {
  // Returns an array that looks like this:
  // [
  //   {
  //     params: {
  //       id: 'ssg-ssr'
  //     }
  //   },
  //   {
  //     params: {
  //       id: 'pre-rendering'
  //     }
  //   }
  // ]
  //If fallback is false, then any paths not returned by getStaticPaths will result in a 404 page.
  return {paths, fallback: false};
}

export async function getStaticProps({ params }) {
  // Fetch necessary data for the blog post using params.id
}
```

### Linking

```jsx
<Link href="/posts/[id]" as="/posts/ssg-ssr">
  <a>...</a>
</Link>
```

### Catch-all Routes

`pages/posts/[...id].js` matches `/posts/a`, but also `/posts/a/b`, `/posts/a/b/c` and so on.

```jsx
function getStaticPaths() {
  //..
  return [
    {
      params: {
        // Statically Generates /posts/a/b/c
        id: ['a', 'b', 'c']
      }
    }
    //...
  ]
}

export async function getStaticProps({ params }) {
  // params.id will be like ['a', 'b', 'c']
}
```

## Router

If you want to access the Next.js router, you can do so by importing the `useRouter` hook from `next/router`. Take a look at our [router documentation](https://nextjs.org/docs/routing/dynamic-routes) to learn more.

## Redirecting Link permantely

In `next.config.js`

```js
module.exports = {
  async redirects() {
    return [
      {
        source: '/about',
        destination: '/',
        permanent: true,
      },
    ]
  },
}
```

### Redirecting in JS

```jsx
import { useRouter } from 'next/router'

function ActiveLink({ children, href }) {
  const router = useRouter()
  
  const handleClick = (e) => {
    e.preventDefault()
    router.push(href)
    router.push('/post/[pid]', '/post/abc')
  }

  return (
    <a href={href} onClick={handleClick} >
      {children}
    </a>
  )
}

export default ActiveLink
```



