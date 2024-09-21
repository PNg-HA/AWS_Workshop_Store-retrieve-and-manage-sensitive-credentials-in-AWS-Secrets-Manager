---
title : "Putting ABAC into Action"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Task-1.2: </b> "
---
Attribute-based access control (ABAC) is an authorization strategy that defines permissions based on attributes. In AWS, these attributes are called tags. You can attach tags to IAM resources, including IAM entities (users or roles) and to AWS resources. You can create a single ABAC policy or small set of policies for your IAM principals. These ABAC policies can be designed to allow operations when the principal's tag matches the resource tag. ABAC is helpful in environments that are growing rapidly and helps with situations where policy management becomes cumbersome.

In this section, you will review the policies attached to the sample application Lambda function role and observe the behavior after making changes to the tags.

#### Steps:
1. Navigate to the [Lambda service console](https://console.aws.amazon.com/lambda).



2. Select “Functions” from the left panel. Click on the “LambdaRDSTest” function name.




3. Click on the “Configuration'” Tab.




4. Click on “Permissions” from the left panel.



5. In the “Execution Role” section, you will see a Role name “LambdaRDSTestRole” that is attached to the Lambda function.

![1.2](/images/m1/1.2/s5.png)

6. Click on “LambdaRDSTestRole”. This action will take you to the Role details in the IAM Management Console.




7. In the Permissions Tab, you will notice 4 policies that are attached to this Role.

![1.2](/images/m1/1.2/s7.png)
Check out Trust relationships
![1.2](/images/m1/1.2/s7b.png)
8. Click on the "+" symbol beside the “AllowSM” policy.
![1.2](/images/m1/1.2/s8.png)
*Q: What do you infer from the policy?*


A: it checks if the aws:ResourceTag/Event and aws:ResourceTag/Workshop tags match the corresponding values in the aws:PrincipalTag/Event and aws:PrincipalTag/Workshop tags.
9. Now let’s review the Tags for this Role. Navigate to the “Tags” tab.

*What Tag Key-Value pairs do you notice?*



10. Navigate to [Secrets Manager service console](https://console.aws.amazon.com/secretsmanager).



11. Click on the secret that was created by the CloudFormation template. The secret name will be “DemoWorkshopSecret“.


12. Under the “Tags” section for the secret, review the Tag Values for the Tags “Event” and “Workshop” and compare the Tag Key and Tag Value for the ”LambdaRDSTestRole“ Tags that you reviewed in step # 10 above.

*What do you observe?*
![1.2](/images/m1/1.2/s12.png)

13. Now click on “Edit tags” to edit the tags for the “DemoWorkshopSecret” secret. Update the value for the tag “Workshop” to another value (e.g. AWSKMSWorkshop).

![1.2](/images/m1/1.2/s13.png)


14. Click “Save”. You will see a green banner on the top stating “Your tags are modified."

![1.2](/images/m1/1.2/s14.png)


15. If you access the API URL again in your web browser, you will see a message “Database not connected” as an output.
![1.2](/images/m1/1.2/s15.png)

*Why did the connection fail?*

A: It failed because of different value in Workshop tag (must be AWSSecretsManagerWorkshop)

16. Experiment by updating the Tags of the secret to a combination of these values and observe the output from the application API URL.

![1.2](/images/m1/1.2/s16.png)
Changing the Workshop tag value to 'AmazonGuardDutyWorkshop' still doesn't connect.


![1.2](/images/m1/1.2/s16b.png)
Changing the Event value to "conference" also does not connect to the database

![1.2](/images/m1/1.2/s16d.png)
If the Workshop and Event tags have values ​​as below, the database query will be successful.