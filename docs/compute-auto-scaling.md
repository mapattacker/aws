# EC2 Auto Scaling

There are three main components to EC2 Auto Scaling.

 * **Launch template or configuration**: What resource should be automatically scaled?
 * **EC2 Auto Scaling Group**: Where should the resources be deployed?
 * **Scaling policies**: When should the resources be added or removed?

## Launch Template

You can create a launch template one of three ways. 

 * The fastest way to create a template is to use an **existing EC2 instance**. All the settings are already defined.
 * Another option is to **create one from an already existing template or a previous version of a launch template**.
 * The last option is to **create a template from scratch**. The following options will need to be defined: AMI ID, instance type, key pair, security group, storage, and resource tags.

The launch template has **version control**.

## Auto Scaling Group

To set the auto scaling group, we need to choose the 
 
 * launch template
 * type of EC2 purchase, i.e. on Demand, Spot instances or a hybrid of the two.
 * VPC and Subnets
 * Elastic Load Balancer
 
The next important task is to set the capacity.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/auto-scaling.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Scaling Policies

We can add in CloudWatch an alarm state trigger to activate ACG to launch EC2 instances when a threshold is met.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/auto-scaling2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>