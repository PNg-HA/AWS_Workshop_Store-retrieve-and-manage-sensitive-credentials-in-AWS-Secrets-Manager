---
title : "Enable Secret Rotation"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> Task-2.4: </b> "
---

Before you enable Secret rotation:

1. Access the sample application API URL in a separate browser tab. You can find the API URL in your Event Engine dashboard. Note the value of the Version IDs for the labels AWSPREVIOUS and AWSCURRENT. Secrets Manager labels the currently active and in-use version of the secret with AWSCURRENT. Any time the label AWSCURRENT moves from one version to another, Secrets Manager automatically moves the staging label AWSPREVIOUS to the version previously labeled AWSCURRENT. To read more about how AWS Secrets Manager rotates secret, refer to the documentation [here](https://docs.aws.amazon.com/secretsmanager/latest/userguide/terms-concepts.html#term_rotation).



2. Access the SNS notification receiving portal in a separate browser tab. To access the portal, just append snsportal at the end of your API URL link. **As an example**:


Do not close the SNS portal browser tab until the end of the workshop. You will use it to view the SNS notification messages.

**Then Enable the Secret Rotation using following steps:**

1. Navigate to [Secrets Manager Service console](https://console.aws.amazon.com/secretsmanager).


2. Click on the secret that was created by the CloudFormation template. The secret name will be “DemoWorkshopSecret“.


3. In the “Rotation configuration” section, click “Edit rotation”.


4. Toggle “Automatic rotation”.



5. Under “Rotation schedule”, enter the number of days this secret will be rotated. e.g. 30 days.



6. Under “Rotation function”, choose the function named “SecretsManagerMySQLRotationLambda”.



7. Click “Save”.



8. At this point, you should see Green Banner on the top of the screen stating “Rotating your secret DemoWorkshopSecret”

*Wait for a few minutes and notice the messages in the SNS Portal.*

Access the sample application API URL again and observe the value of the Version IDs AWSPREVIOUS and AWSCURRENT.

Note that the AWSCURRENT version becomes the AWSPREVIOUS version.

You can also test application when the secret is scheduled for rotation by clicking “Rotate secret immediately”. Then access the application ApiUrl link after you see the Green success banner on the top of the screen.

Test rotation now:
.a
Still fail:
.b
Debug: Find out I have chosen the wrong event type:
.c
After changing the key to AWSSecretsManagerWorkshopKey:
,d

Lambda writes log into DynamoDB table:
.e
.f

Access the URL. Now the AWSCURRENT version becomes the AWSPREVIOUS version:
.g