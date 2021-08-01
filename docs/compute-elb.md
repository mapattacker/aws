# Elastic Load Balancer

Load balancing refers to the process of distributing tasks across a set of resources. 

A typical request for an application would start from the browser of the client. It’s sent to a load balancer. Then, it’s sent to one of the EC2 instances that hosts the application. The return traffic would go back through the load balancer and back to the client browser. Thus, the load balancer is directly in the path of the traffic.

## Benefits

 * The fact that ELB can load balance to IP addresses means that it can work in a hybrid mode as well, where it **also load balances to on-premises servers**.
 * ELB is **highly available**. The only option you have to ensure is that the load balancer is deployed across multiple Availability Zones.
 * In terms of scalability, ELB **automatically scales** to meet the demand of the incoming traffic. It handles the incoming traffic and sends it to your backend application.

## Types

There are 3 types of load balancers in AWS, **Application Load Balancer**, **Network Load Balancer**, and **Gateway Load Balancer**.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb1.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

The differences between Application & Network Load Balancers are as follows.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb2.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

## Components

There are three components in an ELB.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb3.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

 * **Listeners**: The client connects to the listener. This is often referred to as client-side. To define a listener, a port must be provided as well as the protocol, depending on the load balancer type. There can be many listeners for a single load balancer.
 * **Target groups**: The backend servers, or server-side, is defined in one or more target groups. This is where you define the type of backend you want to direct traffic to, such as EC2 Instances, AWS Lambda functions, or IP addresses. Also, a health check needs to be defined for each target group.
 * **Rules**: To associate a target group to a listener, a rule must be used. Rules are made up of a condition that can be the source IP address of the client and a condition to decide which target group to send the traffic to.

Health checks are important to ensure that an instance is working fine before the load balancer directs traffic to it.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb4.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

## Configuring ELB

Below are the steps to build an Application Load Balancer.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb5.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

We need to set the listeners, and define the VPC, AZs and their corresponding subnets within each AZ.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb6.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

Second, we select the target group, and health check route.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/elb7.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

Last, we select the targets, which in this case are the ec2 instances in the earlier selected subnets.