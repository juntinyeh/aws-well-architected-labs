---
title: "200 - Anticipate failure and learn from operational failures"
## menutitle: "Lab #2"
date: 2020-11-08T10:21:08-04:00
chapter: false
weight: 1
hidden: false
---

## Authors
* **Bob Yeh**, Well-Architected Geo Solutions Architect.

## Contributors
* **Brian Carlson**, Well-Architected Operational Excellence Pillar Lead.
* **Nicolas Seilaz**, Senior Enterprise Solutions Architect.

## Introduction

In an architecture design, we want to keep the continuity of service to make sure it deliver highest business objective. That's how we usually describe the availability and reliability. Before we launch every deployment onto production environment for our external customer, a "pre-mortem" exercise to indentify and remove any potential source of failure will inprove the confidence to our operational objective. 

In this lab, we use standard 3-tier website as an example, and we practice the "pre-mortem" exericse with fault injection toward the application layer, the EC2 instance in autoscaling group. In different scenarios, we practice how the incident response with operational failure.

With the propose to anticipate failure, we choose typical case High CPU Utilization status as an example, which it will force application service uncapable to take any external request, and lead to service unavailable. Target the expected response action from our design, we expect our EC2 autoscaling group can scale out and add instance capacity to keep the service continuity.
To validate this mechanism, we inject a simulation event into the system and check if the expected response did take place. If response action not as expectation, then it is the potential point of failure, which need to be remediated immediately. To diagnose, we will first validate the simulation did take place from multiple observation angle, then check the responding mechanism is well configured. 

## Services 
* [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
* [AWS Fault Injection Simulator](https://docs.aws.amazon.com/fis/latest/userguide/what-is.html)
* [Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-automation.html)
* [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)

## Goals: 

* Anticipate failure - indentify potential source of failure
* Use Fault Injection Simulator to organize the predefined failure and experiment
* Simulate the unexpected incident and response for the incident
* Define and validate workload metrics of healthness

## Prerequisites:

* An [AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) that you are able to use for testing. The account should not be used for production purposes.  
* An [IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) in your AWS account with full access to [CloudFormation,](https://aws.amazon.com/cloudformation/) [Amazon EC2,](https://aws.amazon.com/ec2/)[Amazon RDS,](https://aws.amazon.com/rds/)[Amazon Virtual Private Cloud (VPC),](https://aws.amazon.com/vpc/) [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/).  

## Costs

{{% notice note %}}
NOTE: You will be billed for any applicable AWS resources used if you complete this lab that are not covered in the [AWS Free Tier](https://aws.amazon.com/free/).
{{% /notice %}}

## Steps:

{{% children  %}}


{{< prev_next_button link_next_url="./1_deploy_base_application_environment/" button_next_text="Start Lab" first_step="true" />}}

Steps:
{{% children  /%}}
