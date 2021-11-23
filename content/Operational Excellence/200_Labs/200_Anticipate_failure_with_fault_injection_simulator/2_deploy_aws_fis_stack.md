---
title: "Deploy AWS Fault Injection Simulator Stack"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---

AWS Fault Injection Simulator is a fully managed service, using the service you can setup experiments that introduce faults or degraded conditions into a system, application or component, doing this helps you to understand how that system, component or application behaves when under that fault event. Using outcome from the fault experiment you are able to better understand your applications, component or system, make changes or consider alternatives options to avoid that impact as an example. In this section of the lab, you will deploy the AWS Fault Injection Simulator following the below steps, these includes the experiment templates with preset resource target. 

### 2.1 Setup FIS Stack

1. Using this version of the CloudFormation template you can download it to your computer, or by cloning this repository: [200-fis-experiment-templates.yaml](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Code/200-fis-experiment-templates.yaml) to create a AWS FIS stack, which includes the 2 experiment templates.

2. Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/ . Note if your CloudFormation console does not look the same, you can enable the redesigned console by clicking New Console in the CloudFormation menu.

3. Click Create Stack, then With new resources (standard). And we setup the stack name with **WebApp1-FIS**

4. After stack's status changes to CREATE_COMPLETE, if you navigate to the *Resources Tab*, you will find the experiment templates show, there will be two of them 
![cloudformation-fist-stack-resource-output](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session2-cloudformation-fis-stack-resource-output.png)

5. Navigate to the AWS Fault Injection Simulator, 
from the left hand side click the "Experiment templates" you will then find the predefined failure simulation experiment templates as created by the Cloudformation. 
![aws-fault-injection-simulator-experiment-templates](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session2-aws-fis-experiment-templates.png)

6. Click the link of the experiment template and review the details of each experiment. Using the "BurnCPUViaSSM" as an example, you can see this template has assigned an action through Amazon Systems Managers (SSM) to run a CPU Stress command against the instances that are listed in the targets tab.
![aws-fault-injection-simulator-experiment-templates-actions](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session2-aws-fis-experiment-templates-actions.png)

7. Switch to *Targets Tab* note the target are filtered. The targets shown are only those EC2 instances where the resource tag "**Name**" has "**WebApp1**" assigned. 
![aws-fault-injection-simulator-experiment-templates-targets](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session2-aws-fis-experiment-templates-targets.png)

Now you have your Fault Injection Simulator stack ready for the **Next Step**.


{{< prev_next_button link_prev_url="../1_deploy_sample_application_environment/" link_next_url="../3_build_run_investigative_playbook/" />}}

