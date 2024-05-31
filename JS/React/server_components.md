# [Server Components](https://react.dev/reference/rsc/server-components)

Server Components for Working Devs

Two questions: Oh there's a new thing. Should I switch and why? And how is it different then existing SSR like Next.js get Static Props? And the meta question, should I just learn it now if its the future or is it experimental like other React stuff `useTransaction` or `useAction` that is more usecase specific/a curiosity?

Now that we know how it works? Are there problems with adoption rn? Will I run into weird errors? 

- Next.js update
  - need to update image tags, not much benefit
  - get static props rewritten as async
  - use client
  - instead of [..slug].ts its [...slug]/page.ts
  - **generateStaticParams** => [`generateStaticParams`](https://nextjs.org/docs/app/api-reference/functions/generate-static-params)
  - change metadata

## Real

Stable in v19

### Is this different than historical SSR like Next.js `getStaticProps`?

- It is a very similar with the same benefits
  - Historically SSR didn't make app interactive faster(maybe on really slow clients), but made loading state appear earlier
  - Simpler colocated api requests
  - auth can be done earlier, failed requests can handled/redirected sooner
  - seo benefits
- But different implementation with more React support that makes it more efficient,  **Selective Hydration**
  - Combining with [Suspense and the new Streaming SSR architecture](https://github.com/reactwg/react-18/discussions/37), note this stuff can be used seperately from Server Components but work well together:
    - ![Screenshot 2024-08-10 at 10.58.54 PM](/Users/jfuentes/Library/Containers/at.EternalStorms.Yoink/Data/Documents/YoinkPromisedFiles.noIndex/yoinkFilePromiseCreationFolder8FCEB93D-1E61-490C-9A0D-101305B141E6/add8FCEB93D-1E61-490C-9A0D-101305B141E6/Screenshot 2024-08-10 at 10.58.54 PM.png)
    - Basically historically it was full “waterfall”: fetch data (server) → render to HTML (server) → load code (client) → hydrate (client), now you can do this for each part of the tree
      - So historically, if you had a comments component that was complicated it would increase first load of everything else, and while hydrating nothing would be interactive until everything was
        - Now you can wrap comments in `Suspense` to indicate it can start streaming and hydrating without waiting,
  - Less bundle size = less bandwidth usage, server components aren't included in build so while first paint/content painted same, the time to interactive is faster
    - Means we can use huge libraries([syntax highlighting?](https://bright.codehike.org/)) serverside with no performance impact, so changes way to think about tradeoffs
- Server Components can be used [without SSR](https://github.com/reactjs/server-components-demo?tab=readme-ov-file#should-i-use-this-demo-for-benchmarks)

- “Server Side Rendering” is an umbrella term meaning initial render (ie the HTML) sent to client happens on the server
  - Static site generation(SSG) is at build time, but you could do runtime. Both are distinct from Server Components
    - Traditional SSR hydrates a dom passed as string, but server components pass react elements(JSON) that React runs on client - [Source](https://stackoverflow.com/questions/76325862/what-is-the-difference-between-react-server-components-rsc-and-server-side-ren#:~:text=Server%20components%20return%20react%20elements,and%20put%20into%20the%20DOM.&text=SSR%20is%20to%20run%20code%20on%20the%20server.)
      - This means SSR will give HTML before any js loads, while Server Components are only shown after React loads it
        - See the html generated/under the hood of Server Components [here](https://www.joshwcomeau.com/react/server-components/#peeking-under-the-hood-8)
- Server Components can be rendered at either build or request time
  - Next.js makes it static/buildtime by default

## Features

- Runs some component code at runtime server side

  - Not static state generation(SSG) which can still be useful

  - Why? Instead of fetching in useEffect clientside after loading and parsing js packages, can run on server closer to db

- Can use both rendered Server Components and dynamic Client Components(client components can render on server too bad name)
- Server Components never re-render ie no `useState` etc 
  -  `"use client"` directive to use these interactive hooks
    - Note `"use server"` is for server actions not server components
- `await` in server component will stop rendering with streaming support for Suspense

## Usage

- Use Next.js, could use something else but annoying bundling/hydrating/server/router setup

- Pattern is to put interactive `use client` as low as possible
- Need to explicitly mark interactive components  `use client` 
  - `use client` means all children are also client, it sets the boundary
-  You can’t directly nest Server Components inside Client Components, you can pass Server Components as props/children to Client Components

```ts
import marked from 'marked'; // Not included in bundle
import sanitizeHtml from 'sanitize-html'; // Not included in bundle

async function Page({page}) {
  // NOTE: loads *during* render, when the app is built.
  const content = await file.readFile(`${page}.md`);
  
  return <div>{sanitizeHtml(marked(content))}</div>;
}
```

### Composing Client in Server

`notes.ts`

```ts
//Server Component
import Expandable from './Expandable';

async function Notes() {
  const notes = await db.notes.getAll();
  return (
    <div>
      {notes.map(note => (
        <Expandable key={note.id}>
          <p note={note} />
        </Expandable>
      ))}
    </div>
  )
}
```

`Expandable.ts`

```ts
// Client Component
"use client"

export default function Expandable({children}) {
  const [expanded, setExpanded] = useState(false);
  return (
    <div>
      <button
        onClick={() => setExpanded(!expanded)}
      >
        Toggle
      </button>
      {expanded && children}
    </div>
  )
}
```

*In the browser, the Client Components will see output of the Server Components passed as static props.*

## Advanced

- Watch out for using server components under client components

  - ![use client marking Dashboard component and children as as client components](https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F94d1356a8d524f7581397b76ae98a370?width=717)

  - Next.js removes env variables to prevent API key leaks so watch up if you are calling external API as clientside version fail

- `await` will suspend React across server/client boundary
  - Meaning you can choose to await on the client by passing a promise


```ts
// Server Component
import db from './database';

async function Page({id}) {
  // Will suspend the Server Component.
  const note = await db.notes.get(id);
  
  // NOTE: not awaited, will start here and await on the client. 
  const commentsPromise = db.comments.get(note.id);
  return (
    <div>
      {note}
      <Suspense fallback={<p>Loading Comments...</p>}>
        <Comments commentsPromise={commentsPromise} />
      </Suspense>
    </div>
  );
}
```

`comments.ts`

```ts
// Client Component
"use client";
import {use} from 'react';

function Comments({commentsPromise}) {
  // NOTE: this will resume the promise from the server.
  // It will suspend until the data is available.
  const comments = use(commentsPromise);
  return comments.map(commment => <p>{comment}</p>);
}
```

- Instead of having the component *definition* in a JS file, we have the component's *returned value* inlined in a `<script>` tag. This mean JS smaller, HTML bigger so Server Components aren't *totally* free but overall should be smaller
