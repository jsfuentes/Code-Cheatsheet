# [Image](https://nextjs.org/docs/pages/api-reference/components/image)

Why use over `<img>`?

- Images are lazy loaded meaning not loaded if outside viewpoint/unless scrolled to
-  **nextjs** will automatically create optimized images in WebP  for all device heights and widths, including a jpg fallback for older browsers
- Require image ratio to prevent [Cumulative Layout Shift](https://nextjs.org/learn/seo/web-performance/cls),

### Usage

- Needs image ratio(width/height) to prevent [Cumulative Layout Shift](https://nextjs.org/learn/seo/web-performance/cls),
  - If imported, Next.js will [automatically determine](https://nextjs.org/docs/pages/building-your-application/optimizing/images#image-sizing) it
  - If remote, need to set *intrisic* width and height not style width and height thats different (or use fill if unknown)
    - Need to explicitly allow remote image hosts in `next.config.js` to safely optimize
    - Can use fill, but parent element must have `position: relative` and  `display:block`

```ts
import Image from 'next/image'
import profilePic from '../public/me.png'

function Page() {
  return (
    <Image
      src={profilePic}
      alt="Picture of the author"
      // width={500} automatically provided
      // height={500} automatically provided
      // blurDataURL="data:..." automatically provided
      // placeholder="blur" // Optional blur-up while loading
    />
  )
}

function Fill() {
  return (
      <div style={{ position: 'relative', height: '400px' }}>
        <Image
          alt="Mountains"
          src={mountains}
          fill
          sizes="(min-width: 808px) 50vw, 100vw"
          style={{
            objectFit: 'cover', // cover, contain, none
          }}
        />
      </div>
  )
}
```

- 

next.config.js

```ts
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 's3.amazonaws.com',
        port: '',
        pathname: '/my-bucket/**',
      },
    ],
  },
}
```

