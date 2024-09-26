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
![1.1](/images/m1/1.1/s1.png)
2. Select “Functions” from the left panel. Click on the “LambdaRDSTest” function name. This is the function that is used for the sample application to connect to the RDS Database. The function is written in Python language. The Database contains sample data about First Names and the Last Names.

3. You can review the code for the sample application by double clicking on “LambdaRDSTest.py” in the “Code Source” section.
![1.1](/images/m1/1.1/s3a.png)
![1.1](/images/m1/1.1/s3b.png)

The function openConnection() within the code connects to the MySQL RDS DB using the parameters that are stored in the Environment Variables. When the Database is connected, application will print the sample data.

```bash
# Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.
# SPDX-License-Identifier: MIT-0
import sys
import pymysql
import boto3
import botocore
import json
import random
import time
import os
from botocore.exceptions import ClientError
conn = None

# rds settings
rds_host = os.environ['RDS_HOST']
username = os.environ['RDS_USERNAME']
db_name = os.environ['RDS_DB_NAME']
password = os.environ['PASSWORD']

def openConnection():
    global conn
    global describe_secret_response_version

    # PRESS ENTER AFTER THIS COMMENT AND PASTE THE COPIED SAMPLE CODE FROM AWS SECRETS MANAGER
    
    
    #secretstring = json.loads(secret)
    #rds_host = secretstring['host']
    #username = secretstring['username']
    #password = secretstring['password']
    #db_name =  secretstring['dbname']
    

    try:
        print("Opening Connection")
        if(conn is None):
            conn = pymysql.connect(host=rds_host, user=username, passwd=password, db=db_name, connect_timeout=5)
            get_describe_secret_response = client.describe_secret(SecretId=secret_name)
            describe_secret_response_version = str(get_describe_secret_response['VersionIdsToStages'])
        elif (not conn.open):
            conn = pymysql.connect(host=rds_host, user=username, passwd=password, db=db_name, connect_timeout=5)
            get_describe_secret_response = client.describe_secret(SecretId=secret_name)
            describe_secret_response_version = str(get_describe_secret_response['VersionIdsToStages'])

    except Exception as e:
        print (e)
        print("ERROR: Unexpected error: Could not connect to MySql instance.")
        raise e


def lambda_handler(event, context):

    try:
        openConnection()
        if(conn.open):
            with conn.cursor() as cur:
                cur.execute("select * from DemoTable")
                records = cur.fetchall()
                p = []
                tbl = "<tr><td>First Name</td><td>Last Name</td></tr>"
                p.append(tbl)
                
                for row in records:
                    a = "<tr><td>%s</td>"%row[1]
                    p.append(a)
                    b = "<td>%s</td></tr>"%row[2]
                    p.append(b)
            
                lst = str(p)
                f=lst.replace("', '", "")
                g=f.replace("[", "")
                h=g.replace("]","")
                x=h.replace("'", "")
                content = "<html><head><style>table, th, td {  border: 1px solid black;}</style><title>AWS Secrets Manager workshop</title></head><body><table>%s</table></body></html>"%(x)
                
                response = {
                    "statusCode": 200,
                    "body": content+describe_secret_response_version,
                    "headers": {
                        'Content-Type': 'text/html' ,
                    }
                }
                return response
    except Exception as e:
        print(e)
        content =  "<html><head><title>AWS Secrets Manager workshop</title></head><body>Database not connected</body></html>"                
        response = {
            "statusCode": 200,
            "body": content,
            "headers": {
                'Content-Type': 'text/html' ,
                
            }
            
        }
        return response
    finally:
        print("Closing Connection")
        if(conn is not None and conn.open):
            conn.close()
```

4. Paste and access the API URL that you copied earlier (in the CloudFormation stack's Event Outputs section) in a separate web browser tab. You should see a Database not connected message

![1.1](/images/m1/1.1/s4.png)

Ques: Why wasn't the application able to connect to the RDS database for retrieving the sample data?

Answer: Because the password has been configured to be used from Amazon Secret Manager \

5. Now, let’s update application “LambdaRDSTest” code to retrieve the Database credentials from the Secrets Manager instead of using Environment Variables. Return to the browser tab where the LambdaRDSTest.py code is opened.

a. Comment the following 4 lines in the code (lines number 15, 16, 17, 18) by inserting a # in the beginning of each line as shown below.

b. Under “Configuration” click on “Environment variables”. You will see Environment Variables similar to below:

![1.1](/images/m1/1.1/s5b.png)

c. Delete all the Key Value pairs for the Environment Variables:

6. Go back to the source code under Code Source section:



7. Click “Deploy” to save the changes and wait until the following message appears:

![1.1](/images/m1/1.1/s7.png)

8. Navigate to [Secrets Manager service console](https://console.aws.amazon.com/secretsmanager) .

![1.1](/images/m1/1.1/s8.png)

9. Click on the secret that was created by the CloudFormation template. The secret name will be “DemoWorkshopSecret“. 
![1.1](/images/m1/1.1/s9.png)
Check key.
![1.1](/images/m1/1.1/s9b.png)
10. Scroll down to the “Sample code” section. Click on “Python3”

![1.1](/images/m1/1.1/s10.png)
```bash
# Use this code snippet in your app.
# If you need more information about configurations
# or implementing the sample code, visit the AWS docs:
# https://aws.amazon.com/developer/language/python/

import boto3
from botocore.exceptions import ClientError


def get_secret():

    secret_name = "DemoWorkshopSecret"
    region_name = "us-east-1"

    # Create a Secrets Manager client
    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )

    try:
        get_secret_value_response = client.get_secret_value(
            SecretId=secret_name
        )
    except ClientError as e:
        # For a list of exceptions thrown, see
        # https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_GetSecretValue.html
        raise e

    secret = get_secret_value_response['SecretString']

    # Your code goes here.
```
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
![1.1](/images/m1/1.1/s16.png)

17. Click “Deploy” to save the changes and wait until the following message appears:



18. Access the API URL again in your web browser, you should be able to see the sample data retrieved from the database similar to this:

The output displays the sample data as well as Version ID’s of the secret. When the CloudFormation template is deployed, the secret is updated after it’s first created.
![1.1](/images/m1/1.1/s18.png)
You can observe in the lambda function code that an API call describe_secret is made when the connection to the Database is opened:

*get_describe_secret_response = client.describe_secret(SecretId=secret_name)*

According to [Boto3 document](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/secretsmanager/client/describe_secret.html), the function returns the details of a secret. It does not include the encrypted secret value.