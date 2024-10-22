---
title : "Create SNS Topic and Subscription for receiving notifications"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> Task-2.2: </b> "
---

For this workshop, a complimentry SNS notification receiving portal is deployed in your AWS Account. Using this portal you can view the notifications that are generated for the events that you will configure in the EventBridge Rules. You will now configure the SNS Topic to subscribe to the portal application.

#### Steps:

1. Navigate to the [Simple Notification Service console](https://console.aws.amazon.com/sns).



2. Click “Topics” from the left panel.



3. Click “Create topic”.



4. Select “Standard”.



5. Enter the topic name of your choice e.g. “ASMWorkshopTopic”.



6. Click “Create topic”.

![m2](/images/m2/2.2/s6.png)

7. When the Topic is created successfully, you will see a green banner on the top of the screen stating the success message.



8. Click “Create subscription”.



9. Select "AWS Lambda" from the Protocol drop down list.



10. Replace the [AWS-REGION] and [ACCOUNT-ID] parameters with your current AWS Region and AWS Account ID in the ARN string:

```arn:aws:lambda:[AWS-REGION]:[ACCOUNT-ID]:function:SNSPortalLambdaFunction```

**As an example** if you are using us-east-1 region and your Account ID is 111122223333, the ARN will be:

```arn:aws:lambda:us-east-1:111122223333:function:SNSPortalLambdaFunction```

You can copy the account number by expanding the drop down menu from the top right corner.



Copy the updated ARN string in the "Endpoint" text box.
![m2](/images/m2/2.2/s10.png)

11. Click “Create subscription”.

When the Subscription is created successfully, you will see a green banner on the top of the screen stating the success message.

![m2](/images/m2/2.2/s11.png)