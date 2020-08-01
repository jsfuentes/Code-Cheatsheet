# Deploying

### Vercel

Using Vercel makes it really easy since they made it and guides they wrote obv like to use it

- Pages that use Static Generation and assets (JS, CSS, images, fonts, etc) will automatically be served from the [Vercel Edge Network](https://vercel.com/smart-cdn), which is blazingly fast.
- Pages that use Server-Side Rendering and API routes will automatically become isolated [Serverless Functions](https://vercel.com/docs/v2/serverless-functions/introduction). This allows page rendering and API requests to scale infinitely.

### Other Hosting

```bash
yarn build #builds prod app in .next folder
yarn start #after building this starts the node.js server
```

