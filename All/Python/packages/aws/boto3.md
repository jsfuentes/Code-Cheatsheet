# AWS Boto3

Aws credentials must be configured, [*Quickstart*](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/quickstart.html).

```bash
pip install boto3
```

```python
import boto3
s3 = boto3.client('s3')
```

## S3

- `boto3.client("s3")` for low level
- `boto3.resource('s3')` for higher level stuff

```python
def all_objects(filter="mp4", bucket_name="interdimensional-news"):
    s3 = boto3.resource('s3')
    bucket = s3.Bucket(bucket_name)
    all_urls = []
    for obj in bucket.objects.all():
        if obj.key.endswith(filter):
           all_urls.append(construct_url(bucket_name, obj.key))

    return all_urls

def get_object(object_key="space_whales.mp3", file_name="test33.mp3", bucket_name="interdimensional-news"):
    client = boto3.client('s3')

    resp = client.get_object(Bucket=bucket_name, Key=object_key)
    all_binary = resp["Body"].read()

    with open(file_name, "wb") as f:
        f.write(all_binary)

def put_content(body, content_type="video/mp4", object_key="default/test3.mp4", bucket_name="interdimensional-news"):
    s3 = boto3.resource('s3')
    bucket = s3.Bucket(bucket_name)
    bucket.put_object(Key=object_key, Body=body, ContentType=content_type)
    print(f"Successfully uploaded {object_key} to S3")

def construct_url(bucket_name, object_key):
    url = "https://%s.s3.amazonaws.com/%s" % (bucket_name, object_key)
    return url
```

### List 

```python
s3 = boto3.resource('s3')

for bucket in s3.buckets.all():
    print(bucket.name)
```

### Create

```python
s3.create_bucket(Bucket='my-bucket')
```

### Upload

```python
s3.meta.client.upload_file('/tmp/hello.txt', 'mybucket', 'hello.txt')
```

```python
with open('filename', 'rb') as data:
    s3.upload_fileobj(data, 'mybucket', 'mykey')
```

### Presigned URL

Allow clients to access the resource 

```python
url = s3.generate_presigned_url(
    ClientMethod='get_object',
    Params={
        'Bucket': 'bucket-name',
        'Key': 'key-name'
    }
)
```

### Download

```python
import boto3
import botocore

BUCKET_NAME = 'my-bucket' # replace with your bucket name
KEY = 'my_image_in_s3.jpg' # replace with your object key

s3 = boto3.resource('s3')

try:
    s3.Bucket(BUCKET_NAME).download_file(KEY, 'my_local_image.jpg')
except botocore.exceptions.ClientError as e:
    if e.response['Error']['Code'] == "404":
        print("The object does not exist.")
    else:
        raise
```

