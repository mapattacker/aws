# IAM

AWS Identity and Access Management ([IAM](https://aws.amazon.com/iam/)) enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

There are two important terms in security. The first is **Authentication**; being verifying if someone is who they say they are because they logged in with the proper credentials. We can create new user login accounts for this. The second term is **Authorization**, where the policies assign permissions to allow or deny you access to actions for certain AWS resources.

<hr> 

## Security Models

### Shared Responsibility Model

Both AWS and yourself have responsibilities in security. AWS are responsibility for security of the cloud, which include the global infrastructure, and software to the virtualization layer. You are responsible for the security in the cloud.

### Principle of Least Privilege

An important security recommendation is the principle of least privilege, where we only assign policies to a resource or person based on what they require only.

<hr> 

## User Access

Users have static credential keys; i.e. username, password, access keys, and secret keys.

### Root User

When we first create a AWS account, it will be created as a root user, having full access over this account. It will be wise to create a user for future logins for security reasons, as well as setting an **MFA** for this root account.

### User Groups

We can add new users and assign policy permissions to authorize these users. However, it is recommended instead to assign **user groups** with  permissions to these groups, and add users to these user groups. This way, the groups are tied to specific job roles and make management easier.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/iam-group.png?raw=true" style="width:80%" />
  <figcaption>AWS Cloud Essentials Course</figcaption>
</figure>


<hr> 

## Roles

For AWS services requiring programmatic access to other services, a role based access needs to be created. An IAM role is an identity you can create that has specific permissions with credentials that are **valid for short durations**. Roles do not have static login credentials.

### Identity Provider

If you have an organization that spans many employees and multiple AWS accounts, you may want your employees to sign in with a single credential. This can be done using a third-party identity provider, which uses AWS roles to grant access to each of these so-called **federated user**.

We can also use **AWS SSO**, an IdP that lets your users sign in to a user portal with a single set of credentials. It then provides them access to all their assigned accounts and applications in one central location.



### ARN

[AWS Resource Names](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) (ARN) are

> uniquely identify AWS resources. We require an ARN when you need to specify a resource unambiguously across all of AWS, such as in IAM policies, Amazon Relational Database Service (Amazon RDS) tags, and API calls.

Every AWS service that you create have an ARN.

<hr> 

## JSON Policy Syntax

There are three main keys in a policy; `Action`, `Effect`, and `Resource`. Action indicates the various actions an AWS service can perform, Effect indicates to allow or deny the actions, while the Resource is the specific service (by ARN) that you launched that have those actions.

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