---
title : "Cập nhật Ứng dụng Mẫu"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> Nhiệm vụ-1.1: </b> "
---



### Cập nhật ứng dụng mẫu để truy xuất thông tin xác thực của cơ sở dữ liệu từ AWS Secrets Manager
#### Các bước:
Cập nhật ứng dụng mẫu để truy xuất thông tin xác thực của cơ sở dữ liệu từ AWS Secrets Manager

1. Điều hướng đến [bảng điều khiển dịch vụ Lambda](https://console.aws.amazon.com/lambda).

2. Chọn “Functions” từ bảng điều khiển bên trái. Nhấp vào tên hàm “LambdaRDSTest”. Đây là hàm được sử dụng cho ứng dụng mẫu để kết nối với cơ sở dữ liệu RDS. Hàm này được viết bằng ngôn ngữ Python. Cơ sở dữ liệu chứa dữ liệu mẫu về Tên và Họ.

3. Bạn có thể xem code của ứng dụng mẫu bằng cách nhấp đúp vào “LambdaRDSTest.py” trong phần “Code Source”.



Hàm openConnection() trong code kết nối với cơ sở dữ liệu MySQL RDS bằng cách sử dụng các tham số được lưu trữ trong Biến Môi Trường (Environment Variables). Khi cơ sở dữ liệu được kết nối, ứng dụng sẽ in ra dữ liệu mẫu.

4. Dán và truy cập API URL mà bạn đã sao chép trước đó (trong phần Event Outputs của CloudFormation stack) trên một tab trình duyệt web riêng. Bạn sẽ thấy thông báo Database not connected.
```
Why wasn't the application able to connect to the RDS database for retrieving the sample data?
```


5. Bây giờ, hãy cập nhật code hàm “LambdaRDSTest” để lấy thông tin xác thực củacơ sở dữ liệu từ Secrets Manager thay vì sử dụng Biến Môi Trường. Quay lại tab trình duyệt nơi code LambdaRDSTest.py được mở.

a. Comment 4 dòng code sau (dòng số 15, 16, 17, 18) bằng cách thêm dấu # ở đầu mỗi dòng như hiển thị dưới đây.

b. Dưới mục “Configuration”, nhấp vào “Environment variables”. Bạn sẽ thấy các Biến Môi Trường tương tự như dưới đây:

c. Xóa tất cả các cặp khóa giá trị (Key Value pairs) cho các Biến Môi Trường:

6. Quay lại mã nguồn trong phần “Code Source”:



7. Nhấp vào “Deploy” để lưu các thay đổi và đợi cho đến khi xuất hiện thông báo sau:



8. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager) .



9. Nhấp vào secret được tạo bởi CloudFormation template. Tên của secret sẽ là “DemoWorkshopSecret“.



10. Cuộn xuống phần “Sample code”. Nhấp vào “Python3”.



11. Chọn và sao chép code từ dòng #11 đến dòng #34.

*Lưu ý: Python là ngôn ngữ nhạy cảm với việc căn lề, điều quan trọng là phải căn lề code đúng cách. Hãy chắc chắn rằng bạn chọn code mẫu từ dòng #11, nếu không có thể dẫn đến các vấn đề về căn lề.*


12. Quay lại tab trình duyệt nơi code hàm LambdaRDSTest đang mở.



13. Di chuyển đến dòng #24 trong code và nhấn Enter ở cuối dòng.



14. Dán code mẫu mà bạn đã sao chép từ Secrets Manager.




15. Secrets Manager trả về thông tin xác thực của cơ sở dữ liệu dưới dạng chuỗi. Bây giờ bạn sẽ thêm code để trích xuất các tham số kết nối từ chuỗi trả về để kết nối với cơ sở dữ liệu. Để tiết kiệm thời gian cho workshop này, code đã được thêm sẵn vào hàm Lambda mẫu:
```
secretstring = json.loads(secret)
rds_host = secretstring['host']
username = secretstring['username']
password = secretstring['password']
db_name =  secretstring['dbname']
```

Để sử dụng nó, bạn chỉ cần bỏ comment  (bỏ # ở đầu dòng) các dòng code trong hàm Lambda.


16. Xác minh rằng code đã sửa đổi giống với:

Tại thời điểm này, ứng dụng đã được cấu hình để thực hiện kết nối cơ sở dữ liệu bằng cách sử dụng thông tin xác thực được truy xuất từ secret trong AWS Secrets Manager. Lệnh pymysql.connect sử dụng thông tin xác thực được truy xuất từ secret.


17. Nhấp vào “Deploy” để lưu các thay đổi và đợi cho đến khi xuất hiện thông báo sau:



18. Truy cập lại API URL trong trình duyệt web của bạn, bạn sẽ thấy dữ liệu mẫu được truy xuất từ cơ sở dữ liệu tương tự như thế này:

Kết quả hiển thị dữ liệu mẫu cũng như Version ID của secret. Khi CloudFormation template được triển khai, secret được cập nhật sau khi nó được tạo lần đầu tiên.

Bạn có thể quan sát trong code hàm Lambda rằng một lệnh gọi API describe_secret được thực hiện khi kết nối với cơ sở dữ liệu được mở:

*get_describe_secret_response = client.describe_secret(SecretId=secret_name)*