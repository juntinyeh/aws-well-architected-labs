---
title: "Structure of a custom lenses - Risk and Rule"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---


### Choices and Risk Logic:

In previous step we already setup a question, also the available choices for it. After we collected all the necessary resource like developer guide or blog posts, the next step is to create a logical rule - to indicate the risk level if recommended best practices was not applied.

Thus, we list out all the available choices we defined in previous step, and fill in the risk level we want the operating team to be awared. 

#### Rule Collections

Reference to [Custom Lenses Format Specification](https://docs.aws.amazon.com/wellarchitected/latest/userguide/lenses-format-specification.html), we can see all the RiskRule are combinations of "choice id" and operators - Here we need to make sure there is no duplication among choice id, and define the risk level for each option respectively.


||Choice|Risk Level if not applied.|Choices[]["id"]|
| ----------- | ----------- | ----------- | ----------- |
|1|`Manually trigger Amazon DynamoDB Backup process`|High|ddbops1_1|
|2|`Enable Amazon DynamoDB PITR Feature`|Medium, if covered by other backup process.|ddbops1_2|
|3|`Use AWS Backup for Amazon DynamoDB tabls`|Medium, if covered by other backup process.|ddbops1_3|
|4|`Export DynamoDB to other storage media`|Medium, if covered by other backup process.|ddbops1_4|
|5|`None of Above`|High|ddbops1_5|

#### Rule Conditions:

Now, to create a logical rule for this question:

* If the rule require every choice must to be applied, then the condition rule will include 4 options been selected for **"NO_RISK"** as result. In this case the operator **"&&"** will be applied.

```
	{	
     "condition":"ddbops1_1 && ddbops1_2 && ddbops1_3 && ddbops1_4",
     "risk":"NO_RISK"
     }
```

* Or we can set as if any of the choices been applied, it can be seen as no risk, then the condition rule will looks like this.

```
	{	
     "condition":"ddbops1_1 || ddbops1_2 || ddbops1_3 || ddbops1_4",
     "risk":"NO_RISK"
     }
```

* When we want to put some rule into higher priority, use the "OR" operator will cover border condition. 

If the "None of Above" (ddbops1_5) was checked, or one specific choice should be aligned, then we should setup the condition to raise "HIGH_RISK".

```

	{ 
	"condition":"(!ddbops1_1) || ddbops1_5",
    "risk":"HIGH_RISK"
	}
```
#### Aggregate into a rule set


```
               "riskRules":[
                  {
                     "condition":"ddbops1_1 && ddbops1_2 && ddbops1_3 && ddbops1_4",
                     "risk":"NO_RISK"
                  },
                  {
                     "condition":"(!ddbops1_1) || ddbops1_5",
                     "risk":"HIGH_RISK"
                  },
                  {
                     "condition":"default",
                     "risk":"MEDIUM_RISK"
                  }
               ]

```


{{< prev_next_button link_prev_url="../2_ddb_config_questions/" link_next_url="../4_ddb_config_publish/" />}}
