---
title : "Lưu trữ, truy xuất và quản lý thông tin xác thực nhạy cảm trong AWS Secrets Manager"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
Security Architects đang tìm cách giảm thiểu việc truy cập vào các plaintext secret bởi các nhóm phát triển ứng dụng của họ. Các nhà phát triển muốn có một cơ chế để truy xuất secret  một cách an toàn mà không cần mã hóa thông tin xác thực trực tiếp trong ứng dụng của họ. Họ cũng muốn đảm bảo rằng việc luân chuyển secret sẽ không ảnh hưởng đến tính sẵn sàng của ứng dụng. Các nhóm tuân thủ muốn có cơ chế giám sát tính bảo mật của secret và phù hợp với các biện pháp hoặc chính sách tốt nhất. Cuối cùng, SOC muốn có cơ chế phản hồi các hành động trái phép hoặc sai sót đối với các secret.

Trong buổi workshop này, bạn sẽ sử dụng một ứng dụng serverless mẫu với các hàm AWS Lambda kết nối đến cơ sở dữ liệu Amazon RDS. Bạn sẽ kiểm tra việc truy xuất lập trình các thông tin xác thực cơ sở dữ liệu từ AWS Secrets Manager cũng như triển khai Attribute-based Access Control (ABAC) bằng cách sử dụng tags. Bạn sẽ theo dõi trạng thái tuân thủ của các secret bằng AWS Config. Sau đó, bạn sẽ luân phiên các secret trong AWS Secrets Manager và kiểm tra quyền truy cập ứng dụng. Cuối cùng, bạn sẽ kiểm tra các nỗ lực xóa chính sách tài nguyên secret để truy xuất các plaintext secret từ AWS Secrets Manager. hững người tham dự sẽ sử dụng phản hồi theo sự kiện AWS Event Bridge để triển khai các quy trình phản hồi sự cố sẽ luân phiên secret, khôi phục chính sách tài nguyên, cảnh báo SOC và từ chối quyền truy cập đối với kẻ vi phạm.

### Tình huống


Bạn đang làm việc tại một công ty đang chuyển sang lưu trữ thông tin xác thực của họ trong AWS Secrets Manager. Thay vì các ứng dụng sử dụng thông tin xác thực được mã hóa cứng, các nhà phát triển sẽ sử dụng Secrets Manager để truy xuất thông tin xác thực của Cơ sở dữ liệu để kết nối với cơ sở dữ liệu.

Chúng ta sẽ giả định rằng các yêu cầu bảo mật của tổ chức quy định:

- Tất cả các secret phải được mã hóa khi lưu trữ bằng Customer Managed Keys
- Tất cả các nỗ lực sửa đổi hoặc truy xuất secret bởi người dùng không được phép phải thông báo cho Quản trị viên và SOC.
- Kích hoạt tự động hóa phản ứng sự cố để luân phiên secret và giảm hồ sơ quyền hạn của người dùng trái phép.
  
![architecture](/images/asm-workshop-architecture.png)

Trong buổi workshop này, bạn sẽ đảm nhận hai vai trò. Đầu tiên, bạn sẽ đảm nhận vai trò của Quản trị viên để triển khai cấu hình nhằm quản lý các secret được lưu trữ trong Secrets Manager. Thứ hai, bạn sẽ đảm nhận vai trò của Nhà phát triển để cấu hình ứng dụng của bạn để yêu cầu thông tin xác thự của Cơ sở dữ liệu từ Secrets Manager thay vì sử dụng các biến môi trường được mã hóa trực tiếp. Bạn cũng sẽ kiểm tra cấu hình phản ứng sự cố mà bạn đã thiết lập để khắc phục các quy trình cập nhật và truy xuất secret.

Ứng dụng mẫu là một hàm Lambda có tên “LambdaRDSTest” ban đầu sử dụng các biến môi trường được mã hóa trực tiếp để kết nối với MySQL RDS Demo Instance.

Bạn sẽ sử dụng secret được tạo trong AWS Secrets Manager trong ứng dụng mẫu của bạn để truy xuất các thông tin xác thực của Cơ sở dữ liệu từ AWS Secrets Manager thay vì sử dụng các biến môi trường được mã hóa trực tiếp.

Bạn cũng sẽ tạo một quy trình tự động để phát hiện, cảnh báo và phản hồi đối với việc xóa chính sách secret và thay đổi trạng thái tuân thủ đối với các secret trong AWS Secrets Manager.


### Modules
Buổi workshop này được chia thành phần cài đặt và bốn module:

- [Introduction](1-Instructions/)
- [Module-0: Environment Setup](2/)
- [Module-1: Retrieving secrets and implementing access control for secrets stored in AWS Secrets Manager](3) 
- [Module-2: Monitor compliance of secrets](4)
- [Module-3: Automation of Incident Response workflows](5)
<!-- - [Module-4: Recap and summary](6) -->
