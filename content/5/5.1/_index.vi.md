---
title : "Tạo Amazon EventBridge Event Rule"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

**Điều kiện tiên quyết:**

- Nếu chưa hoàn thành, hãy hoàn thành Nhiệm vụ-2.2 trước khi bắt đầu phần này.

#### Các bước thực hiện:

1. Điều hướng đến [Bảng điều khiển dịch vụ Amazon EventBridge](https://console.aws.amazon.com/events).


2. Chọn “Rules" từ bảng điều khiển bên trái và nhấp vào “Create rule”.



3. Nhập Tên cho Event Rule theo ý của bạn, ví dụ: “DeleteSecretResourcePolicyRule”.

![m2](/images/m3/3.1/s3.png)

4. Nhấp vào "Next".



5. Cuộn xuống phần “Event pattern” và chọn “Custom patterns (JSON editor)”.



6. Dán mẫu sau vào “Event pattern” textbox:

```
    {
  "source": [
    "aws.secretsmanager"
  ],
  "detail-type": [
    "AWS API Call via CloudTrail"
  ],
  "detail": {
    "eventSource": [
      "secretsmanager.amazonaws.com"
    ],
    "eventName": [
      "DeleteResourcePolicy"
    ]
  }
}
```

Nó sẽ trông như thế này:
![m2](/images/m3/3.1/s6.png)

7. Nhấp vào "Next".



8. Trong bước “Select target(s)”, chọn “Lambda function” từ danh sách thả xuống cho Target 1.



9. Chọn hàm có tên “UpdateSecretPolicyLambdaFunction” và nhấp vào “Add another target”.
![m2](/images/m3/3.1/s9.png)

10. Chọn “SNS topic” từ danh sách thả xuống đầu tiên và tên của SNS topic “ASMWorkshopTopic“  (bạn đã tạo trong Nhiệm vụ-2.2) trong danh sách thả xuống thứ hai.

![m2](/images/m3/3.1/s10.png)

11. Mở rộng "Additional settings" và chọn "Input transformer" từ menu thả xuống.



12. Nhấp vào "Configure input transformer".



13. Cuộn xuống phần "Target input transformer"  và dán đoạn sau vào "Input path" textbox:

```
{"AccessingParty":"$.detail.userIdentity.arn","EventTime":"$.detail.eventTime","Secret":"$.detail.responseElements.aRN"}
```


14. Dán đoạn sau vào "Template" textbox.
```
"The Resource Policy of a secret <Secret> was attempted for deletion by <AccessingParty> on <EventTime>. "
```


15. Nhấp vào "Confirm".



16. Nhấp vào "Next" và tiếp tục nhấp vào "Next" để bỏ qua bước "Configure tags".



17. Cuộn xuống và nhấp vào “Create rule". Khi Rule được tạo, bạn sẽ thấy một thông báo màu xanh lá cây ở đầu màn hình:
![m2](/images/m3/3.1/s17.png)
![m2](/images/m3/3.1/s17b.png)