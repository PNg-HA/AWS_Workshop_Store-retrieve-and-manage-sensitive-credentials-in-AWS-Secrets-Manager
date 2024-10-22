---
title : "Review AWS Config Rules for Secrets Manager"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> Task-2.1: </b> "
---

You can review the Config Rules by following these Steps:

1. Navigate to [Config Service console](https://console.aws.amazon.com/config).
![m2](/images/m2/2.1/Picture1.png)
2. Click "Rules" from the left panel.
![m2](/images/m2/2.1/Picture2.png)
3. Review the Config Rule details by clicking on the Rule name.

Five Config rules for checking compliance for secrets stored in AWS Secrets Manager have already been created for this workshop:

1. secretsmanager-workshop-rotation-enabled-check
- Checks whether AWS Secrets Manager secret has rotation enabled.
![m2](/images/m2/2.1/s1.png)

{{% notice warning %}}
From rule 2 to 5, the resources haven't loaded yet. So you can look up to the Rules list in step 2 above to see the rule compliance status.
{{% /notice %}} 

2. secretsmanager-workshop-scheduled-rotation-success-check
- Checks whether AWS Secrets Manager secret rotation has rotated successfully as per the rotation schedule.
![m2](/images/m2/2.1/s2.png)

3. secretsmanager-workshop-using-cmk
- Checks if secrets are encrypted using an AWS KMS Customer Master Key (CMK).
![m2](/images/m2/2.1/s3.png)

4. secretsmanager-workshop-secret-unused
- Checks if Secrets Manager accessed secrets within a specified number of days.
![m2](/images/m2/2.1/s4.png)

5. secretsmanager-workshop-secret-periodic-rotation
- Checks if secrets have been rotated within the past specified number of days.
![m2](/images/m2/2.1/s5.png)
