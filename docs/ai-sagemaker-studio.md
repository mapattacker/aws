# Sagemaker Studio

Sagemaker Studio is a customized Jupyter Lab server, a full fledged python IDE with integrated AWS MLOps platform inside for training, experiments tracking, and deployment.

## Create New Studio User

At AWS Sagemaker
 * Open Sagemaker Studio
 * Add User
 * Input user name with sagemaker execution role
 * After user is created, click launch app > Studio

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/sm-studio-create.png?raw=true" style="width:100%" />
  <figcaption>Created Users</figcaption>
</figure>

## Cloning a Git Repository

To link to an external Git repository, we will need to create an SSH Key.

Open a Terminal at File > New > Terminal > `ssh-keygen`. Get the public key using `cat ~/.ssh/id_rsa.pub` and save it to your git user settings.

You should be able to git clone and push to your repository now.


## Understanding the Various Servers

Studio is installed in an Amazon Linux 1 server, which uses `yum` as package manager. It appears to be a slim down linux, and there were some libraries which were unable to be installed there. When they upgrade it to Amazon Linux 2, it should be better I think.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/sm-studio-server.jpg?raw=true" style="width:100%" />
  <figcaption>Various server types in Studio</figcaption>
</figure>

In Studio we can also create a jupyter notebook. This notebook is launched in an instance of its own (we can choose the type), and have additional costs. The server uses debian, with `apt` as the package manager. We have to remember to manually shutdown the server from the left panel.

Both Studio and Notebook servers are attached to an EFS, and your data and scripts you see in the explorer panel are saved there.

<figure>
  <img src="https://github.com/mapattacker/aws/blob/master/images/sm-studio-jupyter.png?raw=true" style="width:100%" />
  <figcaption>Various server types in Studio</figcaption>
</figure>

When we launch a training or deployment job, they are launched in a separate instance again, using the Ubuntu Server. For training, the servers will be shutdown when training ends, while you will need to delete the endpoint to shutdown that server.
