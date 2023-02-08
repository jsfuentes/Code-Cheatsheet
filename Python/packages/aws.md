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

### List 

```python
response = s3.list_buckets()
buckets = [bucket['Name'] for bucket in response['Buckets']]
print("Bucket List: %s" % buckets)
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

