# [Api Routes](https://nextjs.org/docs/api-routes/dynamic-api-routes)

Simple API routes inside Next.js app like for form input 

Just create a **function** inside the `pages/api` directory that has the following format:

/pages/api/hello.js

```js
// req = request data, res = response data
export default (req, res) => {
  res.status(200).json({ text: 'Hello' })
}
```

http://localhost:3000/api/hello

They can be deployed as Serverless Functions (also known as Lambdas).

- `req` is an instance of [http.IncomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage), plus some pre-built middlewares you can see [here](https://nextjs.org/docs/api-routes/api-middlewares).
- `res` is an instance of [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse), plus some helper functions you can see [here](https://nextjs.org/docs/api-routes/response-helpers).

**Do Not Fetch an API Route from `getStaticProps` or `getStaticPaths`**, instead just run the code in them since it runs serverside anyway

[Dynamic Api Routes](https://nextjs.org/docs/api-routes/dynamic-api-routes)