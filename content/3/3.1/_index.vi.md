---
title : "Cập nhật Mẫu Ứng dụng"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> Nhiệm vụ-1.1: </b> "
---



### Cập nhật ứng dụng mẫu để truy xuất thông tin xác thực của cơ sở dữ liệu từ AWS Secrets Manager
#### Các bước:
Cập nhật ứng dụng mẫu để truy xuất thông tin xác thực của cơ sở dữ liệu từ AWS Secrets Manager

1. Điều hướng đến [bảng điều khiển dịch vụ Lambda](https://console.aws.amazon.com/lambda).
![1.1](/images/m1/1.1/s1.png)
2. Chọn “Functions” từ bảng điều khiển bên trái. Nhấp vào tên hàm “LambdaRDSTest”. Đây là hàm được sử dụng cho ứng dụng mẫu để kết nối với cơ sở dữ liệu RDS. Hàm này được viết bằng ngôn ngữ Python. Cơ sở dữ liệu chứa dữ liệu mẫu về Tên và Họ.

3. Bạn có thể xem code của ứng dụng mẫu bằng cách nhấp đúp vào “LambdaRDSTest.py” trong phần “Code Source”.

![1.1](/images/m1/1.1/s3a.png)
![1.1](/images/m1/1.1/s3b.png)

```bash
# Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.
# SPDX-License-Identifier: MIT-0
import sys
import pymysql
import boto3
import botocore
import json
import random
import time
import os
from botocore.exceptions import ClientError
conn = None

# rds settings
rds_host = os.environ['RDS_HOST']
username = os.environ['RDS_USERNAME']
db_name = os.environ['RDS_DB_NAME']
password = os.environ['PASSWORD']

def openConnection():
    global conn
    global describe_secret_response_version

    # PRESS ENTER AFTER THIS COMMENT AND PASTE THE COPIED SAMPLE CODE FROM AWS SECRETS MANAGER
    
    
    #secretstring = json.loads(secret)
    #rds_host = secretstring['host']
    #username = secretstring['username']
    #password = secretstring['password']
    #db_name =  secretstring['dbname']
    

    try:
        print("Opening Connection")
        if(conn is None):
            conn = pymysql.connect(host=rds_host, user=username, passwd=password, db=db_name, connect_timeout=5)
            get_describe_secret_response = client.describe_secret(SecretId=secret_name)
            describe_secret_response_version = str(get_describe_secret_response['VersionIdsToStages'])
        elif (not conn.open):
            conn = pymysql.connect(host=rds_host, user=username, passwd=password, db=db_name, connect_timeout=5)
            get_describe_secret_response = client.describe_secret(SecretId=secret_name)
            describe_secret_response_version = str(get_describe_secret_response['VersionIdsToStages'])

    except Exception as e:
        print (e)
        print("ERROR: Unexpected error: Could not connect to MySql instance.")
        raise e


def lambda_handler(event, context):

    try:
        openConnection()
        if(conn.open):
            with conn.cursor() as cur:
                cur.execute("select * from DemoTable")
                records = cur.fetchall()
                p = []
                tbl = "<tr><td>First Name</td><td>Last Name</td></tr>"
                p.append(tbl)
                
                for row in records:
                    a = "<tr><td>%s</td>"%row[1]
                    p.append(a)
                    b = "<td>%s</td></tr>"%row[2]
                    p.append(b)
            
                lst = str(p)
                f=lst.replace("', '", "")
                g=f.replace("[", "")
                h=g.replace("]","")
                x=h.replace("'", "")
                content = "<html><head><style>table, th, td {  border: 1px solid black;}</style><title>AWS Secrets Manager workshop</title></head><body><table>%s</table></body></html>"%(x)
                
                response = {
                    "statusCode": 200,
                    "body": content+describe_secret_response_version,
                    "headers": {
                        'Content-Type': 'text/html' ,
                    }
                }
                return response
    except Exception as e:
        print(e)
        content =  "<html><head><title>AWS Secrets Manager workshop</title></head><body>Database not connected</body></html>"                
        response = {
            "statusCode": 200,
            "body": content,
            "headers": {
                'Content-Type': 'text/html' ,
                
            }
            
        }
        return response
    finally:
        print("Closing Connection")
        if(conn is not None and conn.open):
            conn.close()
```
Hàm openConnection() trong code kết nối với cơ sở dữ liệu MySQL RDS bằng cách sử dụng các tham số được lưu trữ trong Biến Môi Trường (Environment Variables). Khi cơ sở dữ liệu được kết nối, ứng dụng sẽ in ra dữ liệu mẫu.

4. Dán và truy cập API URL mà bạn đã sao chép trước đó (trong phần Event Outputs của CloudFormation stack) trên một tab trình duyệt web riêng. Bạn sẽ thấy thông báo Database not connected.
```
Q: Tại sao ứng dụng không thể kết nối với cơ sở dữ liệu RDS để lấy dữ liệu mẫu?
```
A: Do password đã dc configure để dc dùng từ Amazon Secret Manager
![1.1](/images/m1/1.1/s4.png)
5. Bây giờ, hãy cập nhật code hàm “LambdaRDSTest” để lấy thông tin xác thực củacơ sở dữ liệu từ Secrets Manager thay vì sử dụng Biến Môi Trường. Quay lại tab trình duyệt nơi code LambdaRDSTest.py được mở.

a. Comment 4 dòng code sau (dòng số 15, 16, 17, 18) bằng cách thêm dấu # ở đầu mỗi dòng như hiển thị dưới đây.

b. Dưới mục “Configuration”, nhấp vào “Environment variables”. Bạn sẽ thấy các Biến Môi Trường tương tự như dưới đây:
![1.1](/images/m1/1.1/s5b.png)
c. Xóa tất cả các cặp khóa giá trị (Key Value pairs) cho các Biến Môi Trường:

6. Quay lại mã nguồn trong phần “Code Source”:



7. Nhấp vào “Deploy” để lưu các thay đổi và đợi cho đến khi xuất hiện thông báo sau:

![1.1](/images/m1/1.1/s7.png)

8. Điều hướng đến [bảng điều khiển dịch vụ Secrets Manager](https://console.aws.amazon.com/secretsmanager) .

![1.1](/images/m1/1.1/s8.png)

9. Nhấp vào secret được tạo bởi CloudFormation template. Tên của secret sẽ là “DemoWorkshopSecret“.
![1.1](/images/m1/1.1/s9.png)
Kiểm tra khóa
![1.1](/images/m1/1.1/s9b.png)


10. Cuộn xuống phần “Sample code”. Nhấp vào “Python3”.

![1.1](/images/m1/1.1/s10.png)

```bash
# Use this code snippet in your app.
# If you need more information about configurations
# or implementing the sample code, visit the AWS docs:
# https://aws.amazon.com/developer/language/python/

import boto3
from botocore.exceptions import ClientError


def get_secret():

    secret_name = "DemoWorkshopSecret"
    region_name = "us-east-1"

    # Create a Secrets Manager client
    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )

    try:
        get_secret_value_response = client.get_secret_value(
            SecretId=secret_name
        )
    except ClientError as e:
        # For a list of exceptions thrown, see
        # https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_GetSecretValue.html
        raise e

    secret = get_secret_value_response['SecretString']

    # Your code goes here.
```
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
![1.1](/images/m1/1.1/s16.png)

17. Nhấp vào “Deploy” để lưu các thay đổi và đợi cho đến khi xuất hiện thông báo sau:



18. Truy cập lại API URL trong trình duyệt web của bạn, bạn sẽ thấy dữ liệu mẫu được truy xuất từ cơ sở dữ liệu tương tự như thế này:

Kết quả hiển thị dữ liệu mẫu cũng như Version ID của secret. Khi CloudFormation template được triển khai, secret được cập nhật sau khi nó được tạo lần đầu tiên.
![1.1](/images/m1/1.1/s18.png)
Bạn có thể quan sát trong code hàm Lambda rằng một lệnh gọi API describe_secret được thực hiện khi kết nối với cơ sở dữ liệu được mở:

*get_describe_secret_response = client.describe_secret(SecretId=secret_name)*

Theo [tài liệu Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/secretsmanager/client/describe_secret.html), hàm trả về thông tin chi tiết của một bí mật. Nó không bao gồm giá trị bí mật được mã hóa.