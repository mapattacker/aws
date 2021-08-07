# S3

AWS S3 stands for Simple Storage Service.

There are various classes of S3, based on how frequently they are accessed.

| Class | Desc |
|-|-|
| S3 Standard | General purpose |
| S3 Intelligent Tier | Auto change of tier |
| S3 Infrequent Access | Access less frequent, but requires rapid access |
| S3 Glacier | Archival purpose (mins/hours retriveal) |
| S3 Deep Glacier | Access only once or twice a year (24h retrieval) |

## SDK helper functions

```python
import boto3


s3 = boto3.resource('s3')


def upload_file(s3, local_filepath, bucketname, s3_filepath):
    """upload a file to S3"""
    s3.meta.client.upload_file(local_filepath, bucketname, s3_filepath)
    print(f"upload {local_path} complete")


def download_file(s3, bucket_name, s3_filepath, local_filepath):
    """Download file from S3"""
    s3.Bucket(bucket_name).download_file(s3_filepath, local_filepath)
    print(f"download {s3_filepath} complete")


def query_json(s3, bucketname, SQL_expression, s3_filepath)
    """select query from json; filter query is done in S3 so its much cheaper"""
    SQL_expression = """select * from S3Object[*][*] as s where s.family_str = 'blue' """  
    result = s3.select_object_content(
                Bucket=bucket_name,
                Key=file_name,
                ExpressionType='SQL',
                Expression=SQL_expression,
                InputSerialization={'JSON': {'Type': 'Document'}},
                OutputSerialization={'JSON': {}}
    return result


if __name__ == "__main__":
    local_path = "/home/dragon_stats_one.json"
    bucketname = "dragon-data"
    s3_path = "dragon_stats_one.json"
    upload_file(s3, local_path, bucketname, s3_path)
```


## AWS CLI

Note that all bucket URLs in aws cli must have the prefix with `s3://bucket-name/example`. More high level commands in the official [documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html).

| Command | Desc |
|-|-|
| `aws s3 ls <target>` | List buckets or files in a bucket etc. |
| `aws s3 cp <source> <target>` | Copy file from s3/local vice versa |
| `aws s3 mv <source> <target>` | move file a bucket location or to local |
| `aws s3 rm s3://<filepath>` | delete file in bucket |
| `aws s3 rm s3://<my-bucket/path> --recursive` | remove all files in directory |


