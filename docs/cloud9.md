# Cloud9

[Cloud9](https://aws.amazon.com/cloud9/) is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cloud95.png?raw=true" style="width:100%" />
  <figcaption>Interface of Cloud9 IDE</figcaption>
</figure>

## Starting Cloud9

Cloud9 runs on an EC2 instance, and charges based on the instance type and storage. If we choose the cheapest `t2.micro`, AWS [estimates](https://aws.amazon.com/cloud9/pricing/) it to only be USD$2.05 per month. Free tier AWS (first year of account opening) has 750 free hours for EC2, so the costs should be either neligible or none at all. We should allow the cost saving settings to be on to prevent ballooning accidental costs.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cloud91.png?raw=true" style="width:80%" />
  <figcaption>Choosing EC2 instance type & cost savings setting when launching a Cloud9 instance</figcaption>
</figure>

To close Cloud9 IDE, we need to go to the EC2 instance to shutdown. To start the instance, we can just go to Cloud9 service in management console and open the IDE.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cloud92.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Credentials

By default, Cloud9 has temporary credentials that will refresh every 5 mins. These credentials are the same as the IAM role that was used to create this Cloud9 instance, so the permissions to AWS resources are the same.

To use a different credentials, we need to go to Cloud9 Settings > AWS Settings > Credentials > turn off AWS managed temporary credentials. Then in the terminal, `AWS Configure` & enter your other credentials.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cloud93.png?raw=true" style="width:100%" />
  <figcaption>Switching off Temp Credentials</figcaption>
</figure>


## File Uploads

We can upload files & access the settings from the Welcome page.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/cloud94.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>