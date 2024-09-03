---
title : "Thiết Lập Môi Trường"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Module-0 </b> "
---

Trong module này, CloudFormation template đã được triển khai để tạo các tài nguyên sau:

- Cấu hình VPC cho ứng dụng mẫu
- Customer Managed Key (CMK) trong AWS KMS thử nghiệm
- Amazon RDS MySQL Database Instance thử nghiệm
- Secret chứa thông tin đăng nhập cho Amazon RDS MySQL Database Instance thử nghiệm
- Hàm Lambda cho ứng dụng mẫu
- Các hàm Lambda để khởi tạo và nạp dữ liệu vào cơ sở dữ liệu cho ứng dụng mẫu
- API Gateway để truy cập ứng dụng mẫu
- Hàm Lambda luân phiên secret cho Cơ sở dữ liệu RDS MySQL
- Hàm Lambda khắc phục sự cố cho quy trình làm việc Ứng phó sự cố

Sau khi hoàn thành Module này, việc triển khai sẽ bao gồm các tài nguyên sau:
![Architecture](/images/m0/mod0-asm-archi.png)