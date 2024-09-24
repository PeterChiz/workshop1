---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

Bây giờ bạn đã hoàn tất hướng dẫn này, hãy làm theo các bước dưới đây để xóa tài nguyên AWS nhằm tránh phát sinh chi phí bất ngờ

Truy cập giao diện Amplify [console.aws.amazon.com/amplify/apps](http://console.aws.amazon.com/amplify/apps)

**Bước 1:**  Điều hướng đến thư mục gốc của ứng dụng và chạy lệnh bên dưới trong terminal của bạn.

```
amplify delete
```

**Bước 2:** Giả sử ứng dụng của mình có tên là amplify4, Mở AWS Amplify sau đó chọn Ứng dụng amplify4, chọn View app
![connect](/images/7.Clean/image1.png)

**Bước 3:** Chọn App settings → chọn General settings → chọn Manage backends
![connect](/images/7.Clean/image2.png)

**Bước 4:** Chọn Actions ở phía bên trên → chọn delete app, đợi khoảng 1 phút
![connect](/images/7.Clean/image3.png)

## **Chúc mừng bạn đã xóa thành công các tài nguyên**