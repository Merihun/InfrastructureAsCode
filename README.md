# Infrastructure As Code (IAC) - Cloud DevOps Engineer - Udacity 
Deploy Infrastructure as code(IAC)
# What is (Cloud) Infrastructure?
Cloud services are broadly categorized as Software as a Service (SaaS), Platform as a Service (PaaS), or Infrastructure as a Service (IaaS). Cloud is a collection of geographically distributed data centers that are logically grouped into regions and availability-zones.

The IaaS allows a user to provision Virtual Machines (VMs), set up networks (VPC), create subnets, and associate necessary security features. Further, VMs can be attached to storage volumes, different networks, or servers. All the resources mentioned above are referred to as Infrastructure.
<img width="1141" alt="image" src="https://user-images.githubusercontent.com/26862785/167639338-d7b40563-b20a-4c03-a15f-ed5765c82b46.png">

# Issues that DevOps tries to solve:
Unpredictable deployments
Mismatched environments (development doesn’t match production)
Configuration Drift

# DevOps best practices and tools
One of the benefits of using DevOps is that it allows predictable deployments using automated scripts. In the DevOps model, development and operations teams are merged into a single team. These DevOps teams use a few tools and best practices that deploy and manage configuration changes to servers.

# The most important practices are:

Continuous Integration / Continuous Delivery (CI/CD) - new features are automatically deployed with all the required dependencies.
Infrastructure as Code (IaaC) - configuration and management of cloud infrastructure using re-usable scripts.
Other prevalent practices are:

Microservices
Monitoring and Logging
Communication and Collaboration

# Continuous Integration Continuous Deployment (CI/CD): 
Tracks the development workflow from testing through production. Continuous integration is the process flow of testing any change made to your development flow, while continuous deployment tracks those changes through to staging and production systems. 

# Infrastructure as code (IaC): 
Provision and manages the cloud-infrastructure by using scripts. These scripts can be written in YAML or JSON format. These scripts ensure that the same architecture can be re-built multiple numbers of times. These scripts are particularly useful in enterprise applications and different environments - dev, prod, or test.

# What is CloudFormation?
CloudFormation is an AWS tool for creating, managing, configuring, and deploying cloud resources. This tool is beneficial if you have to provision a set of cloud resources multiple times, at scale. You can do so by simply writing (YAML or JSON) scripts that you can easily edit and run numerous times. In the script, we mention each resource's necessary configuration that we want to provision and then use the AWS CLI tool and commands to execute the scripts.

# Configuring the AWS Command Line Interface (CLI)
Verify, if you already have a CLI v1 installed. If yes, prefer to uninstall CLI v1 and have CLI v2 installed, which is the latest one. You can verify the version using:
  aws --version
To set up your AWS CLI, type either of the following commands in the terminal:
  aws configure
  aws configure --profile default
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

# CloudFormation
CloudFormation allows you to create and manage Amazon Web Services infrastructure deployments predictably and repeatedly. You can use CloudFormation to leverage Amazon Web Services products, such as Amazon Elastic Compute Cloud, Amazon Elastic Block Store, Amazon Simple Notification Service, Elastic Load Balancing, and Auto Scaling to build highly reliable, highly scalable, cost-effective applications without creating or configuring the underlying Amazon Web Services infrastructure.
With CloudFormation, you declare all your resources and dependencies in a template file. The template defines a collection of resources as a single unit called a stack. CloudFormation creates and deletes all member resources of the stack together and manages all dependencies between the resources for you.

CloudFormation is a declarative language, not an imperative language.
CloudFormation handles resource dependencies so that you don’t have to specify which resource to start up before another. There are cases where you can specify that a resource depends on another resource, but ideally, you’ll let CloudFormation take care of dependencies.
VPC is the smallest unit of resource.

Declarative languages: These languages specify what you want, without requiring you to specify how to get it. An example of a popular declarative language is SQL.
Imperative languages: These languages use statements to change the state of the program. 
Imperative programming focuses on describing how a program operates step by step, rather than on high-level descriptions of its expected results.Procedural programming is a type of imperative programming in which the program is built from one or more procedures (also termed subroutines or functions). Structured programming and modular programming in general have been promoted as techniques to improve the maintainability and overall quality of imperative programs. The concepts behind object-oriented programming attempt to extend this approach.

# Create stack
Create the template file: Use the following code for your first test file: testcfn.yml (or choose any other name). Be careful about the indentation while you paste/write the same code in your editor.
```
AWSTemplateFormatVersion: 2010-09-09
Description: Carlos Rivas / Udacity - This template deploys a VPC
Resources:
UdacityVPC:
  Type: 'AWS::EC2::VPC'
  Properties:
    CidrBlock: 10.0.0.0/16
    EnableDnsHostnames: 'true'
    Tags:
    - Key: name
      Value: myfirsttestvpc
```
Run the aws command : Run the following command in the terminal, from the same directory where you've placed your testcfn.yml file. We are assuming that your stack name is myFirstTest (or choose any other name).

``` 
aws cloudformation create-stack  --stack-name myFirstTest --region us-east-1 --template-body file://testcfn.yml
```
Alternate method - Shell Script: You can write a shell script (.sh) file as:
```
aws cloudformation create-stack --stack-name $1 --template-body file://$2  --parameters file://$3 --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM" --region=us-west-2
```
where $1, $2, and $3 can be replaced with the actual values passed as command-line arguments. Note the --parameters and --capabilities options that we will learn in the upcoming lesson.

# How to execute the Shell scripts?
You can run either of the shell scripts (create.sh or update.sh) as:
```
./<file_name> argument_1 argument_2 argument_3
```
For example, you can run the following command:
```
./create.sh ourdemoinfra ourinfra.yml ourinfra.json

```


Alternate method - Batch Script You can also try a batch script (.bat) with a similar syntax, except that the actual values can be written as %1 instead as$1.

# Update stack
You may also want to use update-stack when you want to update an existing stack instead of destroying your stack and creating a new one. The syntax is similar to before:
```
aws cloudformation update-stack  --stack-name myFirstTest --region us-east-1 --template-body file://testcfn.yml
```
The command above will update the existing stack based on the YAML script you've written.

# Describe stack
Once a stack is created successfully, you can verify by either going to the web console or running the following command, which will display all the details the stack.
```
aws cloudformation describe-stacks --stack-name myFirstTest
```
# To delete a stack

The following delete-stack example deletes the specified stack.
```
aws cloudformation delete-stack \
    --stack-name my-stack
```
This command produces no output.
You can describe the details of multiple stacks in one command. If no stack name is specified, then it will return the description for all the stacks created in your account.
