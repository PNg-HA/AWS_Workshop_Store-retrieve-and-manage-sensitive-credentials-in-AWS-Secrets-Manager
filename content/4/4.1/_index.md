---
title : "Review AWS Config Rules for Secrets Manager"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> Task-2.1: </b> "
---
Five Config rules for checking compliance for secrets stored in AWS Secrets Manager have already been created for this workshop:

1. secretsmanager-workshop-rotation-enabled-check
- Checks whether AWS Secrets Manager secret has rotation enabled.


2. secretsmanager-workshop-scheduled-rotation-success-check
- Checks whether AWS Secrets Manager secret rotation has rotated successfully as per the rotation schedule.


3. secretsmanager-workshop-using-cmk
- Checks if secrets are encrypted using an AWS KMS Customer Master Key (CMK).


4. secretsmanager-workshop-secret-unused
- Checks if Secrets Manager accessed secrets within a specified number of days.


5. secretsmanager-workshop-secret-periodic-rotation
- Checks if secrets have been rotated within the past specified number of days.


You can review the Config Rules by following these Steps:

1. Navigate to [Config Service console](https://console.aws.amazon.com/config).

2. Click "Rules" from the left panel.

3. Review the Config Rule details by clicking on the Rule name.