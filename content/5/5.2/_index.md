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
![m2](/images/m3/3.2/s3.png)

4. Try to retrieve the secret value. Click “Retrieve secret value” in the Secret value section.
![m2](/images/m3/3.2/s4.png)

*Q: Are you able to view the secret value? Why or why not?*
A: this policy denies any AWS service or entity from using secretsmanager:GetSecretValue on any resource unless the invoking entity’s ARN matches one of the specified role ARNs.

5. Within the Resource Permissions section, click “Edit Permissions”. Policy update


6. Click inside the text box area and delete all the text from the box. You can also do this by select+all and backspace.



7. Click “Save”.



8. You should see a banner on the screen stating “Deleted resource policy from secret successfully.”:
![m2](/images/m3/3.2/s8.png)


9. Now try to retrieve the secret value after deleting the policy. Refresh the page and click “Retrieve secret value” in the Secret value section.

*Are you able to view the secret value? Why or why not?*

*Hint: Check the contents of the Lambda function named “UpdateSecretPolicyLambdaFunction”*

As a result of this action:

1. You will see a message in the SNS Portal stating that:

**"The Resource Policy of a secret [the ARN of the secret] was attempted for deletion by [your current IAM Role or User] on [Time Stamp]"**
![m2](/images/m3/3.2/Picture1.png)

2. Refresh the API URL for your sample application and observe the version ID updates for the secret.

*What do you observe?*
![m2](/images/m3/3.2/Picture2.png)

3. Navigate to the secret “DemoWorkshopSecret” again in [Secrets Manager Service console](https://console.aws.amazon.com/secretsmanager). 

Different policy appear:
![m2](/images/m3/3.2/Picture3.png)
The above policy look likes the policy trong lambda UpdateSecretPolicyLambdaFunction after format:
![m2](/images/m3/3.2/Picture4.png)
*Q: Attempt to delete the Resource Policy again, what happens?*\
A: This resource policy cannot be deleted (updated), because the lambda UpdateSecretPolicyLambdaFunction is triggered, and this user session is assigned the role DenyUpdateSecretPolicy
![m2](/images/m3/3.2/Picture5.png)
Review the event DeleteResourcePolicy in Cloudtrail:
![m2](/images/m3/3.2/Picture6.png)
![m2](/images/m3/3.2/.p6.png)