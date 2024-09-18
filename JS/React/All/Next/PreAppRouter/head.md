# Head

- Last Head to be rendered wins if there is a key

```react
import Head from "next/head";

function App() {

return (<>
<Head>
  <title>{conf.get("PROJECT_NAME")}</title>
  <meta
    name="description"
    content="Learn & earn to solidify your financial future"
  />
  <meta
    name="viewport"
    content="width=device-width, initial-scale=1"
  />
  <link rel="icon" href="/favicon.ico" />
</Head>
  </>);
  }
```

Script

```jsx
import Script from 'next/script'

export default function Dashboard() {
  return (
    <>
      <Script src="https://example.com/script.js" />
    </>
  )
}
```