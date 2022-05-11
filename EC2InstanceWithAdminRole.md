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


# Configuring the AWS Command Line Interface (CLI)
Assuming you have already installed the AWS CLI tool and copied the access key for an administrator IAM user, follow the steps below:

Verify, if you already have a CLI v1 installed. If yes, prefer to uninstall CLI v1 and have CLI v2 installed, which is the latest one. You can verify the version using:
```
aws --version 
```
To set up your AWS CLI, type either of the following commands in the terminal:
```
aws configure
aws configure --profile default
```

Upon prompt:
Paste the copied access key (access key id and secret access key).
Enter the default region either as as us-east-1 or us-west-2, even if you’re living closer to another available region.
Enter the output format either as json or leave it blank
Verifying your Setup
Verify the successful configuration of the AWS CLI, by running any AWS command:

# List your S3 buckets. This will be blank if you have no S3 buckets
aws s3 ls
# List the IAM users in your account
aws iam list-users
The output of aws iam list-users command will display the details of the recently created user:


# Additional Access Keys
Note that each user can have up to 2 access keys at the same time.

# Why Making Keys Inactive is a Better Choice
You may make your access key temporarily inactive rather than destroying it and creating a new one. This may be helpful if you want to stop an automated process that uses that key (for example, a CI/CD process).
