---
title : "Store, retrieve, and manage sensitive credentials in AWS Secrets Manager"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
Security Architects are looking to reduce access to plaintext secrets by their application teams. Developers want a mechanism to securely retrieve secrets without hard-coding credentials in their application. They also want assurance that rotation of secrets will not affect application availability. Compliance teams want mechanisms to monitor security of the secrets and aligning with best practices or policy. Finally the SOC want mechanisms to respond to unauthorized or erroneous actions on secrets.

In this workshop, you will use a sample serverless application with AWS Lambda functions connecting to an Amazon RDS database. You will test programmatic retrieval of database credentials from AWS Secrets Manager as well as implement Attribute-based Access Control (ABAC) using tags. You will monitor compliance status of secrets using AWS Config. Later you will rotate secrets within AWS Secrets Manager and test application access. Finally you will test attempts to delete the secrets resource policy for retrieving secrets in plaintext from AWS Secrets Manager. Attendees will use AWS Event Bridge event driven response to deploy incident response workflows that will rotate the secret, restore the resource policy, alert the SOC, and deny access to the offender.

### Scenario


You are working at a company who is moving towards storing their credentials in AWS Secrets Manager. Rather than applications using hard-coded credentials, developers will use Secrets Manager to retrieve the Database credentials for connecting to the database.

We will assume that the organization's security requirements state:

- All secrets must be encrypted at rest using Customer Managed Keys
- All secret modification or retrieval attempts by unauthorized users must notify Admins and SOC.
- Trigger incident response automation to rotate the secret and reduce unauthorized user's privilege profile.
  
![architecture](/images/asm-workshop-architecture.png)

In this workshop, you will wear two hats. First, you will wear the Administrator hat to deploy the configuration to manage the secrets stored in Secrets Manager. Second, you will wear the Developer hat to configure your application for requesting database credentials from Secrets Manager instead of using hard-coded credentials. You will also test the Incident Response configuration that you put in place for remediating against Secret update and retrieval workflow.

The sample application is a Lambda function “LambdaRDSTest” which is initially using Hard-coded environment variables to connect with the Demo MySQL RDS DB Instance.

You will use the secret created in AWS Secrets Manager in your sample application to retrieve the DB credentials from AWS Secrets Manager instead of using Hard-coded Environment variables.

You will also create an automated workflow for Detecting, Alerting and Responding to secret policy deletion and compliance changes for secrets in AWS Secrets Manager.

### Modules
This workshop is broken up into setup and then four modules:

- [Introduction](1-Instructions/)
- [Module-0: Environment Setup](2/)
- [Module-1: Retrieving secrets and implementing access control for secrets stored in AWS Secrets Manager](3) 
- [Module-2: Monitor compliance of secrets](4)
- [Module-3: Automation of Incident Response workflows](5)
<!-- - [Module-4: Recap and summary](6) -->
