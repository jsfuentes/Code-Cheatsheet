# [Bun](https://bun.sh/)

- not full node compatibility, still buggy especially test runner, not production ready

### benefits

- dropin node replacement that works with package.json
- Benefits over Node
  - `bun run` watches and restarts automatically
  - typescript and jsx first class so runnable/transpiled in bun and respects tsconfig
  - Built-in package manager, test runner, bundler, and api for server

- Bun and Node.js are both JavaScript runtimes, but they have some key differences:
  - Node.js is primarily written in C++, while Bun is written in Zig

### starting server builtin

```ts
const server = Bun.serve({
  port: 3000,
  fetch(request) {
    return new Response("Welcome to Bun!");
  },
});

console.log(`Listening on localhost:${server.port}`);
```

