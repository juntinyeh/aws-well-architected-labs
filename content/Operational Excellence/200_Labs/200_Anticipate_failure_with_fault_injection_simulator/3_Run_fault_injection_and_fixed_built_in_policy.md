---
title: "Simulate High CPU failure to Validate the Scaling Mechanism"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---


**AWS Fault Injection Simulator (AWS FIS)** provides visibility throughout every stage of an experiment via the console and APIs. As an experiment is running you can observe what actions have executed. After an experiment has completed you can see details on what actions were run, if stop conditions were triggered, how metrics compared to your expected steady state, and more. To support accurate operational metrics and effective troubleshooting, you can also identify what resources and APIs are affected by a Fault Injection Simulator experiment.

In [Step.2](../2_deploy_aws_fis_stack/) we had setup a FIS stack with an experiement template to make EC2 instances run into a high CPU utilization status. This scenario  simulates an incorrect application behaviour, malfunction, or external intent such as a denial of service. 

In [Step.1](../1_deploy_sample_application_environment/) you deployed a WordPress stack which has an EC2 instance running in an Auto-Scaling Group. The CPU-Burning experiment template  executes operating system commands to load the CPU, it is executed via AWS Systems Managers. This simulation is expected to cause CPU exhaustion.

### 3.1.Run experiment on high CPU failure

### Run through AWS Console

- Find the experiment template from AWS FIS console
- Check the template "**BurnMemoryViaSSM**", drag down the "**Actions**"
list, and click "**Start Experiment**"

![fis-start-experiment](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-fis-start-experiment.png)

- Enter the tag Key and Value to indicate the purpose for this experiment, set the values as Key=Name, Value=Burn CPU

![fis-set-experiment-tag](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-fis-set-experiment-tag.png)

- Click ***Start*** 
- Confirm in the dialog by typing ***start***


### Run through AWSCLI

- You can use the awscli to find the experiment template id by running
```
aws fis list-experiment-templates --region <REGION>
```
- TThe expected output will look similar to the below, ID and times will be different:
![fis-cli-list-experiment-templates](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-fis-cli-list-experiment-templates.png)

- Use the ***"id"*** value with following command, also ensure the correct ***REGION*** input.
```
aws fis start-experiment --experiment-template-id <TEMPLATE_ID> --region <REGION>
```
- You can see the FIS experiment is initiating from the terminal output:
![fis-cli-start-experiment-burn-cpu](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-fis-cli-start-experiment-burn-cpu.png)

### 3.2 Validate the responding actions 

We expect Fault Injection Simulation to cause all the running webapp EC2 instance into a high CPU utilization condition, from this condition we expect it to trigger the scaling mechanism to add capacity into autoscaling group. At this moment, our operational procedure will be:

 Check the response of Auto-Scaling Group

 1. Go to AutoScaling Group on EC2 service page

 2. Find the autoscaling group "**WepApp1**" and switch to "Activity Tab"

 3. Scorlliong down to "**Activity history**". Unfortunately you observe that no scaling activity has occured. 

 4. You switch to "Automatic scaling Tab" to check of there is a poloicy configuired to respond to the high CPU utilization. 
![fis-cli-start-experiment-burn-cpu](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-asg-has-no-policy.png)
 You note that there is no dynamic scaling policies, without this policy configured the autoscaling will not occur. 

 5. To resolve the autoscaling and correct the configuration, you click the button "Create dynamic scaling policy".
 Choose the **Policy Type** as "**Target tracking policy**"
    **Scaling policy name** as "**Target Tracking Policy**"
    **Metric type** as "**Average CPU Utilization**". 
    Input the **Target Value** as 50, and set **300** seconds warm up before including in metric. 
![asg-create-dynamic-target-tracking-policy](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-asg-create-dynamic-target-tracking-policy.png)

 8. Click the **Create** to create a scaling policy which reacting to future CPU exhaustion.

### 3.3 We launch a new experiment with same template and verify again.

 1. **As per the previous step, start the CPU experiment again**
 * Since the FIS experiment is launched as a Systems Managers Run Command on the target instances, you can check the Run Command History page in AWS Systems Managers for details. To navigate there, navigate to the System Manager service, from the left hand menu select ***run command*** then select in the main tab at the top the command history tab.
 * You will see that a Success record for our CPU stress process is displayed. 
 ![Validate the action from external](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-validate-action-external.png)
 2. **Validate the simulation action, in this experiments case, it was a high CPU event** 
 * You expect to see high CPU usage, for this you can leverage the the CloudWatch metrics of CPU utilization. 
 * Navigate to the EC2 service, then on the left hand menu select the AutoScaling Groups, find **WebApp1** and switch to **Monitoring** tab, select **EC2**, you can see the **CPU Utilization (Percent)** metrics.
 * As expected, the CPU is being consumed by the the experiment.
![Validate the action from internal](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-validate-action-internal.png)

 3. Select the Activity History Tab on Autoscaling Group "**WebApp1**". It shows an instance Scale-out event has occured, this was expected. 
![asg-create-dynamic-target-tracking-policy](/Operations/200_Anticipate_failure_with_fault_injection_simulator/Images/session3-asg-history-scale-out-high-cpu.png)

In terms of the experiment, you firstly identfied an incorrect behaviour when the experiment was first run, there was no scaling event that occured.  You where then able to take action to rectify the incorrect configuration, retest and you are now certain that the expected auto scaling is occuring.  You are now confident that your web site will be able to scale and remain avalaible when a high CPU event occurs. 

{{< prev_next_button link_prev_url="../2_deploy_aws_fis_stack/" link_next_url="../4_anticipate_failure_with_customized_cw_metrics/" />}}

 
