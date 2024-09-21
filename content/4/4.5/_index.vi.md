---
title : "Kiểm tra Secret CMK Compliance"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> Nhiệm vụ-2.5: </b> "
---


#### Các bước thực hiện:

1. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager).

![m2](/images/m2/2.5/s1.png)


2. Nhấp vào secret đã được tạo bởi CloudFormation template triển khai trong Module-0. Tên của secret sẽ là "DemoWorkshopSecret".



3. Trong phần “Secret details”, nhấp vào “Edit encryption key” từ menu thả xuống “Actions”:



4. Chọn “aws/secretsmanager”.



5. Bỏ chọn tùy chọn “Create new version of secret with new encryption key”.

**LƯU Ý: Để phục vụ mục đích trình bày trong workshop này, tùy chọn này không được chọn. Đây KHÔNG phải là biện pháp bảo mật tốt nhất cho môi trường sản xuất. Trong môi trường sản xuất, bạn nên chọn tùy chọn này để tạo phiên bản mới của secret với khóa mã hóa mới.**
![m2](/images/m2/2.5/s5.png)

6. Nhấp vào “Save”. Bạn sẽ thấy một thông báo cập nhật thành công màu xanh lá cây ở đầu màn hình.

![m2](/images/m2/2.5/s6.png)
Chuyển thành NON_COMPLIANT:
![m2](/images/m2/2.5/s6b.png)
7. Bây giờ quay lại Encryption Key cho CMK bí danh "AWSSecretsManagerWorkshopKey". CMK này đã được tạo bởi CloudFormation template trong module-0.



8. Bỏ chọn tùy chọn “Create new version of secret with new encryption key”.
![m2](/images/m2/2.5/s8.png)

9. Nhấp vào “Save”. Bạn sẽ thấy một thông báo cập nhật thành công màu xanh lá cây ở đầu màn hình.



*Chờ vài phút và lưu ý các thông báo trong Cổng SNS.*
![m2](/images/m2/2.5/s9.png)