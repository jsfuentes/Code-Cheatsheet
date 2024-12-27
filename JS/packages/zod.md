# Zod

Zod is a TypeScript-first schema declaration and validation library

- declare a validator *once* and infers static TypeScript type
- [libraries adapters](https://github.com/colinhacks/zod?tab=readme-ov-file#ecosystem) like react-hook-form

```bash
npm install zod
```

Requires TypeScript 4.5+ and `strict` mode in your `tsconfig.json`

```json
// tsconfig.json
{
  // ...
  "compilerOptions": {
    // ...
    "strict": true
  }
}
```

## Usage

```ts
import { z } from "zod";

const User = z.object({
  username: z.string(),
});

User.parse({ username: "Ludwig" });

// extract the inferred type
type User = z.infer<typeof User>;
// { username: string }
```

```
{
    NODE_ENV: 

    DATABASE_URL: z.string().url(),
    PRISMA_LOG_LEVEL: z.string().optional(),
```



### Types

#### Primitatives

```ts
import { z } from "zod";

// primitive values
z.string();
z.number();
z.bigint();
z.boolean();
z.date();
z.symbol();

// empty types
z.undefined();
z.null();
z.void(); // accepts undefined

// catch-all types, allows any value
z.any();
z.unknown();

z.never(); // allows no values

z.enum([`development`, `test`, `production`])
 .default(`development`),
```

##### String Validation

```ts
// validations
z.string().max(5);
z.string().min(5);
z.string().length(5);
z.string().email();
z.string().url();
z.string().emoji();
z.string().uuid();
z.string().nanoid();
z.string().cuid();
z.string().cuid2();
z.string().ulid();
z.string().regex(regex);
z.string().includes(string);
z.string().startsWith(string);
z.string().endsWith(string);
z.string().datetime(); // ISO 8601; by default only `Z` timezone allowed
z.string().ip(); // defaults to allow both IPv4 and IPv6

// transforms
z.string().trim(); // trim whitespace
z.string().toLowerCase(); // toLowerCase
z.string().toUpperCase(); // toUpperCase

// added in Zod 3.23
z.string().date(); // ISO date format (YYYY-MM-DD)
z.string().time(); // ISO time format (HH:mm:ss[.SSSSSS])
z.string().duration(); // ISO 8601 duration
z.string().base64();
```

