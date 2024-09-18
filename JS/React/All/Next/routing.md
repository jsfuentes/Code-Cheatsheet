# App Router

Recommended instead of pages approach in v13

In `/app`:

- **Folders** are used to define routes
  - [][`page.js` file](https://nextjs.org/docs/app/building-your-application/routing/pages) in that folder makes route segments accessible
  - Can colocate components, stylesheets, and images
  - [layouts](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#layouts) in `layout.ts` show UI that is shared across multiple routes. If multiple layouts apply, they do nested wrapping
  - `app/blog/[slug]/page.tsx` for dynamic slug
  - `app/blog/[...slug]/page.tsx` for catch all slug ie `/blog/a/b` and slug is list
- A route group(folder that doesn't affect path) can be created by wrapping a folder's name in parenthesis: `(folderName)`

app/page.tsx

```tsx
export default function Page() {
  return <h1>Hello, Home page!</h1>
}
```

app/blog/[slug]/page.tsx

```tsx
export default function Page({ params }: { params: { slug: string } }) {
  return <div>My Post: {params.slug}</div>
}

//optional, prerender the dynamic routes 
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json())
 
  return posts.map((post) => ({
    slug: post.slug,
  }))
}
```

### Linking

Link component recommended and provides prefetching

```tsx
import Link from 'next/link'
 
export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>
}
```

Programmatically

```tsx
'use client'
 
import { useRouter } from 'next/navigation'
 
export default function Page() {
  const router = useRouter()
 
  return (
    <button type="button" onClick={() => router.push('/dashboard')}>
      Dashboard
    </button>
  )
}
```

Server components programmatically

```tsx
import { redirect } from 'next/navigation'
 
async function fetchTeam(id: string) {
  const res = await fetch('https://...')
  if (!res.ok) return undefined
  return res.json()
}
 
export default async function Profile({ params }: { params: { id: string } }) {
  const team = await fetchTeam(params.id)
  if (!team) {
    redirect('/login')
  }
 
  // ...
}
```



