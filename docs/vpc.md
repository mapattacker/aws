# VPC

Amazon **Virtual Private Cloud** ([VPC](https://aws.amazon.com/vpc/?vpc-blogs.sort-by=item.additionalFields.createdDate&vpc-blogs.sort-order=desc)) is a service that lets you launch AWS resources in a logically isolated virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

| Terms | Desc |
|-|-|
| VPC | An isolated network you create in the AWS cloud |
| Subnet | Smaller isolated networks inside VPC |
| Internet Gateway | Enable internet to VPC |
| Route Tables | Direct traffic at VPC or subnet |

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc1.png?raw=true" style="width:100%" />
  <figcaption>VPC with Subnets</figcaption>
</figure>

## IP & CIDR Notation

An example of a IPv4 address is `192.168.1.30`. If we want to specify a range of IPs between 192.168.1.0 and 192.168.1.255, we can use the Classless Inter-Domain Routing (CIDR) notation, to represent as `192.168.1.0/24`

**The higher the number after the /, the smaller the number of IP addresses in your network**. For example, a range of 192.168.1.0/24 is smaller than 192.168.1.0/16. 

When working with networks in the AWS Cloud, you choose your network size by using CIDR notation. In AWS, the smallest IP range you can have is **/28**, which provides you 16 IP addresses. The largest IP range you can have is a **/16**, which provides you with 65,536 IP addresses.

## Creating VPC

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Creating Subnet

As mentioned to compartmentalize our traffic in our VPC, we can divide them into subnets.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc4.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Gateways

A subnet can be public or private depending on whether it is assign to an internet gateway. To do that, we first create an internet gateway, and associate it with our VPC.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc3.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Routing Tables

A main route table is automatically create to route traffic to our VPC. However, we need further directions to guide the traffic to each subnet, for that, we can create custom route tables.

First we association the table with our VPC.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc5.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Then, we edit the route, and add in `0.0.0.0/0` meaning it can take and deliver traffic from anywhere, and assign it to our previously created internet gateway.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc6.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Last, we edit the subnet associations and add the subnets we want internet access to.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc7.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Below shows an overall diagram on setting up of the VPC, subnets, and internet gateway and routing tables.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc-diagram.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Security

### ACL Tables for Subnets

Think of a network ACL (access control list) as a firewall at the subnet level. A network ACL enables you to control what kind of traffic is allowed to enter or leave your subnet. You can configure this by setting up rules that define what you want to filter.

Network ACL’s are considered stateless, so you need to include both the inbound and outbound ports used for the protocol. If you don’t include the outbound range, your server would respond but the traffic would never leave the subnet. 

### Security Groups for EC2

Security group is a firewall you define for your EC2 instances. The default configuration of a security group blocks all inbound traffic and allows all outbound traffic.

The default configuration of a security group blocks all inbound traffic and allows all outbound traffic. To enable internet access, we need to open `ports 80 (HTTP)` and `443 (HTTPS)`. We only need to define inbound rules as security groups are **stateful**.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/vpc-security-gp.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>