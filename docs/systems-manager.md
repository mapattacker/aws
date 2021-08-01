# Systems Manager

The AWS Systems Manager helps to manage multiple AWS resources including EC2, S3, RDS, etc.

This includes automation, run command, inventory, and others stated below.

## Automation and Run Command

Systems Manager have feature called document, whereby you can select some automation or commands to various AWS resources.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/sys-manager1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Inventory

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/sys-manager2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Patch Manager

The patch manager can deploy system and software packages to groups of EC2 instances and also on-premises

## Compliance

This feature can scan our managed instances for patch compliance and configuration inconsistencies.

## Session Manager

The session manager allows us to get a secure session into your instances without having to open the firewall rules to
allow access to those other ports. This means that you don't need to use the secure shell, the SSH protocol or the remote desktop to access our instances.

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