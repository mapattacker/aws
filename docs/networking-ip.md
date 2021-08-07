# IP Address

Internet Protocol Address is a numerical value used for host or network interface identification and location addressing.

There are two notations of IP address, the IPv4 and IPv6.

In AWS there are 3 types of IP addresses.

| Private IP | Public IP | Elastic IP |
|-|-|-|
| Retained with instance stop | Change when instance restart | Associated to Private IP |
| All instances will have | Only Public instances have | For Public IPs only |
| - | - | Can be dissociated and linked to a different Private IP |
| Free | Free | Charged only when associated but not used |

Private, Public and Elastic IP stated in an EC2 instance.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ip1.png?raw=true" style="width:100%" />
  <figcaption>AWS Cloud Essentials Course</figcaption>
</figure>