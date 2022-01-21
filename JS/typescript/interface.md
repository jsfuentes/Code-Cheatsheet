# Interfaces

```typescript
type PresenceList = Array<{metas: Array<UserPresenceInfo>}>;
type PresenceById = Record<string, UserPresenceInfo>;

interface UserPresenceInfo {
  group_id: string | null;
  hasLoaded: boolean;
  headline: string;
  id: string;
  is_admin: boolean;
  name: string;
  online_at: string;
  phx_ref: string;
  phx_ref_prev: string;
  picture: string; 
  social_links: Array<string>;
  status: string;
}

interface PresenceState {
  attendees : {
    byId: PresenceById;
    allIds: Array<string>
  },
  waiting : {
    byId: PresenceById
    allIds: Array<string>
  },
  blocked : {
    byId: PresenceById
    allIds: Array<string>
  },
  groups: Record<string, Array<string>>
}
```

Example 2

```ts
interface Message {
  from: {
    id: string,
    picture: string,
    name: string,
    headline?: string //optional
  },
  timestamp: string,
  text: string,
  type: "user_join" |
  "message" |
  "user_leave" |
  "announcement" |
  "question"
}
```

