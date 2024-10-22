---
title : "Tạo Amazon EventBridge Event Rule"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> Nhiệm vụ-2.3: </b> "
---
#### Các bước thực hiện
1. Điều hướng đến [bảng điều khiển dịch vụ Amazon EventBridge](https://console.aws.amazon.com/events).



2. Nhấp vào “Create rule”.


3. Nhập tên cho Event Rule theo ý của bạn, ví dụ: MonitorSecretsConfig.

![m2](/images/m2/2.3/s3.png)

4. Nhấp vào "Next".



5. Cuộn xuống phần “Event pattern”:



a. Dưới mục “Event source”, chọn “AWS services”.

b. Dưới mục “AWS service”, chọn “Config” từ danh sách.

c. Dưới mục “Event type”, chọn “Config Rules Compliance Change” từ danh sách.
![m2](/images/m2/2.3/s5c.png)
d. Chọn “Any message type”.
![m2](/images/m2/2.3/s5d.png)
e. Chọn “Specific rule name(s)” và

- Nhập tên config rule secretsmanager-workshop-scheduled-rotation-success-check vào text-box. Nhấp vào ”Add“.
- Nhập tên config rule secretsmanager-workshop-rotation-enabled-check vào text-box mới. Nhấp vào ”Add“.
- Nhập tên config rule secretsmanager-workshop-using-cmk vào text-box mới. Nhấp vào ”Add“.
- Nhập tên config rule secretsmanager-workshop-secret-periodic-rotation vào text-box mới. Nhấp vào ”Add“.
- Nhập tên config rule secretsmanager-workshop-secret-unused vào text-box mới.


f. Chọn “Any resource type”. 
g. Chọn “Any resource ID”.
![m2](/images/m2/2.3/5f1.png)
![m2](/images/m2/2.3/5f2.png)


6. Nhấp vào "Next".


7. Trong bước “Select target(s)”, chọn “SNS topic” từ danh sách thả xuống cho Target 1 và sau đó chọn tên của SNS topic đã được tạo trong Nhiệm vụ-2.4, ví dụ: "ASMWorkshopTopic".



8. Mở rộng "Additional settings" và chọn "Input transformer" từ menu thả xuống.

![m2](/images/m2/2.3/s8.png)


9. Nhấp vào "Configure input transformer".



10. Cuộn xuống phần "Target input transformer", và dán nội dung sau vào "Input path" textbox.
```
{"resource":"$.detail.resourceId","compliance":"$.detail.newEvaluationResult.complianceType","rule":"$.detail.configRuleName","time":"$.detail.newEvaluationResult.resultRecordedTime"}
```
![m2](/images/m2/2.3/s10.png)
11. Dán nội dung sau vào "Template" textbox.
```"The compliance state of secret <resource> for rule <rule> has changed to <compliance> at <time>."```

![m2](/images/m2/2.3/s11.png)
12. Nhấp vào "Confirm".



13. Nhấp vào "Next" và tiếp tục nhấp "Next" để bỏ qua bước "Configure tags".



14. Cuộn xuống và nhấp vào "Create rule". Sau khi Rule được tạo, bạn sẽ thấy một thông báo màu xanh lá cây xuất hiện ở trên cùng của màn hình.

Xem lại:
![m2](/images/m2/2.3/s14.png)
Kết quả:
![m2](/images/m2/2.3/s14b.png)
Xem EventBridge Rule: - Event partern:
![m2](/images/m2/2.3/s14c.png)
![m2](/images/m2/2.3/s14d.png)