---
title: "Structure of a custom lenses - Pillars, Questions, and Best Practices"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---


### Prerequisites:

Read through [this blog](
https://aws.amazon.com/blogs/aws/well-architected-custom-lenses-internal-best-practices/)
, it has clear step-by-step instructions with following steps:
1. Download a JSON template from AWS Console - Well-Architected Tool.
2. Create and publish a Custom Lens.
3. Create a workload with Custom Lens. 

### Get Started:

In this lab, we will give a detail explaination on how to draft and create a custom lens hierarchically. All the custom lense should follow the JSON template, aligned with the structure of AWS Well-Architected Framework and Lenses. 
```
- Pillars
   +- Questions
        +- Choices
```

When we start to draft a custom lenses, the first thing to be considered is how many "pillars" will be covered by this custom lens. From the JSON template, you will can see a "pillars" as a major list, and each pillar will contains "questions". 

In the map hiearachy, each question will have elements like "choices" and "riskRules" which directly represent to each area of best practices we want to cover. 

```
{
    "schemaVersion": "2021-11-01",
    "name": "My Test Lens",
    "description": "This is a description of my test lens.",
    "pillars": [
        {
            "id": "pillar_red",
            "name": "Red Pillar",
            "questions": [
                {
                    "id": "pillar_1_q1",
                    "title": "How do you get started with this pillar?",
                    "description": "Optional description.",
                    "choices": [
                        {
                            "id": "choice1",
                            "title": "Best practice #1",
                            "helpfulResource": {
                                "displayText": "This is helpful text for the first choice.",
                                "url": "https://aws.amazon.com"
                            },
                            "improvementPlan": {
                                "displayText": "This is text that will be shown for improvement of this choice."
                            }
                        },
                        {
                            "id": "choice2",
                            "title": "Best practice #2",
                            ...
                        }
                    ],
                    "riskRules": [
                        {
                            "condition": "choice1 && choice2",
                            "risk": "NO_RISK"
                        },
                        {
                            "condition": "choice1 && !choice2",
                            "risk": "MEDIUM_RISK"
                        },
                        {
                            "condition": "default",
                            "risk": "HIGH_RISK"
                        }
                    ]
                }
            ]
            ...
        },
        ...
    ]
}
```

Take Amazon DynamoDB configuration as an example, we want to build a configuration standard review with following ***custom pillars***(example) :
* *Operating Readiness*
* *Security* 
* *Application Performance*
* *Cost Model Optimization* 

Then the JSON structure now will looks like this:
```
{
    "schemaVersion": "2021-11-01",
    "name": "My Test Lens for organization DynamoDB Check",
    "description": "This is a description of my test lens.",
    "pillars": [
        {
            "id": "pillar_oper",
            "name": "Operating Readiness",
            "questions": [
                {...
                    }
            ]
            ...
        },
        {
            "id": "pillar_security",
            "name": "Security",
            "questions": [
                {...
                    }
            ]
            ...
        },
        ...
    ]
}
```



{{< prev_next_button link_prev_url="../" link_next_url="../2_ddb_config_questions/" />}}
