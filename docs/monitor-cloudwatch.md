# Cloudwatch

## Metrics

**Metrics** are data about the performance of your systems. By default, many services provide free metrics called **basic monitoring** for resources (such as Amazon EC2 instances, Amazon EBS volumes, and Amazon RDS DB instances). You can also enable **detailed monitoring** for some resources, such as your Amazon EC2 instances, or publish your own application metrics.

## Logs

CloudWatch **Logs** allows us to monitor, store, and access your log files from Amazon Elastic Compute Cloud (Amazon EC2) instances, AWS CloudTrail, Route 53, and other sources. 

Some services are set up to send log data to CloudWatch Logs with minimal effort like Lambda. All we need to do is to give the Lambda function the correct IAM permissions to post logs to CloudWatch Logs. 

Other services like EC2 and even on-premise servers requires more effort. We have to first install and configure the **CloudWatch Logs agent** in the instance.

Some logging terminology are as follows.

**Log event**: A log event is a record of activity recorded by the application or resource being monitored, and it has a timestamp and an event message.

**Log stream**: Log events are then grouped into log streams, which are sequences of log events that all belong to the same resource being monitored. For example, logs for an EC2 instance are grouped together into a log stream that you can then filter or query for insights.

**Log groups**: Log streams are then organized into log groups. A log group is composed of log streams that all share the same retention and permissions settings. For example, if you have multiple EC2 instances hosting your application and you are sending application log data to CloudWatch Logs, you can group the log streams from each instance into one log group. This helps keep your logs organized.

## Dashboards

We can display metrics or logs as charts in a unified dashboard for easy monitoring of our resources.

## Alarms

We can set cloudwatch alarms when a metric exceeds a certain threshold for a period of time.

An alarm has three possible states.

 * **OK**: The metric is within the defined threshold. Everything appears to be operating like normal.
 * **ALARM**: The metric is outside of the defined threshold. This could be an operational issue.
 * **INSUFFICIENT_DATA**: The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state.

**Billing**

You can set billing alerts in Cloudwatch by following this [resource](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html). Note that billing metric data is stored in the US East (N. Virginia) Region and represents worldwide charges.