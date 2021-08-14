# Billing

The fundamentals of pricing of AWS services are as follows

 1. Charge when using Compute, Data Storage, and Out Bound Data
 2. Pay-As-You-Go model
 3. Reserve (paying upfront for EC2 & RDS)
 4. Pay less by using more

## Services

### EC2

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/billing-ec21.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>


<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/billing-ec22.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>


<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/billing-ec23.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## AWS Pricing Calculator

The pricing calculator allows you to add AWS services and their configurations to get an estimation of the pricing.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/billing-pricing-cal.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## AWS Cost Explorer

Allows us to visualize usage patterns over time and to identify underlying cost drivers. We can also create a forecast by selecting a future time range for your report.

 * which service used the most
 * which linked account used the most
 * which region or AZ used the most

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/billing-cost-explorer.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## AWS Budgets

Budgets gives alerts when the cost reaches or exceeds actual or forecasted threshold.