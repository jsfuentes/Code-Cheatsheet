# Trpc

Typesafe Remote Procedure Call, Better APIs

-  define a server-side router for your procedures, then export inferred type, then import type client side
- Type errors with your API contracts will be caught at build time
- Arguably server actions and ssc in Next.js solve most of these problems

## Usage

```ts
// HTTP/REST
const res = await fetch('/api/users/1');
const user = await res.json();
// RPC
const user = await api.users.getById({ id: 1 });
```

