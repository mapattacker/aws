# Infrastructure

There are data centers in Availability Zones (AZ) and AZs within Regions. Both AZs and Regions have **redundancies**.

## Regions

Region is a cluster of data centers, or Availability Zones. We should choose regions based on the following, with compliance being the priority.

| Considerations | Desc |
|-|-|
| Compliance | with data governance & legal requirements |
| Latency | hosted proximity to consumer |
| Pricing | varies with regions due to, e.g. tax structure |
| Available Services | not all services within a region |

Regions are represented by codes e.g. Singapore is `ap-southeast-1`.

In the management console, we can choose the region at the top right corner of the screen.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/infra-region.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Availability Zones

