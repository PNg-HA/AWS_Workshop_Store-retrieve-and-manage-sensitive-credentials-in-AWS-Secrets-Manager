---
title : "Đưa ABAC vào hoạt động"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> Nhiệm vụ-1.2: </b> "
---
Attribute-based access control (ABAC) là một chiến lược ủy quyền xác định quyền dựa trên các thuộc tính. Trong AWS, các thuộc tính này được gọi là tag. Bạn có thể gắn các tag vào IAM resource, bao gồm IAM entity (user hoặc role) và vào AWS resource. ạn có thể tạo một ABAC duy nhất hoặc một tập hợp nhỏ các policy cho các IAM principal. Các ABAC policy này có thể được thiết kế để cho phép các hoạt động khi tag của principal khớp với tag của tài nguyên. ABAC hữu ích trong các môi trường đang phát triển nhanh chóng và giúp ích cho các tình huống mà việc quản lý policy trở nên phức tạp.

Trong phần này, bạn sẽ xem xét các policy được gắn với role của hàm Lambda của ứng dụng mẫu và quan sát hành vi sau khi thực hiện thay đổi các tag.

#### Steps:
1. Điều hướng đến [bảng điều khiển dịch vụ Lambda](https://console.aws.amazon.com/lambda).



2.  Chọn “Functions” từ bảng điều khiển bên trái. Nhấp vào tên hàm “LambdaRDSTest”.




3. Nhấp vào Tab “Configuration”.




4. Chọn “Permissions” từ bảng điều khiển bên trái.



5. Trong phần “Execution Role”, bạn sẽ thấy tên Role “LambdaRDSTestRole” được gắn với hàm Lambda.



6. Nhấp vào “LambdaRDSTestRole”. Thao tác này sẽ đưa bạn đến phần Details của Role trong IAM Management Console.



7. Trong Tab Permissions, bạn sẽ thấy 4 chính sách được gắn với Role này.


8. Nhấp vào biểu tượng "+" bên cạnh “AllowSM” policy.

*Bạn rút ra điều gì từ policy này?*



9. Bây giờ hãy xem xét các Tag cho Role này. Điều hướng đến tab “Tags”.

*Bạn nhận thấy các cặp Key-Value nào của Tag?*



10. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager).



11. Nhấp vào secret được tạo bởi CloudFormation template. Tên secret sẽ là “DemoWorkshopSecret“.


12. Dưới phần “Tags” cho secret, hãy xem xét Tag Values cho các Tag “Event” và “Workshop” và so sánh Tag Key và Tag Value cho các ”LambdaRDSTestRole“ Tag mà bạn đã xem xét ở bước #10 ở trên.

*Bạn quan sát thấy gì?*


13. Bây giờ nhấp vào “Edit tags” để chỉnh sửa các tag cho “DemoWorkshopSecret” secret. Cập nhật giá trị cho tag “Workshop” thành một giá trị khác (ví dụ: AWSKMSWorkshop).



14. Nhấp vào “Save”. Bạn sẽ thấy một thông báo  màu xanh ở trên cùng “Your tags are modified."



15. Nếu bạn truy cập lại API URL trong trình duyệt web của mình, bạn sẽ thấy một thông báo “Database not connected” làm đầu ra.

*Tại sao kết nối lại thất bại?*



16. Thử nghiệm bằng cách cập nhật các Tag của secret thành một kết hợp các giá trị này và quan sát đầu ra từ API URL của ứng dụng.
