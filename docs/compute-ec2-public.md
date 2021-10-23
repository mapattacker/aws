# Launch Flask in EC2

## Launch a new EC2 instance

First we go to the EC2 instance page in the console, and click Launch Instances.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public1.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

This will divert you to the steps to launch an instance, first by choosing an Amazon Machine Image (AMI). For me, I prefer Ubuntu, hence I seleted Ubuntu 18.04 image.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public2.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Then we can choose the instance type, where I choose t2.micro, which is eligible to free tier.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public3.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

There are other configurations we can specify, but if we choose to accept defaults, we can just choose Review and Launch.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public4.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

A popup will appear asking you to create or use a key-pair. This allows you to SSH into the instance later on. After you created it, you can download a `.pem` file to your local machine.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public5.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

After this, you will be led to the EC2 instance page, and you can see that the instance is being initalized.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public6.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

## Allocate an Elastic IP

Before we go further, we need to understand that the public IP address of the instance will change whenever you stop-start the instance. To fix an IP address, we need to assign an Elastic IP to it.

First, we will need to create an Elastic IP. Go to Network & Security > Elastic IP. And click Allocate Elastic IP.

After it is created, click Actions > Associate Elastic IP > choose the EC2 instance you setup. You may choose to name your Elastic IP so that it is easier to identify it with your EC2 instance or project.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public7.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Note that Elastic IPs are free ONLY if they are associated with an EC2 instance.

## SSH into EC2

Before we can SSH into our newly created EC2 instance, we need to reduce the permissions of our pem file.

```bash
chmod 600 testing.pem
```

Then we can SSH in using the following command. Note that the public-ip is now the elastic IP. As we are using ubuntu, the computer name will be as such.

```bash
ssh -i testing.pem ubuntu@<public-ip>
```

Once in the EC2 instance, you may want to update any security patches with the following.

```bash
sudo apt-get update
```

## Create & Launch Flask app

We first install pip3 and then flask.

Then we can create an `app.py` script with the following contents, and then launch it with `python3 app.py`. The flask app now runs!

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Web App with Python Flask!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

## Enable Port Access to Internet

To enable internet access, we need to open the port `5000`. We only need to define inbound rules as security groups are stateful. Note that by default ports are `80 (HTTP)` and `443 (HTTPS)` though, but we do not need them for this use case.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public8.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>

Now we can test from our browser that we can view our flask app, using the address `http://<public-ip>:5000`.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public9.png?raw=true" style="width:50%" />
  <figcaption></figcaption>
</figure>

## Close EC2

To prevent incurring charges, let's close our instance.


<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/ec2-public10.png?raw=true" style="width:100%" />
  <figcaption></figcaption>
</figure>