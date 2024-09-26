---
title : "Monitor Compliance of Secrets"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> Module-2 </b> "
---

In this module, you will deploy the workflow to monitor compliance status of secrets stored in AWS Secrets Manager.

Architecture for Compliance Monitoring:
![Architecture](/images/m2/mod2-asm-compliancemonitoring-workflow.png)

#### How rotation works?
![how_rotation_works](/images/m2/how_rotation_works.png)

- Ub (Unchanged Before): This refers to the current active secret value before the rotation process starts.

- Pb (Pending Before): This is the new secret value that is generated during the rotation process, but it has not yet been applied or become active.

- Ua (Unchanged After): This is the same as Ub, representing the current active secret value after the rotation process completes successfully.

- Pa (Pending After): This is the new secret value that has been generated during the rotation process and has become the new active secret value after the rotation process completes successfully.

The rotation process typically follows these steps:

1. Initially, the active secret value is Ub (Unchanged Before).
2. During the rotation process, a new secret value Pb (Pending Before) is generated.
3. The rotation function (either AWS Lambda or the Secrets Manager rotation) updates the resources (e.g., databases, applications) with the new Pb secret value.
4. If the update is successful, the Pb value becomes the new active secret value, Pa (Pending After), and the old Ub value is marked as Ua (Unchanged After) for reference.
5. If the update fails, the rotation process is rolled back, and the Ub value remains as the active secret value.

