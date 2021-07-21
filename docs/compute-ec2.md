# EC2

To select the operating system (OS) of the VM, we first need to select the **Amazon Machine Image** (AMI). This can be images created by AWS, community created, offered in the Marketplace, or even one created by yourself.

There are many different EC2 instance types that are [optimized](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html) to either **memory**, **compute**, **accelerated compute** (GPU), **storage**, and **general purpose**. The naming conventions of instance type & size are as such.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-type.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

We can also change the instance type for an instance which was already created.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-change-type.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Pricing

There are three types of EC2 pricing options. **[On Demand](https://aws.amazon.com/ec2/pricing/on-demand/)** means that you only pay for when the instance is up, aka pay-as-you-go model. We can configure the instances to shutdown off office hours, resulting in significant savings. **[Reserved Instances](https://aws.amazon.com/ec2/pricing/reserved-instances/pricing/)** means that you are reserving and paying for the instance on a 1-3 year term. It can be a significant discount (~40%) to On-Demand. **Spot Instances** take advantage of unused EC2 capacity in the AWS Cloud. They are available at up to a 90% discount compared to On-Demand prices.

