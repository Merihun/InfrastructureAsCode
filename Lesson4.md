# Servers and Security Groups

# What is a Jumpbox?
These are the EC2 instances in the public subnet with required access to the private subnets' servers. Generally, we would not want our private servers to be discoverable by anyone outside the VPC. However, we want to access those private servers from the Internet. It is made possible by using a Jumpbox (also called as Bastion Host). It is important to note that the security group attached to the private servers must allow the IP address of the public Jumpbox to connect to it.


<img width="1056" alt="image" src="https://user-images.githubusercontent.com/26862785/168442112-a037fdf2-2af4-493c-8881-7d516d7c7cb2.png">

# Create a Jumpbox
Create a new key-pair, jumpbox-key.pem. However, you can use an existing key-pair if available. Remember that key-pairs are specific to an AWS region. Also, the VPC you have to choose while launching the Jumpbox must be the same one in which you have been creating Cloudformation stacks.
<img width="1181" alt="image" src="https://user-images.githubusercontent.com/26862785/168442185-bf80e4dc-e070-4b00-9658-63e36c14527c.png">


# Connect to the Jumpbox
Since the Jumpbox is a Linux machine, therefore you will have to use SSH protocol to connect to it. Remember that the flow of connection will be

Your local computer (Mac/Windows/Linux) → Jumpbox(CentOS Linux) → Private servers (Ubuntu Linux).

If you are running a Windows computer locally, then you would have to convert the jumpbox-key.pem to jumpbox-key.ppk using the PuTTy utility and use the same PuTTy to connect to the Jumpbox.
Test the Jumpbox
Recall that the instructor has the following two different login keys: 1). jumpbox-key.pem for the Jumpbox and 2). private-server-devops-key.pem for the private servers. Let's test if you are able to connect to the private servers via a Jumpbox:

Copy the public IP address of the Jumpbox, say 3.17.80.159
Copy and paste the private servers' login key file from your local computer to the Jumpbox. Run the following command from your local terminal (replace the file names and the IP address as applicable to you):
```
scp -i jumpbox-key.pem private-server-devops-key.pem ec2-user@3.17.80.159:/home/ec2-user/private-server-devops-key.pem
```
SSH login to the Jumpbox:
```
ssh ec2-user@3.17.80.159 -i jumpbox-key.pem
```
Copy the private IP address of any private server, say 10.0.2.74.
Once you are logged into the Jumpbox, confirm if you have the private-server-devops-key.pem key available in the home directory, and then change the access-mode of the key file. Later, try to SSH login to the private server:
ls
# you must see the private-server-devops-key.pem file]
```
chmod 400 private-server-devops-key.pem
ssh -i "private-server-devops-key.pem" ubuntu@10.0.2.74
```
Recall that the default user name for a Linux system is ec2-user and for an Ubuntu system is ubuntu.
Lastly, check the status of the running web server in the private instance, as shown in the snapshot below:
