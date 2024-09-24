---
title : "Thêm danh mục xác thực Amplify vào ứng dụng"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

**Bước 1:** Điều hướng đến thư mục gốc của ứng dụng và chạy lệnh bên dưới trong terminal của bạn.

```
amplify add auth
```

**Bước 2:** Chọn tùy chọn **Default configuration** và sau đó chọn **Email** làm phương thức đăng nhập. Sau đó chọn tùy chọn **No, I am done**.

```
Using service: Cognito, provided by: awscloudformation
 The current configured provider is Amazon Cognito. 
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? Email
 Do you want to configure advanced settings? No, I am done.
✅ Successfully added auth resource memorymatchgame28e6d925 locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

**Bước 3:** Bây giờ danh mục Amplify Auth đã sẵn sàng. Chạy lệnh `amplify push` để tạo tài nguyên trên đám mây.
![connect](/images/3.CreateProject/image5.png)

**Bước 4:** Nhấn Enter. Amplify CLI sẽ triển khai các tài nguyên xác thực và hiển thị xác nhận, như trong ảnh chụp màn hình.
![connect](/images/3.CreateProject/image6.png)
