# Comparisons

## Monorepo vs Manyrepo

Mono is better for atomic changes and is the more popular choice

Many seperates the pull requests and commit history of mostly seperate projects

## Server-Side Vs Client-Side Rendering

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

## Server Vs Clientside ID Generation

Server-side/Autoincrementing ID

- Need to access DB before you can propogate ID
- Less space - int8 is 8 bytes
- Simple and auto for dbs
- Leaks usage stats to people looking at ids number

**Client-side/Nanoid**

- Allows storing/using ids before saving in the DB
- Allows you to put id in urls without them being guessable by users 
- Should add prefix to ids like stripe b/c easier for debugging and more
- Globally unique unless theres a bad/malicious actor
  - Have to enforce uniqueness in the DB/catch id conflict errors
- More space - varchar(255) is up to 255 bytes and one byte per char so nanoid is 21 chars/bytes