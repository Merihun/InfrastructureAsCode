# Challenge 1 - Create an EC2 instance in a given VPC

# ToDo
Write a CloudFormation script that will create the following two Resources: AWS::EC2::SecurityGroup and AWS::EC2::Instance. See the snapshot below as a starter point.

You will have to write the suitable properties for each resource. Inside one of the properties' fields, you will have to specify the VPC and Subnet ID. Details of the resource to create are:

1. AWS::EC2::SecurityGroup
Creates a Security Group which only allows inbound access on TCP port 80 and also allows unrestricted outbound access. Refer to the documentation to check which properties you want to use.

2. AWS::EC2::Instance
In the same CloudFormation script: create a resource that deploys an EC2 Server and associate its network interface with the security group mentioned above. Use the following properties:

The instance type will be t3.micro.
You will need the AMI ID of the base Amazon Linux 2 AMI (HVM), SSD Volume Type, on top of which we’ll install our web server software. To get this ID, go to the EC2 web console and click on Launch Instance. Since we’ll be launching a t3.micro instance, be sure to copy the AMI Id that says 64-bit x86 next to it.

Your EC2 resource’s networking interface will need this property set to true: AssociatePublicIpAddress. It ensures that your server gets assigned a public IP address that you can reach over the internet to verify it’s working correctly.
Script to run: We want a script to run automatically at the time of provisioning of the EC2 instance. In the UserData section of this EC2 server, you will deploy the Apache Web Server software that we can then use to verify that the machine correctly deployed. Use the following UserData script for your EC2 CloudFormation Resource:

```
     UserData:
       Fn::Base64: !Sub |
         #!/bin/bash
         sudo yum update -y
         sudo yum install -y httpd
         sudo systemctl start httpd
         sudo systemctl enable httpd

```
The script above installs, and start the Apache Web Server in the new EC2 instance. Also, it will enable this service to start automatically after reboot.
Bonus points: Write your script to use parameters for the Subnet, VPC and AMI! This will make the script easier to maintain in the future and easier to move to other AWS Regions or accounts.

Expected Output
To verify, you will use the public IP address of the newly launched EC2 instance, and paste it in a new browser window. You should see the Apache web server test page.

# Solution
```
aws cloudformation create-stack  --stack-name challenge1 --region us-east-1 --template-body file://challenge1.yml --parameters file://challenge1-parameters.json

```
# template (name it challenge1)
```
Parameters:
  myVPC:
      Description: VPC used to deploy our resources below
      Type: AWS::EC2::VPC::Id
  PublicSubnet:
      Description: Subnet to be used for our Web Server
      Type: AWS::EC2::Subnet::Id
  AMItoUse:
      Description: AMI to use for our base image
      Type: String
Resources:
  myWebAccessSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
        GroupDescription: Allow http to our test host
        VpcId:
          Ref: myVPC
        SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        SecurityGroupEgress:
        - IpProtocol: -1
          FromPort: -1
          ToPort: -1
          CidrIp: 0.0.0.0/0
  myWebServerInstance: 
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t3.micro
      ImageId: !Ref AMItoUse
      NetworkInterfaces: 
        - AssociatePublicIpAddress: "true"
          DeviceIndex: "0"
          GroupSet: 
            - Ref: "myWebAccessSecurityGroup"
          SubnetId: 
            Ref: "PublicSubnet"
      UserData:
        Fn::Base64: !Sub |
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd
```
# parameter file (name it challenge1-parameters.json)

```
[
  {
    "ParameterKey": "myVPC",
    "ParameterValue": "vpc-01a24c50e054d5fc8"
  },
  {
    "ParameterKey": "PublicSubnet",
    "ParameterValue": "subnet-0a650d9fba9cc1084"
  },
  {
    "ParameterKey": "AMItoUse",
    "ParameterValue": "ami-047a51fa27710816e"
  }
]
```

# Challenge 2

# Project Overview
You have been tasked with creating the required Infrastructure-as-code scripts for a new cloud environment in AWS. The Lead Solutions Architect for the project sends you the following diagram.
<img width="1122" alt="image" src="https://user-images.githubusercontent.com/26862785/168165394-7c0b4f62-3a9a-4255-aff9-39b7f4848e10.png">

# ToDo
Write a CloudFormation script that:
<li>
Creates a VPC<br><li>
It will accept the IP Range -also known as CIDR block- from an input parameter<br><li>
Creates and attaches an Internet Gateway to the VPC<br><li>
Creates Two Subnets within the VPC with Name Tags to call them “Public” and “Private”<br><li>
These will also need input parameters for their ranges, just like the VPC.<br><li>
The Subnet called “Public” needs to have a NAT Gateway deployed in it<br><li>
This will require you to allocate an Elastic IP that you can then use to assign it to the NAT Gateway.<br><li>
The Public Subnet needs to have the MapPublicIpOnLaunch property set to true. Use this reference for help.<br><li>
The Private Subnet needs to have the MapPublicIpOnLaunch property set to false.<br><li>
Both subnets need to be /24 in size.<br><li>
If you need assistance with IP math, you can use a subnet calculator such as this one.<br><li>
You will need 2 Routing Tables, one named Public and the other one Private<br><li>
Assign the Public and Private Subnets to their corresponding Routing table<br><li>
Create a Route in the Public Route Table to send default traffic ( 0.0.0.0/0 ) to the Internet Gateway you created<br><li>
Create a Route in the Private Route Table to send default traffic ( 0.0.0.0/0 ) to the NAT Gateway<br><li>
Finally, once you execute this CloudFormation script, you should be able to delete it and create it again, over and over in a predictable and repeatable manner, this is the true verification of working Infrastructure-as-Code<br>
# Helpful hints:
     
# Helpful hints:
     
The numbers in the diagram below show the recommended sequence for resource creation. This is not required by CloudFormation but it helps to keep you on track and allows you to stop and verify as you go.
<img width="1047" alt="image" src="https://user-images.githubusercontent.com/26862785/168167228-5f27b2e2-96a4-43e6-9db3-4d312932a737.png">
