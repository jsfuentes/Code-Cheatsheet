# Dynamo

### Setup

```python
import boto3
from botocore.config import Config

session = boto3.Session(
  aws_access_key_id='AAAAAAAAAAAAAAAA',
aws_secret_access_key='VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV',
)

config = Config(
    region_name = 'us-west-2', 
    retries = {
        'max_attempts': 10,
        'mode': 'standard'
    }
)

ddb_client = session.resource('dynamodb', config=config)
story_category_table = ddb_client.Table('StoryCategory-yyyyyyyyyyyyd3c6xquflibtu-prod')
```

### Get

```python
response = table.get_item(Key={'id': id})

if 'Item' in response:
  retrieved_item = response['Item']
  print("Retrieved Item:", retrieved_item)
else:
  print("Item not found")
```

### Insert

```python
category = {
  'id': str(uuid.uuid4()),
  'title': 'Thirst Trap',
}
    
try:
    response = story_category_table.put_item(Item=category)
    print("PutItem succeeded:", response)
except Exception as e:
    print("Error inserting item:", e)
```

### Update

```python
updated_attributes = {
    'attribute_to_update': 'new_value',
}

response = story_category_table.update_item(
    Key={'your_primary_key': story_category_key},
    UpdateExpression='SET ' + ', '.join([f'{key} = :{key}' for key in updated_attributes]),
    ExpressionAttributeValues={f':{key}': value for key, value in updated_attributes.items()},
    ReturnValues='ALL_NEW'  # Optional, specify if you want to get the updated item's attributes in the response
)

```

## Delete
