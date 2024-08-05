---
title : "Test Secret CMK Compliance"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> Task-2.5: </b> "
---


#### Steps:

1. Navigate to [Secrets Manager Service console](https://console.aws.amazon.com/secretsmanager).



2. Click on the secret that was created by the CloudFormation template deployed in Module-0. The secret name will be “DemoWorkshopSecret“.



3. In the “Secret details” section, click “Edit encryption key” from the drop down “Actions” menu:



4. Select “aws/secretsmanager”.



5. Uncheck “Create new version of secret with new encryption key” option.

**NOTE: For the demonstration purposes during this workshop, this option is not selected. This is NOT a security best practice for a production environment. In a production environment, it is recommended that you select this option for creating new version of secret with new encryption key.**


6. Click “Save”. You will see a green banner on top of the screen indicating a successful update.



7. Now revert back to the Encryption Key to the CMK with alias “AWSSecretsManagerWorkshopKey”. This CMK was created by the CloudFormation template in module-0.



8. Uncheck “Create new version of secret with new encryption key” option.


9. Click “Save”. You will see a green banner on top of the screen indicating a successful update.



*Wait for a few minutes and notice the messages in the SNS Portal.*
