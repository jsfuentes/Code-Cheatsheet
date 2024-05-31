# Next

- Since v13, [app router](https://nextjs.org/docs/app) using React's latest features such as [Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components), [Streaming with Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#streaming-with-suspense), and [Server Actions](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations).
- Allows pre-rendering, static generation (SSG) and **server-side rendering** (SSR) supported on a per-page basis
- Automatic **code splitting** for faster page loads
- Client-side routing with optimized prefetching
- Tailwind default
- Hot reloading development environment and error handling
- API routes to build API endpoints with Serverless Functions
- Has an electron specific repo

Seems awesome, basically adds some efficiency to React and easy page adding without being as heavyweight as Gatsby 

### How is it different than a SPA?

- Renders HTML per page, instead of one big one
  - So to avoid changing header/footer when you go across pages, need to use Layout
  - Next.js automatically prefetches the JavaScript for linked pages in the background so no load time
- [Technically possible/hacky](https://gist.github.com/gaearon/9d6b8eddc7f5e647a054d7b333434ef6) to make Next.js operate like a SPA with one index.html

## Unlike Gatsby

Usually uses a server, can configure to be static site get

Seems to be used by more companies

Can become completely clientside rendered

**Less opinonated** 

Gatsby dictates how you handle data(GraphQL)

Let’s say you wanted to use client-side rendering for a route like `/products/yellow-dress-1`. With NextJS, this isn’t possible. Instead, you would need to use query parameters like this `/product?productId=yellow-dress-1`.
