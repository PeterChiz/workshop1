---
title : "Dành cho mac OS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

**Tải xuống Flutter SDK**

- Tải xuống thư mục zip tại [Trang web Flutter.](https://docs.flutter.dev/get-started/install/macos#get-sdk) *flutter_macOS_<-version-number->.zipflutter_macos_arm64_<-version-number->.zip*
    
Hãy đảm bảo tải xuống gói phát hành Flutter chính xác cho chip của máy Mac. Tải xuống tệpcho máy tính xách tay chip Intel hoặc tải xuống tệp cho Apple Silicon.
    
- Giải nén Flutter SDK vào thư mục có tên là *development* trên Desktop của bạn.
    
{{% notice note %}}
Bước thư mục tệp ở trên chỉ là khuyến nghị và tham chiếu này sẽ được sử dụng trong suốt workshop. Bạn cũng có thể di chuyển nó đến bất kỳ thư mục nào khác. Chỉ cần đảm bảo giữ tham chiếu đến nơi thư mục Flutter của bạn được giải nén.
{{% /notice %}}

**Thêm Flutter vào Path**

- Vào thư mục Flutter đã giải nén và sao chép đường dẫn của thư mục đó.
    - Bạn có thể sao chép nó bằng cách nhấp chuột phải vào thư mục Flutter và chọn tùy chọn "Get Info". Thao tác này sẽ mở một cửa sổ có thông tin thư mục. Trong tab *General , hãy kiểm tra Where* information. Chọn toàn bộ văn bản và sao chép.
- Mở terminal và viết lệnh sau để tìm hiểu về loại terminal của bạn:
![connect](/images/2.Prerequiste/image6.png)
![connect](/images/2.Prerequiste/image7.png)

```
 echo $SHELL
```

- Nếu bạn đang sử dụng Bash, hãy viết:

```
open ~/.bash_profile # or open ~/.bashrc
```

- Nếu bạn sử dụng Z shell, hãy viết:

```
open ~/.zshrc
```

- Dán nội dung sau vào tệp dưới dạng một dòng mới:

```
 export PATH="$PATH:[PATH_OF_FLUTTER]/flutter/bin"
```

- Đóng tất cả các thiết bị đầu cuối và mở một thiết bị đầu cuối mới
- Sau đó mở Terminal mới và viết lệnh sau để kiểm tra:

```
flutter doctor
```

