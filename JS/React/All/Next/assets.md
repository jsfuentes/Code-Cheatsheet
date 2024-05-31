# [Assets](https://nextjs.org/docs/basic-features/static-file-serving)

Next.js can serve static files, like images, under **the top-level `public` directory**. Files inside `public` can be referenced from the root of the application similar to `pages`.

/public/vercel.svg 

```jsx
<img src="/vercel.svg" alt="Vercel Logo" className="logo" />
```

## [Next/Image](https://nextjs.org/docs/api-reference/next/image)

This `next/image` component uses browser native [lazy loading](https://caniuse.com/loading-lazy-attr), w

Src must be [statically imported](https://nextjs.org/docs/basic-features/image-optimization#local-images) o absolute external URL, or an internal [loader](https://nextjs.org/docs/api-reference/next/image#loader) prop.

*When using an external URL, you must add it to [remotePatterns](https://nextjs.org/docs/api-reference/next/image#remote-patterns) in `next.config.js`.*

```react
import Image from 'next/image'
import profilePic from '../public/me.png'

const Example = () => (
  <div className="grid-element">
    <Image
      src={profilePic}
      alt="Picture of the author"
      width={500}
      height={500}
    />
    <Image
      src="/example.png"
      alt="Picture of the author"
      fill
      sizes="(max-width: 768px) 100vw,
              (max-width: 1200px) 50vw,
              33vw"
    />
  </div>
)
```

Custom Loader

```react
const myLoader = ({ src, width, quality }) => {
  return `https://example.com/${src}?w=${width}&q=${quality || 75}`
}

const MyImage = (props) => {
  return (
    <Image
      loader={myLoader}
      src="me.png"
      alt="Picture of the author"
      width={500}
      height={500}
    />
  )
}
```

