# CloudFormation

AWS CloudFormation allows us to deploy our AWS infrastructure **stack** inside a template file. This template file is then uploaded to CloudFormation build the stack.

We can define the template in either a JSON or YAML format.

```yaml
Resources:
  Ec2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      SecurityGroups:
        - !Ref InstanceSecurityGroup
      KeyName: mykey
      ImageId: ''
  InstanceSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '22'
          ToPort: '22'
          CidrIp: 0.0.0.0/0
```

CloudFormation is similar to [Terraform](https://www.terraform.io) with the difference that Terraform can be used to serve multiple cloud providers, not just AWS.