# Boto3

Boto3 is the AWS SDK for Python. To get started, you need to have python installed.

```bash
pip install boto3
```

## Boto3 Types

Boto3 has two types of interfaces, the client and resource. The **client interface** is low level and provides 1-1 mapping with the AWS services' APIs, with the return responses in JSON. All service operations are supported by clients.

The **resource interface** is a high level API, a wrapper for the client interface so that commands are more intuitive. 

Below is an [example](https://docs.basis-ai.com/guides/data-loading-helpers-for-s3-and-gcs/s3-helpers) to download a file from S3.

```python
import boto3

def download_file(bucket_name, origin_blob_path, dest_filename):
    """Download blob from S3 bucket.
    
    Args:
        bucket_name (str)
        origin_blob_path (str)
        dest_filename (str): destination filename
    """
    s3 = boto3.resource("s3")
    s3_bucket = s3.Bucket(bucket_name)
    s3.Bucket(bucket_name).download_file(origin_blob_path, dest_filename)
```

However, it only exposes a subset of AWS API, so **functionalities might be limited**, though we can assess the client interface in the resouce too as shown below.

```python
s3 = boto3.resource("s3").meta.client()
```

## Credentials

To access each of the AWS services, we will need to pass our credentials either as arguments into the client or resource interfaces (not recommended!), or the SDK can detect them within the env variables, or lastly if u set them in your `aws configure`.

## S3

S3 [charges](https://aws.amazon.com/s3/pricing/) for the bandwidth transferred out of S3 if its more than 1GB/mth. One of the ways to reduce this limit is to use `S3 Select` where you send a filter that 