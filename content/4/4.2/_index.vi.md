---
title : "Tạo SNS Topic và Subscription để nhận thông báo"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> Nhiệm vụ-2.2: </b> "
---

Trong workshop này, một cổng thông báo SNS bổ sung đã được triển khai trong AWS Account. của bạn. Sử dụng cổng này, bạn có thể xem các thông báo được tạo ra cho các sự kiện mà bạn sẽ cấu hình trong EventBridge Rules. Bây giờ, bạn sẽ cấu hình SNS Topic để đăng ký với cổng thông báo.

#### Các bước thực hiện:

1. Điều hướng đến [Simple Notification Service console](https://console.aws.amazon.com/sns).



2. Nhấp vào “Topics” từ bảng điều khiển bên trái.



3. Nhấp vào “Create topic”.



4. Chọn “Standard”.



5. Nhập tên topic mà bạn chọn, ví dụ: “ASMWorkshopTopic”.



6. Nhấp vào “Create topic”.



7. Khi Topic được tạo thành công, bạn sẽ thấy một thông báo thành công màu xanh ở đầu màn hình.



8. Nhấp vào “Create subscription”.



9. Chọn "AWS Lambda" từ danh sách Protocol.



10. Thay thế các tham số [AWS-REGION] và [ACCOUNT-ID] bằng AWS Region hiện tại và AWS Account ID của bạn trong chuỗi ARN:

```arn:aws:lambda:[AWS-REGION]:[ACCOUNT-ID]:function:SNSPortalLambdaFunction```


**Ví dụ** nếu bạn đang sử dụng us-east-1 region và Account ID của bạn là 111122223333, ARN sẽ là:

```arn:aws:lambda:us-east-1:111122223333:function:SNSPortalLambdaFunction```

Bạn có thể sao chép số tài khoản bằng cách mở rộng menu thả xuống từ góc trên bên phải.



Sao chép chuỗi ARN đã cập nhật vào ô "Endpoint".

11. Nhấp vào “Create subscription”.

Khi Subscription được tạo thành công, bạn sẽ thấy một thông báo thành công màu xanh ở đầu màn hình.