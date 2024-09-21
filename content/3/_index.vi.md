---
title : "Truy xuất khóa bí mật và triển khai kiểm soát truy cập cho khóa bí mật"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> Mô-đun 1 </b> "
---

Trong module này, bạn sẽ cập nhật ứng dụng mẫu của mình để truy xuất thông tin xác thực từ AWS Secrets Manager. Bạn có thể sử dụng phần minh họa này để hiểu cách lập trình để truy xuất các secret trong ứng dụng mà không cần con người nhìn thấy các giá trị plaintext secret. Bạn cũng sẽ thấy cách sử dụng các AWS IAM PrincipalTag và ResourceTag condition key để triển khai attribute-based access control (ABAC).

Module này có 2 nhiệm vụ:

- Nhiệm vụ-1.1: Cập nhật mẫu ứng dụng để truy xuất thông tin xác thực của cơ sở dữ liệu từ AWS Secrets Manager
- Nhiệm vụ-1.2: Đưa ABAC vào hoạt động
![Architecture](/images/m1/mod1-asm-flow.png)
