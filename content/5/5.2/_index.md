---
title : "Test Automation Workflow"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Task-3.2: </b> "
---

**Pre-requisites**:

- If not completed already, complete Task-2.4 before starting this section.

#### Steps:

1. Navigate to the [Secrets Manager Service console](https://console.aws.amazon.com/secretsmanager).


2. Click on the secret name “DemoWorkshopSecret”.



3. Review the Resource Permissions of the secret.


*Which entities have access to retrieve the secret value?*


4. Try to retrieve the secret value. Click “Retrieve secret value” in the Secret value section.


*Are you able to view the secret value? Why or why not?*


5. Within the Resource Permissions section, click “Edit Permissions”. Policy update


6. Click inside the text box area and delete all the text from the box. You can also do this by select+all and backspace.



7. Click “Save”.



8. You should see a banner on the screen stating “Deleted resource policy from secret successfully.”:



9. Now try to retrieve the secret value after deleting the policy. Refresh the page and click “Retrieve secret value” in the Secret value section.

*Are you able to view the secret value? Why or why not?*

*Hint: Check the contents of the Lambda function named “UpdateSecretPolicyLambdaFunction”*

As a result of this action:

1. You will see a message in the SNS Portal stating that:

**"The Resource Policy of a secret [the ARN of the secret] was attempted for deletion by [your current IAM Role or User] on [Time Stamp]"**


2. Refresh the API URL for your sample application and observe the version ID updates for the secret.

*What do you observe?*


3. Navigate to the secret “DemoWorkshopSecret” again in [Secrets Manager Service console](https://console.aws.amazon.com/secretsmanager). 

*Why do you see the Resource Policy again? Attempt to delete the Resource Policy again, what happens?*