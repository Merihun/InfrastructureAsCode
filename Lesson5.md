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

Versioning
You can keep past versions of your S3 bucket, which means that deleted files will still exist in prior versions of your S3 bucket.
