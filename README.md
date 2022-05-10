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
