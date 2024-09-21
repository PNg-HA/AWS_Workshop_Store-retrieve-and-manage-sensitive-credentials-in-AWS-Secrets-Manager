---
title : "Create Amazon EventBridge Event Rule"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> Task-2.3: </b> "
---
#### Steps
1. Navigate to the [Amazon EventBridge Service console](https://console.aws.amazon.com/events).



2. Click “Create rule”.


3. Enter the Name for the Event Rule of your choice, e.g. MonitorSecretsConfig.



4. Click "Next".



5. Scroll down to the “Event pattern” section:



a. Under “Event source”, select “AWS services”.

b. Under “AWS service”, choose “Config” from the list.

c. Under “Event type”, choose “Config Rules Compliance Change” from the list.

d. Select “Any message type”.

e. Select “Specific rule name(s)” and

- Enter the config rule name secretsmanager-workshop-scheduled-rotation-success-check in the text-box. Click ”Add“.
- Enter the config rule name secretsmanager-workshop-rotation-enabled-check in the new text-box. Click ”Add“.
- Enter the config rule name secretsmanager-workshop-using-cmk in the new text-box. Click ”Add“.
- Enter the config rule name secretsmanager-workshop-secret-periodic-rotation in the new text-box. Click ”Add“.
- Enter the config rule name secretsmanager-workshop-secret-unused in the new text-box.


f. Select “Any resource type”. g. Select “Any resource ID”.



6. Click "Next".


7. Under “Select target(s)” step, choose “SNS topic” from the drop down list for Target 1 and then select the name of the SNS topic that was created in Task-2.4 e.g. "ASMWorkshopTopic".



8. Expand "Additional settings" and select "Input transformer" under the drop down menu.



9. Click "Configure input transformer".



10. Scroll down to "Target input transformer" section, and paste the following under "Input path" textbox.
```
{"resource":"$.detail.resourceId","compliance":"$.detail.newEvaluationResult.complianceType","rule":"$.detail.configRuleName","time":"$.detail.newEvaluationResult.resultRecordedTime"}
```

11. Paste the following under "Template" textbox.
```"The compliance state of secret <resource> for rule <rule> has changed to <compliance> at <time>."```


12. Click "Confirm".



13. Click "Next" and continue to click "Next" to skip the "Configure tags" step.



14. Scroll down and click "Create rule". Once the Rule is created, you will see a Green banner on the top of screen.

Review:
.a
Result:
.b
View the EventBridge Rule: - Event partern:
.c
.d