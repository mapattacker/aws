# Systems Manager

## Parameter Store

The [parameter store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html) provides

> secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, Amazon Machine Image (AMI) IDs, and license codes as parameter values. You can store values as plain text or encrypted data.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/parameter-store1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Example of using parameter store to extract some variables.

```python
import boto3

ssm = boto3.client('ssm', 'ap-southeast-1')
bucket_name = ssm.get_parameter( Name='dragon_data_bucket_name',WithDecryption=False)['Parameter']['Value']
file_name = ssm.get_parameter( Name='dragon_data_file_name',WithDecryption=False)['Parameter']['Value']
```