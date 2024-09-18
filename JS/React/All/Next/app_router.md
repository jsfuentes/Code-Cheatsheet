# App Router

Next.js 13.4, released on May 4, 2023, marked the App Router as stable and ready for production use. v14 added Server Actions

## Updating versions

- Routing
  - `/pages` => `/app`
  - [..slug].ts => [...slug]/page.ts
- Client-side rendering ⇒ Server Components by default, need `use client` to change
- Layouts in `_app.ts` => `layout.ts` an allows nested layouts(just include in folder)  
- `getStaticProps`, `getServerSideProps`, `getInitialProps` ⇒ Async server components can just call fetch
- Custom pages like `404.js`, `500.js` ⇒ `error.js` and `global-error.js` for route segments and global errors
- need to update image tags, not much benefit
- metadata tags=> export metadata