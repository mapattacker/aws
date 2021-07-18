# API Gateway

[API Gateway](https://aws.amazon.com/api-gateway/) is a 

> fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway.png?raw=true" style="width:100%" />
  <figcaption>A gateway to AWS services</figcaption>
</figure>

## Models & Mappings

We can use API Gateway as a proxy for our backend.

If we use REST API Gateway we can:

 * Validate requests & responses with models
    * written in JSON
    * done at Method Request/Response
 * Transform requests & responses with mappings
    * written in VTL language
    * done at Integration Request/Response

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway1.png?raw=true" style="width:100%" />
  <figcaption>Method & Integration for Requests & Responses</figcaption>
</figure>

## Deployment

Once a REST API is created in API Gateway, it doesn’t automatically become available to invoke. We need to publish the API first. 

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway2.png?raw=true" style="width:80%" />
  <figcaption>Deploying the API</figcaption>
</figure>

In API Gateway, we publish the API to a stage.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway3.png?raw=true" style="width:80%" />
  <figcaption>Indicate deployment stage</figcaption>
</figure>

The API endpoint will be appended with the stage path, e.g., for dev stage, it would be `https://a69m13u8y3.execute-api.ap-southeast-1.amazonaws.com/dev`. For each stage, we can add configurations to it, e.g., throttling, logs, or canary deployment.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway4.png?raw=true" style="width:100%" />
  <figcaption>Choosing EC2 instance type & cost savings setting when launching a Cloud9 instance</figcaption>
</figure>

## API Authorization

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway5.png?raw=true" style="width:100%" />
  <figcaption>Some ways we can authorize and authenticate users of our API</figcaption>
</figure>

### CORS

By default, if the API is executed from a different domain, this will be blocked by AWS. However, we can enable it in API-Gateway by enabling Cross Origin Resource Sharing (CORS).

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-gateway6.png?raw=true" style="width:100%" />
  <figcaption>Allowing CORS</figcaption>
</figure>

### API-Key

An [API-key](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-setup-api-key-with-console.html) is a password that is generated to an API-user. With this, only the correct api-key have access to the API. However, as it is a password string sent within a request, it is not very secure.

The upside of this method is that, we can tag a usage plan for a particular API-key, including the **quota** (# request/mth) and **throttling** (# request/sec).

First we will need to create an API key. Copy the API key generated. The key is retrieval, unlike your AWS credentials which can only be generated once.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-key1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Then, we will need to create a usage plan and add the API Key to that plan.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-key2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Once that is done, we will need to assign an API Stage & Method with this plan.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-key4.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Last, we will need to go to the Resouces > click on the API method > Method Request > Settings > change the **API Key Required** to true. Once that is done, we redeploy the API.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/api-key3.png?raw=true" style="width:50%" />
  <figcaption>Change API Key Required to True</figcaption>
</figure>

Lastly, we can try accessing the API by adding it as a header in the request with the key name `x-api-key`.

### IP Whitelisting

We can use the API gateway resource policy to limit access to specific IP addresses. An example below.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "execute-api:Invoke",
            "Resource": "execute-api:/*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": [
                        "1.2.3.4/32"
                    ]
                }
            }
        }
    ]
}
```

### VPC Endpoint Policy

For private APIs, we can improve the security by configuring the policy at the VPC endpoints. 

### Cognito

AWS [Cognito](https://aws.amazon.com/cognito/) consists of user pool & identity pool, which are two separate services. [User pool](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html) is a user directory in Cognito, and it also provides a UI for users to sign into your app.

If we only need to authorize an API gateway, we can just use the user-pool. This involves signing in to cognito via their UI and obtaining a JSON Web Token (JWT).

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cognito-up.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

However, if we require access to other AWS services besides just API gateway, we will need to use an identity pool.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cognito-idp.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

