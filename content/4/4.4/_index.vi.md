---
title : "Bật chức năng luân phiên Secret"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> Task-2.4: </b> "
---

Trước khi bật chức năng luân phiên Secret:

1. Truy cập API URL của ứng dụng mẫu trong một tab trình duyệt riêng. Bạn có thể tìm thấy API URL trong bảng điều khiển Event Engine của mình. Lưu ý giá trị của các Version ID cho các nhãn AWSPREVIOUS và AWSCURRENT. Secrets Manager  gán nhãn phiên bản hiện tại đang hoạt động và được sử dụng của secret là AWSCURRENT. Mỗi khi nhãn AWSCURRENT huyển từ phiên bản này sang phiên bản khác, Secrets Manager tự động di chuyển nhãn AWSPREVIOUS đến phiên bản trước đó được gán nhãn AWSCURRENT. Để đọc thêm về cách AWS Secrets Manager luân phiên secret, hãy tham khảo tài liệu [tại đây](https://docs.aws.amazon.com/secretsmanager/latest/userguide/terms-concepts.html#term_rotation).



2. Truy cập cổng nhận thông báo SNS trong một tab trình duyệt riêng. Để truy cập cổng, chỉ cần thêm snsportal vào cuối liên kết API URL của bạn. **Ví dụ**:


Không đóng tab trình duyệt cổng SNS cho đến khi kết thúc workshop. Bạn sẽ sử dụng nó để xem các tin nhắn thông báo SNS.

**Sau đó bật chức năng luân phiên Secret bằng các bước sau:**

1. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager).


2. Nhấp vào secret được tạo bởi CloudFormation template. Tên secret sẽ là “DemoWorkshopSecret”.


3. Trong phần “Rotation configuration”, nhấp vào “Edit rotation”.


4. Chuyển đổi sang “Automatic rotation”.



5. Dưới “Rotation schedule”, nhập số ngày mà secret này sẽ được luân phiên. Ví dụ: 30 ngày.



6. Dưới “Rotation function”, chọn hàm có tên “SecretsManagerMySQLRotationLambda”.



7. Nhấp vào “Save”.



8. Tại thời điểm này, bạn sẽ thấy thông báo màu xanh lá cây ở đầu màn hình “Rotating your secret DemoWorkshopSecret”

*Chờ vài phút và chú ý các tin nhắn trong cổng SNS.*

Truy cập lại API URL của ứng dụng mẫu và quan sát giá trị của các Version ID AWSPREVIOUS và AWSCURRENT.

Lưu ý rằng phiên bản AWSCURRENT sẽ trở thành phiên bản AWSPREVIOUS.

Bạn cũng có thể kiểm tra ứng dụng khi secret được lên lịch để luân phiên bằng cách nhấp vào “Rotate secret immediately”. Sau đó truy cập liên kết API URL của ứng dụng sau khi bạn thấy thông báo thành công màu xanh lá cây ở đầu màn hình.