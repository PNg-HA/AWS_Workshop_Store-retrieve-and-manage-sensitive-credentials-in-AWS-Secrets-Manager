---
title : "Update Sample Application"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> Task-1.1: </b> "
---



### Update Sample Application to retrieve database credentials from AWS Secrets Manager
#### Steps:
Update Sample Application to retrieve database credentials from AWS Secrets Manager

1. Navigate to the [Lambda service console](https://console.aws.amazon.com/lambda).

2. Select “Functions” from the left panel. Click on the “LambdaRDSTest” function name. This is the function that is used for the sample application to connect to the RDS Database. The function is written in Python language. The Database contains sample data about First Names and the Last Names.

3. You can review the code for the sample application by double clicking on “LambdaRDSTest.py” in the “Code Source” section.



The function openConnection() within the code connects to the MySQL RDS DB using the parameters that are stored in the Environment Variables. When the Database is connected, application will print the sample data.

4. Paste and access the API URL that you copied earlier (in the CloudFormation stack's Event Outputs section) in a separate web browser tab. You should see a Database not connected message
```
Why wasn't the application able to connect to the RDS database for retrieving the sample data?
```


5. Now, let’s update application “LambdaRDSTest” code to retrieve the Database credentials from the Secrets Manager instead of using Environment Variables. Return to the browser tab where the LambdaRDSTest.py code is opened.

a. Comment the following 4 lines in the code (lines number 15, 16, 17, 18) by inserting a # in the beginning of each line as shown below.

b. Under “Configuration” click on “Environment variables”. You will see Environment Variables similar to below:

c. Delete all the Key Value pairs for the Environment Variables:

6. Go back to the source code under Code Source section:



7. Click “Deploy” to save the changes and wait until the following message appears:



8. Navigate to [Secrets Manager service console](https://console.aws.amazon.com/secretsmanager) .



9. Click on the secret that was created by the CloudFormation template. The secret name will be “DemoWorkshopSecret“.



10. Scroll down to the “Sample code” section. Click on “Python3”



11. Select and Copy the code from line # 11 to line # 34.

*Note: Python is an indent sensitive language, it’s important to indent the code correctly. Make sure you select the sample code from line # 11, otherwise it can lead to indentation issues.*


12. Return to the browser tab where the LambdaRDSTest Lambda function code is opened.



13. Traverse to line # 24 in the code and press Enter at the end of the line:



14. Paste the sample code that you copied from Secrets Manager.




15. Secrets Manager returns the DB Credentials as a string. You will now add code to extract the connection parameters for connecting to the Database from the returned string. To save time for this workshop, the code block is already added in the sample Lambda function:
```
secretstring = json.loads(secret)
rds_host = secretstring['host']
username = secretstring['username']
password = secretstring['password']
db_name =  secretstring['dbname']
```

To use it, you will just need to un-comment the lines (remove # from the start of the line) of codes in the Lambda function.


16. Verify that the modified code should be similar to this:

At this point, the application is configured to make a database connection using the retrieved credentials from the secret in AWS Secrets Manager. The pymysql.connect command uses the retrieved credentials from the secret.


17. Click “Deploy” to save the changes and wait until the following message appears:



18. Access the API URL again in your web browser, you should be able to see the sample data retrieved from the database similar to this:

The output displays the sample data as well as Version ID’s of the secret. When the CloudFormation template is deployed, the secret is updated after it’s first created.

You can observe in the lambda function code that an API call describe_secret is made when the connection to the Database is opened:

*get_describe_secret_response = client.describe_secret(SecretId=secret_name)*