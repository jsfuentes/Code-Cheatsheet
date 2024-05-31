# Opensearch

https://localhost:4443/_dashboards/app/dev_tools#/console

AWS elasticsearch rip off

```ts
async function getUsersWithContactCountByPhoneNumberMap(
  ctx: Ctx,
  callerUserId: string,
  phoneNumbers: string[]
) {
  const response = await ctx.openSearchClient.search({
    index: process.env.OPENSEARCH_USER_CONTACT_V1_INDEX_NAME,
    body: {
      size: 0,
      query: {
        bool: {
          must: [
            {
              terms: {
                'phoneNumber.keyword': phoneNumbers,
              },
            },
          ],
          must_not: [
            {
              term: {
                'owner.keyword': callerUserId,
              },
            },
          ],
        },
      },
      aggs: {
        phoneNumbers: {
          terms: {
            field: 'phoneNumber.keyword',
            size: Math.min(phoneNumbers.length, MAX_ES_SIZE),
          },
          aggs: {
            uniqueOwnerCounts: { cardinality: { field: 'owner.keyword' } },
          },
        },
      },
    },
  });

  return response.body?.aggregations?.phoneNumbers?.buckets?.reduce(
    (acc, curr) => ({ ...acc, [curr.key]: curr.uniqueOwnerCounts.value }),
    {} as Record<string, number>
  );
}
```

## Scripting

Go to https://localhost:4443/_dashboards/app/dev_tools#/console

- Can do custom scoring/filters

#### Deving

```
POST /_scripts/painless/_execute
{
  "script": {
    "source": "123",
    "params": {
      "min_honors_gpa": 3.5
    }
  },
  "context": "score",
  "context_setup": {
    "index": "filter-v1",
    "document": {
      "owner": "77a5f57a-d7e8-43a2-b7a7-d7371589a680",
      "createdAt": "2024-02-21T22:16:24.938Z",
      "imageQualityScore": -1,
      "detectedGender": "female",
      "pending": false,
      "detectedEthnicity": "asian",
      "id": "879db7a7-11e2-4428-b457-37a999c154c4",
      "label": "",
      "state": "PUBLIC",
      "tags": [
        {
          "source": "automatic",
          "value": "travel"
        }
      ],
      "thumbnailUrl": "https://optimatik-optix-prod.s3.us-west-2.amazonaws.com/custom-filter-thumbnails/77a5f57a-d7e8-43a2-b7a7-d7371589a680/dc53226c-ae0f-4f61-90c2-a2e278a079ea.png",
      "updatedAt": "2024-02-21T22:18:46.231Z"
    }
  }
}
```
