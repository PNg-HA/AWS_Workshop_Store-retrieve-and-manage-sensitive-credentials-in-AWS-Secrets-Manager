---
title : "Kiểm tra Quy trình Tự động hóa"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Nhiệm vụ-3.2: </b> "
---

**Điều kiện tiên quyết:**:

- Nếu chưa hoàn thành, hãy hoàn thành Nhiệm vụ-2.4 trước khi bắt đầu phần này.

#### Các bước thực hiện:

1. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager).


2. Nhấp vào tên secret “DemoWorkshopSecret”.



3. Xem xét Resource Permissions của secret.


*Những entity nào có quyền truy xuất giá trị secret?*
![m2](/images/m3/3.2/s3.png)

4. Thử truy xuất giá trị secret.  Nhấp vào “Retrieve secret value” trong phần Secret value.
![m2](/images/m3/3.2/s4.png)

*Q: Bạn có thể xem giá trị secret không? Tại sao có hoặc tại sao không?*
A: chính sách này từ chối bất kỳ dịch vụ hoặc thực thể AWS nào sử dụng secretsmanager:GetSecretValue trên bất kỳ tài nguyên nào trừ khi ARN của thực thể gọi khớp với một trong các ARN vai trò đã chỉ định

5. Trong phần Resource Permissions, nhấp vào “Edit Permissions”. Cập nhật Policy


6. Xóa tất cả văn bản trong text box. Bạn cũng có thể thực hiện việc này bằng cách chọn tất cả và nhấn phím Backspace.



7. Nhấp vào “Save”.



8. Bạn sẽ thấy một thông báo trên màn hình ghi rằng “Deleted resource policy from secret successfully.”:

![m2](/images/m3/3.2/s8.png)

9. Bây giờ hãy thử truy xuất giá trị secret sau khi xóa policy. Làm mới trang và nhấp vào “Retrieve secret value” trong phần Secret value.

*Bạn có thể xem giá trị secret không? Tại sao có hoặc tại sao không?*

*Gợi ý: Kiểm tra nội dung của hàm Lambda có tên “UpdateSecretPolicyLambdaFunction”*

Kết quả của hành động này:

1. Bạn sẽ thấy một tin nhắn trong Cổng SNS nêu rằng:

**"The Resource Policy of a secret [the ARN of the secret] was attempted for deletion by [your current IAM Role or User] on [Time Stamp]"**
![m2](/images/m3/3.2/Picture1.png)

2. Làm mới API URL cho ứng dụng mẫu của bạn và quan sát các bản cập nhật version ID cho secret.

*Bạn nhận thấy điều gì?*

![m2](/images/m3/3.2/Picture2.png)
3. Điều hướng đến secret “DemoWorkshopSecret” một lần nữa trong [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager). 

![m2](/images/m3/3.2/Picture3.png)

Policy trên giống policy trong lambda UpdateSecretPolicyLambdaFunction sau khi format lại:
![m2](/images/m3/3.2/Picture4.png)

*Q: Hãy thử xóa Resource Policy lần nữa, điều gì xảy ra?*\
A: Không thể xóa (update) resource policy này, là do lambda UpdateSecretPolicyLambdaFunction được trigger, và session user này được gán role DenyUpdateSecretPolicy
![m2](/images/m3/3.2/Picture5.png)

Có thể check bằng Event DeleteResourcePolicy trên CloudTrail:
![m2](/images/m3/3.2/Picture6.png)
![m2](/images/m3/3.2/.p6.png)