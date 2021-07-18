# IAM

AWS Identity and Access Management ([IAM](https://aws.amazon.com/iam/)) enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

## Root User

When we first create a AWS account, it will be created as a root user, having full access over this account. It will be wise to create a user for future logins for security reasons.

## Principle of Least Privilege

An important security recommendation is the principle of least privilege, where we only assign policies to a resource or person based on what they require only.


## ARN

[AWS Resource Names](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) (ARN) are

> uniquely identify AWS resources. We require an ARN when you need to specify a resource unambiguously across all of AWS, such as in IAM policies, Amazon Relational Database Service (Amazon RDS) tags, and API calls.

Every AWS service that you create have an ARN.

## JSON Policy Syntax

There are two main keys in a policy, one is the `Action`, and another is `Resource`. Action indicates the various actions an AWS service can perform while the Resource is the specific service (by ARN) that you launched that have those actions.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:GetLifecycleConfiguration",
                "s3:GetBucketTagging",
                "s3:GetInventoryConfiguration",
                "s3:GetObjectVersionTagging",
                "s3:GetBucketLogging",
                "s3:GetAccelerateConfiguration",
                "s3:GetBucketPolicy",
                "s3:GetObjectVersionTorrent",
                "s3:GetObjectAcl",
                "s3:GetEncryptionConfiguration",
                "s3:GetBucketObjectLockConfiguration",
                "s3:GetIntelligentTieringConfiguration",
                "s3:GetBucketRequestPayment",
                "s3:GetObjectVersionAcl",
                "s3:GetObjectTagging",
                "s3:GetMetricsConfiguration",
                "s3:GetBucketOwnershipControls",
                "s3:GetBucketPublicAccessBlock",
                "s3:GetBucketPolicyStatus",
                "s3:GetObjectRetention",
                "s3:GetBucketWebsite",
                "s3:GetBucketVersioning",
                "s3:GetBucketAcl",
                "s3:GetObjectLegalHold",
                "s3:GetBucketNotification",
                "s3:GetReplicationConfiguration",
                "s3:PutObject",
                "s3:GetObject",
                "s3:GetObjectTorrent",
                "s3:GetBucketCORS",
                "s3:GetAnalyticsConfiguration",
                "s3:GetObjectVersionForReplication",
                "s3:GetBucketLocation",
                "s3:GetObjectVersion"
            ],
            "Resource": [
                "arn:aws:s3:::dragon-data-sy/*",
                "arn:aws:s3:::dragon-data-sy"
            ]
        }
    ]
}
```

This can be further shorterned by using the asterisk symbol.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:Get*"
            ],
            "Resource": [
                "arn:aws:s3:::dragon-data-sy/*",
                "arn:aws:s3:::dragon-data-sy"
            ]
        }
    ]
}
```