---
title : "Giám sát việc tuân thủ khóa bí mật"
date : "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> Mô-đun 2 </b> "
---

Trong mô-đun này, bạn sẽ triển khai quy trình làm việc để theo dõi trạng thái tuân thủ của các bí mật được lưu trữ trong AWS Secrets Manager.

Kiến trúc Compliance Monitoring:
![Architecture](/images/m2/mod2-asm-compliancemonitoring-workflow.png)

#### How rotation works?
![how_rotation_works](/images/m2/how_rotation_works.png)
- Ub (Không thay đổi trước): Giá trị này đề cập đến giá trị bí mật đang hoạt động hiện tại trước khi quá trình xoay vòng bắt đầu.

- Pb (Đang chờ trước): Đây là giá trị bí mật mới được tạo trong quá trình xoay vòng, nhưng vẫn chưa được áp dụng hoặc trở thành giá trị bí mật đang hoạt động.

- Ua (Không thay đổi sau): Giá trị này giống với Ub, biểu thị giá trị bí mật đang hoạt động hiện tại sau khi quá trình xoay vòng hoàn tất thành công.

- Pa (Đang chờ sau): Đây là giá trị bí mật mới được tạo trong quá trình xoay vòng và đã trở thành giá trị bí mật đang hoạt động mới sau khi quá trình xoay vòng hoàn tất thành công.

Quá trình xoay vòng thường tuân theo các bước sau:

1. Ban đầu, giá trị bí mật đang hoạt động là Ub (Không thay đổi trước).
2. Trong quá trình xoay vòng, một giá trị bí mật mới Pb (Đang chờ trước) được tạo.
3. Chức năng xoay vòng (AWS Lambda hoặc xoay vòng Secrets Manager) cập nhật các tài nguyên (ví dụ: cơ sở dữ liệu, ứng dụng) bằng giá trị bí mật Pb mới.
4. Nếu cập nhật thành công, giá trị Pb sẽ trở thành giá trị bí mật hoạt động mới, Pa (Đang chờ sau) và giá trị Ub cũ được đánh dấu là Ua (Không thay đổi sau) để tham khảo.
5. Nếu cập nhật không thành công, quá trình xoay vòng sẽ được khôi phục và giá trị Ub vẫn là giá trị bí mật hoạt động.