# EC2 Instance With Admin Role
Brief Introduction
You will create an EC2 Instance based on Amazon Linux AMI that you can connect via SSH. While provisioning the instance, you will make sure to limit access to your IP address only, using Security Groups. The instance will already have the CLI installed by default. You just need to assign permissions to this instance.

Once the instance is running, create an IAM role with admin access to your account. Then, attach the role to your EC2. In this case, the CLI tool will pick up the credentials from the role and won’t need hard-coded credentials.

# Exercise objectives

Launch a secure EC2 instance
Create IAM role with admin privileges
Attach the IAM role to the EC2 instance created earlier
Connect to your EC2 instance via SSH
Use CLI tool in the EC2 instance
