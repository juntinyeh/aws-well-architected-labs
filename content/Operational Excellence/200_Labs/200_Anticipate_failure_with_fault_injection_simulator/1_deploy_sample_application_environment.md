---
title: "Deploy the sample application environment"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---

In this lab, you will use an EC2 autoscaling group with a Wordpress application running in a VPC. You will use the VPC stack from the lab Automated Deployment of VPC with the default parameters and the recommended stack name. 

### 1.1 Setup the VPC Stack

Please download the latest version of the CloudFormation template here: [vpc-alb-app-db.yaml](/Common/Create_VPC_Stack/Code/vpc-alb-app-db.yaml) and setup the VPC using the stack name **WebApp1-VPC**
or reference to [Create VPC Stack](/security/200_labs/200_automated_deployment_of_vpc/1_create_vpc_stack/)

### 1.2 Setup the Application Services Stack

1.  Use the latest version of the CloudFormation template and download it to your computer, or clone this repository: [200-ops-wordpress-fis.yaml](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Code/200-ops-wordpress-fis.yaml), this stack will create a WordPress site, with a provisioned RDS database and a pre-defined tag for the Fault Injection Simulation experiemnt.

    In order to have better alignment as you follow the steps, please use the stack name **WebApp1-Wordress** for the application.

2. Sign in to the AWS Management Console, select your preferred region and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/ . Note if your CloudFormation console does not look the same, you can enable the redesigned console by clicking New Console in the CloudFormation menu.

3. Click **Create Stack**, then **With new resources (standard)**.
 ![cloudformation-createstack-1](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session1-cloudformation-createstack-1.png)

4. Click **Upload a template file** and then click **Choose file**.
![cloudformation-createstack-2](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session1-cloudformation-createstack-2.png)

5. Choose the CloudFormation template you downloaded in [**Step 1.1**](#11-setup-the-vpc-stack), return to the CloudFormation console page and click Next.
Enter the following details:
Stack name: **WebApp1-WordPress**
![cloudformation-wp-params](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session1-cloudformation-wp-params.png)

6. Review the information for the stack. When you’re satisfied with the configuration, check I acknowledge that AWS CloudFormation might create IAM resources with custom names then click Create stack.
![cloudformation-wp-params](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session1-cloudformation-wp-createstack-final.png)

7. After the stack status has changed to **CREATE_COMPLETE**, you can find the *WebsiteURL* value from *Outputs tab* of Cloudformation console, this is how to access what you just created.
![cloudformation-wp-createstack-final](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session1-cloudformation-wp-createstack-complete.png)


## Congratulations! 

You have now completed the first section of the Lab.

Click on **Next Step** to continue to the next section.

{{< prev_next_button link_prev_url="..//" link_next_url="../2_deploy_aws_fis_stack/" />}}


