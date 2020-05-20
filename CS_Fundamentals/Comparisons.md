## Monorepo vs Manyrepo

Mono is better for atomic changes and is the more popular choice

Many seperates the pull requests and commit history of mostly seperate projects

## Yarn vs NPM

NPM:

- New version of npm has lock-packages
- Included with node
- Doesn't go through Facebook's mirror(privacy???)

Yarn:

- Use deterministic installation, better caches/faster
- Uses package.json, so super super easy to switch; can use both at once
- Emojis 

### Server-Side Vs Client-Side Rendering

ServerSide Rendering means the server will generate the initial html of the React element that can then be rehydrated. Default lib in node.

Server-Side

- Faster initial load(Less roundtrips)
- No access to Window, History APIS
- Supposedly SEO
  - According to [this](https://medium.com/@benjburkholder/javascript-seo-server-side-rendering-vs-client-side-rendering-bc06b8ca2383), Google will take longer(hours to weeks) to index server rendered websites
  - According to a head of SEO from Airbnb, Google is stupid and cant render js
- Not all the React related libraries will be compatible with SSR, and even if they are, it might require some non-obvious setup to get them working.

Client-Side

- Easier/Standard
- Better for Apps that are mostly behind a login because it doesnt need SEO right