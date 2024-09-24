---
title : "Kết nối với AWS Amplify"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.2 </b> "
---

**Bước 1:** Điều hướng đến thư mục gốc của ứng dụng và cung cấp chương trình phụ trợ Amplify cho ứng dụng bằng cách chạy lệnh bên dưới trong thiết bị đầu cuối của bạn.

```
amplify init
```

**Bước 2:** Nhập tên cho dự án Amplify hoặc chấp nhận tên được đề xuất và nhấn **Enter.**

```
? Enter a name for the project memorymatchgame
The following configuration will be applied:
Project information
| Name: memorymatchgame
| Environment: dev
| Default editor: Visual Studio Code
| App type: flutter
| Configuration file location: ./lib/
? Initialize the project with the above configuration? (Y/n)
```

Đối với người dùng android studio:
![connect](/images/3.CreateProject/image2.png)
**Bước 3:** Nhấn **Enter** lần nữa để chấp nhận các tùy chọn tự động tạo và chọn phương thức Xác thực AWS. Trong ví dụ này, mình đang sử dụng cấu hình AWS. Amplify CLI sẽ khởi tạo phần phụ trợ và kết nối dự án với đám mây.

- Đối với người dùng Visual Studio code:
![connect](/images/3.CreateProject/image3.png)
- Amplify CLI sẽ thêm một thư mục mới có tên `amplify` là thư mục gốc của ứng dụng, chứa dự án amplify và thông tin chi tiết về backend. Và nó cũng sẽ thêm một dartfile (*amplifyconfiguration.dart*) mới vào lib/. Ứng dụng sẽ sử dụng tệp này để biết cách tiếp cận các tài nguyên backend được cung cấp của bạn khi chạy.
![connect](/images/3.CreateProject/image4.png)
