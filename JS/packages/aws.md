# AWS SDK

### DynamoDB

- dynamoDB is NoSQL so need to for whatever index you use you must include some condition for the index and sorting key in the keyconditionexpression
  - Might need to create a new index or scan

## V3

- Better than V2(aws-sdk) cuz allows selective importing and typescript and async is first class

```bash
npm i @aws-sdk/lib-dynamodb @aws-sdk/client-dynamodb
```

##### Setup

```javascript
import { DynamoDBClient } from '@aws-sdk/client-dynamodb';
import { DynamoDBDocument } from '@aws-sdk/lib-dynamodb';

ddbClient = DynamoDBDocument.from(
      new DynamoDBClient({
        apiVersion: '2012-08-10',
        region: process.env.AWS_REGION,
      })
    )
```

##### Get

```js
import { GetCommand } from '@aws-sdk/lib-dynamodb';

const response = await ddbClient.send(
  new GetCommand({
    TableName: process.env.THEME_DYNAMODB_TABLE,
    Key: { id },
  })
);

const filter = response.Item as Filter;
```

#### Update

```js
import { UpdateCommand } from '@aws-sdk/lib-dynamodb';

await ddbClient.send(
  new UpdateCommand({
    TableName: `Notification-${appsyncApiId}-${env}`,
    Key: { id: accumulatingNotif.id },
    UpdateExpression: 'ADD #count :inc SET #updatedAt = :now',
    ExpressionAttributeNames: {
      '#count': 'count',
      '#updatedAt': 'updatedAt',
    },
    ExpressionAttributeValues: {
      ':inc': 1,
      ':now': now,
    },
  })
);
```

#### Create

```js
await ddbClientV3.send(
  new PutCommand({
    TableName: `Notification`,
    Item: {
      id: notificationId,
      to: owner.id,
      type: 'inspired_optix',
      createdAt: now,
      updatedAt: now,
    },
  })
);
```

#### Query

```ts
const filters: Filter[] = [];
let nextToken: Record<string, any>;
do {
  const response = await ddbClient.send(
    new QueryCommand({
      TableName: process.env.CUSTOM_THEME_DYNAMODB_TABLE_NAME,
      KeyConditionExpression: '#state = :state',
      ExpressionAttributeNames: {
        '#state': 'state',
      },
      ExpressionAttributeValues: {
        ':state': 'PUBLIC',
      },
      ExclusiveStartKey: nextToken,
      IndexName: 'ByStateCreated',
    })
  );

  nextToken = response.LastEvaluatedKey;
  filters.push(...(response.Items as Filter[]));
} while (nextToken != null);
```

#### Scan

```ts
const users: User[] = [];
let response: ScanCommandOutput | null = null;

do {
  response = await ctx.ddbClient.send(
    new ScanCommand({
      TableName: process.env.USER_DYNAMODB_TABLE_NAME,
      ExclusiveStartKey: response ? response.LastEvaluatedKey : undefined,
      FilterExpression:
        '#notificationsEnabled = :notificationsEnabled AND #createdAt > :createdAt',
      ExpressionAttributeNames: {
        '#createdAt': 'createdAt',
        '#notificationsEnabled': 'notificationsEnabled',
      },
      ExpressionAttributeValues: {
        ':createdAt': startDate,
        ':notificationsEnabled': true,
      },
    })
  );

  users.push(...(response.Items as User[]));
} while (response.LastEvaluatedKey != null);
```

## V2

##### Setup

`npm i aws-sdk`

```javascript
import AWS from 'aws-sdk';

const ddbClient: AWS.DynamoDB.DocumentClient = new AWS.DynamoDB.DocumentClient({
    region: 'us-west-2',
    apiVersion: 'latest',
});
```

##### Get

```js
const resp = await ddbClient.get({
  TableName : 'Table',
  Key: { '<idname>': someValue }
}).promise(); 

const item = resp?.Item;
```

##### Query

```javascript
const response = await ddbClient
  .query({
      TableName: tableName,
      KeyConditionExpression: '#owner = :owner and #createdAt BETWEEN :start and :end',
      FilterExpression: '#imageQualityScore > :score',
      ExpressionAttributeNames: {
          '#imageQualityScore': 'image_quality_score',
          '#owner': 'owner',
          '#createdAt': 'createdAt'
      },
      ExpressionAttributeValues: {
          ':score': 0.3,
          ':owner': "6c3d137a-575b-4a57-86b9-5a87ba3b465f",
          ':start': '1970-01-01T00:00:00Z',
          ':end': '2999-01-01T00:00:00Z'
      },
      IndexName: 'ByOwner',
      ScanIndexForward: false
  })
  .promise();

//fullScan
const users = [];
let nextToken;
do {
    const response: AWS.DynamoDB.DocumentClient.ScanOutput = await ddbClient
        .scan({
            TableName: `User-${appsyncApiId}-${env}`,
            ExclusiveStartKey: nextToken,
        })
        .promise();

    users.push(...response.Items!);
    nextToken = response.LastEvaluatedKey;
} while (nextToken);
```

##### Update

```java
// update field
const updateResp = await ddbClient
  .update({
      TableName: tableName,
      Key: { 'id': item.id },
      UpdateExpression: 'set #ranking = :ranking',
      ExpressionAttributeNames: {
          '#ranking': 'ranking'
      },
      ExpressionAttributeValues: {
          ':ranking': newRanking
      },
      ReturnValues: 'ALL_NEW'  // This will return the updated item attributes
  }).promise();
const newItem = updateResp.Attributes;

//Increment counter
const resp = await ddbClient
      .update({
        TableName: themeTableName,
        Key: { Id: { S: styleId } },
        UpdateExpression: "SET remixCount = remixCount + :i",
        ExpressionAttributeValues: { ":i": { N: "1" } }
      })
      .promise();

//Remove field
const updateResp = await ddbClient
    .update({
        TableName: tableName,
        Key: { 'id': item.id },
        UpdateExpression: 'remove #ranking = :ranking',
        ExpressionAttributeNames: {
            '#ranking': 'ranking'
        },
        ExpressionAttributeValues: {
            ':ranking': 1
        },
        ReturnValues: 'UPDATED_NEW'  // This will return the updated item attributes
    }).promise();
```

