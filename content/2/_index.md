---
title : "Module-0: Environment Setup"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Module-0 </b> "
---

In this module, the CloudFormation template has been deployed to create the following resources:

- VPC Configuration for sample application
- Demo Customer Managed Key (CMK) in AWS KMS
- Demo Amazon RDS MySQL Database Instance
- Secret with database credentials for the Demo Amazon RDS MySQL Database Instance
- Lambda function for the sample application
- Lambda functions to initialize and populate the database with data for sample application
- API Gateway for accessing the sample application
- Rotation Lambda function to rotate secrets for RDS MySQL Database
- Remediation Lambda function for Incident Response workflow

By the end of this Module, the deployment includes the following resources:
![Architecture](/images/m0/mod0-asm-archi.png)