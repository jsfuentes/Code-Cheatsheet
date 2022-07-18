# Next

- Adds **Page-based** routing system
- Pre-rendering, static generation (SSG) and **server-side rendering** (SSR) supported on a per-page basis
- Automatic **code splitting** for faster page loads
- Client-side routing with optimized prefetching
- Built-in CSS and Sass support, and support for any CSS-in-JS library
- Development environment which supports Hot Module Replacement
- API routes to build API endpoints with Serverless Functions
- Fully extendable

- Has an electron specific repo

Seems awesome, basically adds some efficiency to React and easy page adding without being as heavyweight as Gatsby 

## Unlike Gatsby

Usually uses a server, can configure to be static site get

Seems to be used by more companies

Can become completely clientside rendered

**Less opinotated** 

Gatsby dictates how you handle data(GraphQL)

Let’s say you wanted to use client-side rendering for a route like `/products/yellow-dress-1`. With NextJS, this isn’t possible. Instead, you would need to use query parameters like this `/product?productId=yellow-dress-1`.

## Pre-rendering

Next pre-renders every page, generate HTML in advance