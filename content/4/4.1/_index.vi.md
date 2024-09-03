---
title : "Xem xét AWS Config Rules cho Secrets Manager"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> Nhiệm vụ-2.1: </b> "
---
Năm Config rules để kiểm tra tính tuân thủ cho các secret được lưu trữ trong AWS Secrets Manager đã được tạo sẵn cho workshop này:

1. secretsmanager-workshop-rotation-enabled-check
- Kiểm tra AWS Secrets Manager secret có bật tính năng luân phiên hay không.


2. secretsmanager-workshop-scheduled-rotation-success-check
- Kiểm tra việc luân phiên AWS Secrets Manager secret có thành công theo lịch trình luân phiên hay không.


3. secretsmanager-workshop-using-cmk
- Kiểm tra xem các secret có được mã hóa bằng AWS KMS Customer Master Key (CMK) hay không.


4. secretsmanager-workshop-secret-unused
- Kiểm tra xem các secret trong Secrets Manager có được truy cập trong một số ngày nhất định hay không.


5. secretsmanager-workshop-secret-periodic-rotation
- Kiểm tra xem các secret có được luân phiên trong số ngày được chỉ định gần đây hay không.


Bạn có thể xem xét các Config Rule bằng cách thực hiện các bước sau:

1. Điều hướng đến [Config Service console](https://console.aws.amazon.com/config).

2. Nhấp vào "Rules" từ bảng điều khiển bên trái.

3. Xem chi tiết Config Rule bằng cách nhấp vào tên Rule.