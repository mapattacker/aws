# AWS CLI

The [AWS Command Line Interface](https://aws.amazon.com/cli/), **AWS CLI** for short, allows us to easily access AWS services in the terminal. 

## Installation

If you’re using Amazon EC2 instances or AWS Cloud9, the tools are already installed for you.

To install in your local machine, refer to this [guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

## Command Syntax

```bash
# command syntax
aws --<optional-command> <main-command> <subcommand> <parameters>

# e.g.
aws s3 mb s3://bucketname
```

We can find more info in the online CLI help docs, or just type `aws <optional: command> <optional: subcommand> help`, e.g. `aws s3 mb help` if needed.

## Configure

To make it easier to send commands without the need to enter the credentials everytime, we can set a default profile or a specific profile name with those variables. The 4 credentials are the **access and secret keys**, **region**, and **output format** (default is `json`).

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/aws-cli1.png?raw=true" style="width:50%" />
  <figcaption>AWS Configure</figcaption>
</figure>

| Cmd | Desc |
|-|-|
| `aws configure` | enter access, secret & region names, for default profile |
| `aws configure --profile <name>` | enter access, secret & region names, based on a specific name |
| `aws s3 ls --profile <name>` | enter commands based on profile |

These credentials are stored in `~/.aws/credentials`.
 