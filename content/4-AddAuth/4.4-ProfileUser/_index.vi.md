---
title : "Xem thông tin về người dùng đã đăng ký thông qua Amplify Auth trên AWS Console"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

{{% notice info %}}
Cần truy cập vào dịch vụ Amazon Cognito, vì Amplify Auth sử dụng Cognito làm backend.
{{% /notice %}}

Đây là các bước bạn có thể thực hiện:

1. Đăng nhập vào AWS Console (console.aws.amazon.com).
2. Tìm và chọn dịch vụ "Cognito" trong danh sách dịch vụ.
3. Chọn "Manage User Pools".
4. Tìm và chọn User Pool tương ứng với ứng dụng Amplify của bạn.
![connect](/images/4.AddAuth/image5.png)

5. Trong menu bên trái, chọn "Users pool name" mà bạn đã tạo trước đó.
6. Ở đây, bạn sẽ thấy danh sách tất cả người dùng đã đăng ký.
![connect](/images/4.AddAuth/image6.png)
