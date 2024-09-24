---
title : "Dành cho Windows"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

**Tải xuống Flutter SDK**

- Tải xuống thư mục zip tại [Trang web Flutter.](https://docs.flutter.dev/get-started/install/windows#get-the-flutter-sdk)
- Giải nén Flutter SDK vào thư mục có tên là *development* trên Desktop của bạn.
{{% notice note %}}
Thư mục tệp ở trên chỉ là khuyến nghị và tham chiếu này sẽ được sử dụng trong suốt workshop Bạn cũng có thể di chuyển nó đến bất kỳ thư mục nào khác. Chỉ cần đảm bảo giữ tham chiếu đến nơi thư mục Flutter của bạn được giải nén.
{{% /notice %}}

> 

**Thêm Flutter vào Path**

- Vào thư mục Flutter đã giải nén và sao chép đường dẫn của thư mục đó.
- Bạn có thể sao chép nó bằng cách nhấp chuột phải vào thư mục và chọn tùy chọn "Copy as Path" hoặc Nhấp vào thanh điều hướng ở đầu cửa sổ và sao chép văn bản đường dẫn từ đó.
![connect](/images/2.Prerequiste/image1.png)

- Nhấp vào biểu tượng Windows ở góc dưới bên trái và tìm **Environment Variables**. Chọn **Edit Environment variables for your account**.
![connect](/images/2.Prerequiste/image2.png)

- Nó sẽ mở ra một cửa sổ với tab Advanced được chọn tại **System Properties**, nhấp vào nút **Environment Variables**...
![connect](/images/2.Prerequiste/image3.png)

- Trên cửa sổ mở ra, tại phần **System variables**, tìm **Path** và nhấp đúp vào đó.
![connect](/images/2.Prerequiste/image4.png)

- Thêm trường mới bằng cách nhấp vào nút **New** ở bên phải và dán đường dẫn bạn đã sao chép trước đó.
![connect](/images/2.Prerequiste/image5.png)

- Lưu và đóng tất cả các cửa sổ
- Đóng bất kỳ Command Prompt nào
- Sau đó mở Command Prompt mới và viết lệnh sau để kiểm tra:
```
flutter doctor
```