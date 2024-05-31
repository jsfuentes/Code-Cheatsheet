# [Amplify](https://docs.amplify.aws/cli/graphql/data-modeling/)

- A managed serverless backend that is a layer onto of AppSync(Managed GraphQL API) and Lambda functions
- [17 Query patterns](https://docs.amplify.aws/cli-legacy/graphql-transformer/dataaccess/)

```bash
amplify push --iterative-rollback #to rollback the last-known-good state
amplify push --force #rollback the last-known-good state and try redeploying your changes again using.
```

## Modeling

Primitatives: ID | String | Int | Float | Boolean | 

AWS Types: AWSDate | AWSTime | AWSDateTime | AWSTimestamp | AWSEmail | AWSJSON | AWSPhone | AWSURL | AWSIPAddress

```graphql
type Post @model {
  id: ID!
  title: String!
  comments: [Comment] @hasMany
}

type Comment @model {
  id: ID!
  content: String!
}
```

### Advanced Modeling

#### Adding Indexes

- The primary key of an index must use equality, the secondary/sort key can use gt, ge, lt, le, eq, beginsWith, and between
- Can have multiple sort keys and will created composite key, so you can query by more then three values
  - May need to backfill composite key

- `@index` is basically `@key` v2 and is used to define secondary index, while `@primaryKey` is for primary keys

```
type StoryLike @model @auth(rules: [{ allow: public }]) {
  userId: String! @primaryKey(sortKeyFields: ["storyId"])
  user: User @hasOne(fields: ["userId"])
  storyId: String!
  story: Story @hasOne(fields: ["storyId"])

  createdAt: String!
  updatedAt: String!
}
```

Will error out if the index primary or secondary key does not exist

```graphql
type Ranking @model @auth(rules: [{ allow: public }]) {
  id: String! @primaryKey

  type: String!
    @index(name: "ByTypeStatus", sortKeyFields: ["status"], queryField: "rankingByTypeStatus")
  userId: String!
    @index(name: "ByUserStatus", sortKeyFields: ["status"], queryField: "rankingByUserStatus")
  user: User @hasOne(fields: ["userId"])
  rank: Int! @default(value: "0")
  lastRank: Int
  status: String!

  createdAt: String!
  updatedAt: String!
}
```

## Using Javascript

#### [Query](https://docs.amplify.aws/lib/graphqlapi/query-data/q/platform/js/#simple-query)

```ts
import { API } from 'aws-amplify';
import { ThemesByEnabledQuery, Theme } from '../../API';
import { themesByEnabled } from '../../graphql/queries';

async function getEnabledThemes(): Promise<Theme[] | null> {
  console.log('getting enabled themes');

  try {
    const response = (await API.graphql({
      query: themesByEnabled,
      variables: {
        enabled: 1,
      },
    })) as { data: ThemesByEnabledQuery };

    const data = response.data.themesByEnabled;

    if (!data) {
      throw new Error('Data was null');
    }

    return data.items ?? null;
  } catch (err) {
    console.error('Failed to get enabled themes', err);
    return null;
  }
}

export default getEnabledThemes;

```

