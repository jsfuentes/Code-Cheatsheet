# [Route Handlers]()

Route Handlers can be nested anywhere inside the `app` directory, with similar `[slug]/` for dynamic routes. But must only be   `route.js` or `page.js` at each level.

Next.js browser Web [Request](https://developer.mozilla.org/docs/Web/API/Request) and [Response](https://developer.mozilla.org/docs/Web/API/Response) APIs with [`NextRequest`](https://nextjs.org/docs/app/api-reference/functions/next-request) and [`NextResponse`](https://nextjs.org/docs/app/api-reference/functions/next-response) 

app/api/route.ts

```ts
export const dynamic = 'force-static' //cache get
 
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
  })
  const data = await res.json()
 
  return Response.json({ data })
}
```

### Dynamic

```tsx
import { type NextRequest } from 'next/server'

export function GET(
  request: NextRequest,
  { params }: { params: { slug: string } }
) {
  const searchParams = request.nextUrl.searchParams
  const query = searchParams.get('query')
  
  const slug = params.slug // 'a', 'b', or 'c'
}
```

## Advanced

- Can [stream](https://nextjs.org/docs/app/building-your-application/routing/route-handlers#streaming)
- [Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware)
  - intercept routes for logging or auth

### Cookies/Headers

```ts
import { cookies } from 'next/headers'
import { headers } from 'next/headers'

export async function GET(request: Request) {
  const cookieStore = cookies()
  const token = cookieStore.get('token')
  
  const headersList = headers()
  const referer = headersList.get('referer')
 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { 'Set-Cookie': `token=${token.value}` },
  })
}
```

## 