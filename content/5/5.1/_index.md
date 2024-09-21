---
title : "Create an Amazon EventBridge Event Rule"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

**Pre-requisites:**

- If not completed already, complete Task-2.2 before starting this section.

#### Steps:

1. Navigate to the [Amazon EventBridge Service console](https://console.aws.amazon.com/events).


2. Select “Rules" from the left panel and click “Create rule”.



3. Enter the Name for the Event Rule of your choice, e.g. “DeleteSecretResourcePolicyRule”.
![m2](/images/m3/3.1/s3.png)


4. Click "Next".



5. Scroll down to the “Event pattern” section and select “Custom patterns (JSON editor)”.



6. Paste the following pattern in the “Event pattern” textbox:

```
    {
  "source": [
    "aws.secretsmanager"
  ],
  "detail-type": [
    "AWS API Call via CloudTrail"
  ],
  "detail": {
    "eventSource": [
      "secretsmanager.amazonaws.com"
    ],
    "eventName": [
      "DeleteResourcePolicy"
    ]
  }
}
```

It should look like:
![m2](/images/m3/3.1/s6.png)

7. Click "Next".



8. Under “Select target(s)” step, choose “Lambda function” from the drop down list for Target 1.



9. Select the function named “UpdateSecretPolicyLambdaFunction” and click “Add another target”.
![m2](/images/m3/3.1/s9.png)

10. Choose “SNS topic” from the first drop down list and the name of the SNS topic “ASMWorkshopTopic“ (that you created in Task-2.2) in the second drop down list.
![m2](/images/m3/3.1/s10.png)


11. Expand "Additional settings" and select "Input transformer" under the drop down menu.



12. Click "Configure input transformer".



13. Scroll down to "Target input transformer" section, and paste the following under "Input path" textbox:

```
{"AccessingParty":"$.detail.userIdentity.arn","EventTime":"$.detail.eventTime","Secret":"$.detail.responseElements.aRN"}
```


14. Paste the following under "Template" textbox.
```
"The Resource Policy of a secret <Secret> was attempted for deletion by <AccessingParty> on <EventTime>. "
```


15. Click "Confirm".



16. Click "Next" and continue to click "Next" to skip the "Configure tags" step.



17. Scroll down and click “Create rule".
![m2](/images/m3/3.1/s17.png)
Once the Rule is created, you will see a green banner at the top of the screen:
![m2](/images/m3/3.1/s17b.png)