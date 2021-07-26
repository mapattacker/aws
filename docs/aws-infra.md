# Infrastructure

There are data centers in Availability Zones (AZ) and AZs within Regions. Both AZs and Regions have **redundancies**.

## Regions

Region is a cluster of data centers, or Availability Zones. We should choose regions based on the following, with compliance being the priority. 

AWS Regions are independent from one another. This means that your data is not replicated from one Region to another, without your explicit consent and authorization.

| Considerations | Desc |
|-|-|
| Compliance | with data governance & legal requirements |
| Latency | hosted proximity to consumer |
| Pricing | varies with regions due to, e.g. tax structure |
| Available Services | not all services within a region |

Regions are represented by codes e.g. Singapore is `ap-southeast-1`.

In the management console, we can choose the region at the top right corner of the screen.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/infra-region.png?raw=true" style="width:60%" />
  <figcaption></figcaption>
</figure>

Note that there are some services which are global by nature, while others are region specific. For example, switching to another region, you can still see the same IAM service with your data as it is a global service, while your EC2 instances will not appear as it is region specific.

## Availability Zones

AZ(s) or Availability Zones individual data centres within a region, but have redundancy from each other. 

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/infra-az.png?raw=true" style="width:60%" />
  <figcaption></figcaption>
</figure>

## Edge Locations

Edge Locations are **Content Delivery Network** (CDN) endpoints of CloudFront. 

## Interacting with AWS API

There are 3 ways which we can interact with AWS services, which include the AWS Management Console, AWS Command Line Interface (AWS CLI), and AWS Software Development Kits (AWS SDKs).