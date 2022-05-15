# Storage and Databases

# Lesson Objectives
In this lesson, you will learn to utilize the following two different types of AWS storage options for a web application architecture:

Relation Database Storage (RDS) service
Object storage service - Simple Storage Service (S3)

# Persisting Data
Most applications need their data to persist and not be lost, which requires a database.
We don't want a database to be a single point of failure, so we'll use resources that are designed for reliability. For example, RDS for the database, and S3 for the filestore.
Relational Database Service (RDS): AWS service for creating databases.
# Choosing a database
AWS Aurora and MySQL have no additional licensing costs. Microsoft SQL Server will have additional licensing costs.


# S3 bucket
Choose a DNS compliant name for the S3 bucket.
Command line arguments
```
aws s3 ls <link to S3 bucket>
```
This line above lists files in the S3 bucket.

```
aws s3 cp <file name> <link to S3 bucket>  
```
Exmaple: Assume you have a bucket named 'merihunbucket' and a file named AWSWebApp.jpeg on your local machine.

```
aws s3 cp AWSWebApp.jpeg s3://merihunbucket
```

This line above copies a file from your local machine to the S3 bucket.

## Versioning
You can keep past versions of your S3 bucket, which means that deleted files will still exist in prior versions of your S3 bucket.

# Key Points
S3 can be used to store your config files, media or log files.
Your servers don't need credentials to access S3 provided they have a role assigned.
We recommend you choose RDS as opposed to installing a database in your own servers that you have to manage and back up yourself.

# Exercise 1
Deploy a MySQL database
Create a CloudFormation script that deploys a MySQL DB with an associated security group.

<img width="797" alt="image" src="https://user-images.githubusercontent.com/26862785/168476115-39efc49a-2e52-4a69-82ee-88393e930c5e.png">

## Bonus Steps
Export a few resources, such as private Subnet IDs, from your previous stack. Then only you can cross-reference the resources from another stack, such as using:
```
Fn::ImportValue: <Exported_value>
```
Use parameters from a separate file to make your template script reusable. In your new template file, use the substitution function, !Sub "${parameter} to refer to any parameter variable.

# Solution
To create a database in CloudFormation, you'll need
A Subnet group created, a Security Group that will control access in and out of your database.
A user name and a password that will serve as the master for this db server. These should be the parameters in your script.
You'll also need subnets, ideally 2.

# Best Practice
Add DeletionPolicy and set it to Retain at the bottom of your DB Creation script. This way you don't lose your database if you accidentally delete your stack. (Keep this in mind if you indeed intend to delete this DB when done practicing)


Best github repo for this complete lessons.
https://github.com/udacity/nd9991-c2-Infrastructure-as-Code-v1-Exercises_Solution

Final solution:
https://github.com/mehmetincefidan/Deploy-a-High-Availability-Web-App-Using-CloudFormation

