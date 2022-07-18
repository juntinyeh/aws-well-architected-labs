---
title: "Level 100: Custom Lenses on AWS Well-Architected Tool"
#menutitle: "Lab #2"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 2
hidden: false
---
## Authors
- Bob Yeh, Well-Architected Geo SA
- Ray Wang, Solutions Architect, Analytics SME 
- Cathy Lai, Database GTM Specialist, Database SME

## Introduction

The AWS Well-Architected Tool support [Custom lenses](https://docs.aws.amazon.com/wellarchitected/latest/userguide/lenses-custom.html) in Nov 2021, it provide a consolidated view and a consistent way to measure and improve your workloads on AWS without relying on external spreadsheets or third-party systems.
  
The purpose of this lab is to walk through the features of the [Custom lenses](https://docs.aws.amazon.com/wellarchitected/latest/userguide/lenses-custom.html) feature on AWS Well-Architected Tool. 

We take "Amazon DynamoDB Configuration Checks" to demostrate how exactly a domain-specific check list could be draft for a custom review, with self-defined pillar & questions structure.

## Goals:

* Learn the basic concept of building a custom lenses for domain-specific review.
* Learn where the Custom Lenses can be created/imported on Well-Architected Tool.
* Use the example custom lenses to understand the from difference between Well-Architected Framework Review and Custom Lenses Review.
* Innovate from the custom lenses and extend to automation for possible items.

## Prerequisites:

* An
[AWS Account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) that you are able to use for testing, that is not used for production or other purposes.
* An Identity and Access Management (IAM) user or federated credentials into that account that has permissions to use Well-Architected Tool (WellArchitectedConsoleFullAccess managed policy).

## Costs:
* There are no costs for this lab
* [AWS Pricing](https://aws.amazon.com/pricing/)

## Time to complete
- The lab should take approximately 30 minutes to complete 

## Steps:
{{% children /%}}

{{< prev_next_button link_next_url="./1_ddb_config_pillars_and_bps/" button_next_text="Start Lab" first_step="true" />}}
