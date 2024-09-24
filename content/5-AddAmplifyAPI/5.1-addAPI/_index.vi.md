---
title : "Thêm Amplify API vào ứng dụng"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.1 </b> "
---

**Bước 1:** Điều hướng đến thư mục gốc của ứng dụng và cung cấp tài nguyên API Amplify bằng cách chạy lệnh bên dưới trong thiết bị đầu cuối của bạn.

```
amplify add api
```

**Bước 2:** Chọn tùy chọn GraphQL và nhấn **Enter**, Cập nhật các thiết lập được đề xuất như bên dưới. Cuộn lên tùy chọn **Authorization modes** và đổi thành **Amazon Cognito User Pool**. Chọn **No** cho lời nhắc loại xác thực bổ sung. Chọn tùy chọn **Continue**.Phần GrapQL API chọn **Coflict detection: Disabled**, Chọn tiếp **yes**, Phần default resolution strategy chọn **Auto Merge**, Chọn tiếp **Continue**, Chọn mẫu **Blank Schema** và nhấn **Enter**. Chọn **No** để chỉnh sửa lời nhắc lược đồ.
![connect](/images/5.AddAmplifyAPI/image1.png)

Amplify CLI sẽ thêm một thư mục mới cho API, trong đó có chứa `schema.graphql` tệp mà bạn sẽ xác định các mô hình cho ứng dụng.
![connect](/images/5.AddAmplifyAPI/image2.png)

**Bước 3:** Mở tệp *schema.graphql* và thay thế nội dung của tệp bằng nội dung sau để xác định mô hình phiên làm việc
```
type Trip @model @auth(rules: [{ allow: owner }]) {
    id: ID!
    tripName: String!
    destination: String!
    startDate: AWSDate!
    endDate: AWSDate!
    tripImageUrl: String
    tripImageKey: String
}
```