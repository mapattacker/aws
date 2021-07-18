# Lambda

AWS [Lambda](https://aws.amazon.com/lambda/) is 

> a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes.

> We can upload our code as a ZIP file or container image, and Lambda automatically and precisely allocates compute execution power and runs your code based on the incoming request or event, for any scale of traffic. We can also set up your code to automatically trigger from over 200 AWS services and SaaS applications or call it directly from any web or mobile app.

## Execution Environment

It takes time to set up an execution context and do the necessary "bootstrapping", which adds some latency each time the Lambda function is invoked. You typically see this latency when a Lambda function is invoked for the first time or after it has been updated because AWS Lambda tries to reuse the execution context for subsequent invocations of the Lambda function. This is known as **cold start**.

After a Lambda function is executed, AWS Lambda maintains the execution context for some time in anticipation of another Lambda function invocation. In effect, the service freezes the execution context after a Lambda function completes, and thaws the context for reuse, if AWS Lambda chooses to reuse the context when the Lambda function is invoked again. This is known as **execution context reuse**. The execution context is kept **warm** 15mins after the end of an execution, before cold starting again. 

To keep your lambda warm, we can have a scheduled job in Cloudwatch to involve the API every 15mins. This setting is also available in tools like zappa & serverless. To keep multiples of the same lambdas always warm, we can set a lambda **provisioned concurrency setting**, but there will be an add-on charge.

**Objects declared outside of the function's handler method remain initialized, providing additional optimization when the function is invoked again**. For example, if your Lambda function establishes a database connection, instead of reestablishing the connection, the original connection is used in subsequent invocations. However, it is recommended to add logic in the code to check if a connection exists before creating one.

Each execution context provides 512 MB of additional disk space in the /tmp directory. The directory content remains when the execution context is frozen, providing transient cache that can be used for multiple invocations. You can add extra code to check if the cache has the data that you stored. For information on deployment limits, see AWS Lambda limits.


## Create Lambda

### Handler

In a python handler, it includes the **handler name** (function name), **event**, which is the information passing from the request, and **context**, which contains AWS specific invocations or execution of your lambda, e.g. memory, cognito identity details etc.

```python
def handler_name(event, context):
    # do something
    return something
```

### Zip libraries & handler

We will need to zip both python packages and the handler... [More](https://docs.aws.amazon.com/lambda/latest/dg/python-package-create.html)

```bash
# Download dependencies into folder
sudo pip install --target ./add-dragon-package boto3
# Zip up your code (with dependencies); zip file created yet
cd add-dragon-package
zip -r9 ${OLDPWD}/ pythonAddDragonFunction.zip .   
# Add python script to zip, zip file is generated at this stage
cd ..
zip -g pythonAddDragonFunction.zip addDragon.py
```

### Create Lambda

Then upload the zip file using either...

Using AWS CLI, or

```bash
# Create Lambda Function
aws lambda create-function --function-name add-dragon --runtime python3.6  --role <IAM ROLE ARN> --handler addDragon.addDragonToFile --publish --zip-file fileb://pythonAddDragonFunction.zip
# Invoke Lambda Function
aws lambda invoke --function-name add-dragon output.txt --payload file://newDragonPayload.json 
# Update Lambda Code
aws lambda update-function-code --function-name add-dragon --zip-file fileb://pythonAddDragonFunction.zip --publish
```
There are additional options to add on to the lambda's configuration when we are creating the function, otherwise they will be defaulted.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda0.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Using management console, to upload the zip file.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Adding and saving test requests.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda2_.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Attaching Lambda to API Gateway

When we have created the Lambda function, we can attached it to our API Gateway by clicking the Integration Request.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda-api-gateway1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

And selecting the relevant integration options.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda-api-gateway2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Basic Configs

Some important settings for lambda include the memory, which also determines the number of CPU, timeout, and execution roles.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Others include concurrency, which limits the number of lambdas that will be spun up at a given time, and environment variables, which your function can access.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Permissions

There are two types of permissions for lambda. The first is **execution permissions**, which defines what the lambda can do. This is set up in an IAM role.

The most basic policy is `AWSLambdaBasicExecutionRole`, which is allows permission to upload logs to CloudWatch. Some other lambda configured policies are included [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html).

The second type of permission is **resource permissions**, which defines what can invoke or manage your lambda functions. This is set by triggers.

## Triggers

Lambda functions can be invoked by the push or pull models.

For the push model, for example, someone can send a request to the API Gateway, which triggers the lambda to run. Alternatively, someone can upload a file to S3, and it triggers a lambda to process that file.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda3.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

For the pull model, for example, lambda will look for data in streaming or queue services like SQS, Kinesis, DynamoDB Streams, and trigger to pull the data into the function. This is configured through event source mappings.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/lambda4.png?raw=true" style="width:80%" />
  <figcaption></figcaption>
</figure>

## Version & Alias

You can publish a new **version** of your AWS Lambda function when you create new or update existing functions. Each version of a lambda function gets it’s own unique Amazon Resource Name (ARN). You can then use these ARNs to use different versions of the Lambda function for different purposes. You also have the ability to create **aliases** for AWS Lambda functions. Aliases are essentially pointers to one specific Lambda version.

