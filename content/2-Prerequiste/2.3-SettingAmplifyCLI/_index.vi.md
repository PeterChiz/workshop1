---
title : "Tạo người dùng IAM"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

**Cài đặt Amplify CLI**
- Cài đặt cURL nếu bạn chưa từ Trang web chính thức 
- Chạy các lệnh sau để cài đặt Amplify CLI
- Mac và Linux:

```
curl -sL https://aws-amplify.github.io/amplify-cli/install | bash && $SHELL
```

  - Windows:
```
curl -sL https://aws-amplify.github.io/amplify-cli/install-win -o install.cmd && install.cmd
```

**Cấu hình Amplify**
- CLI Amplify yêu cầu người dùng IAM có quyền chính sách phù hợp để tương tác với tài khoản AWS. Lệnh này sẽ hướng dẫn qua quy trình tạo người dùng mới trong tài khoản AWS và lưu trữ thông tin xác thực hồ sơ người dùng trong môi trường cục bộ. Các lệnh trong tương lai sẽ chạy với CLI sẽ sử dụng các thông tin đăng nhập này để thực hiện các hành động mà yêu cầu amplify configure.

```
amplify configure
```
- *amplify configure* sẽ yêu cầu bạn đăng nhập vào Bảng điều khiển AWS.

- Sau khi bạn đăng nhập, Amplify CLI sẽ yêu cầu bạn tạo người dùng IAM. Chọn khu vực mà bạn muốn và làm theo hướng dẫn.

```
Specify the AWS Region
? region:  # Your preferred region
Follow the instructions at
https://docs.amplify.aws/cli/start/install/#configure-the-amplify-cli

to complete the user creation in the AWS console
https://console.aws.amazon.com/iamv2/home#/users/create
```

**Tạo người dùng IAM**

- Điều hướng đến nút [Trang tạo người dùng IAM](https://console.aws.amazon.com/iamv2/home#/users/create) nếu nó chưa mở.

- Nhập Tên người dùng và chọn **Next**. Bạn có thể đặt tên người dùng là gì cũng được nhưng mình sẽ gọi nó là `amplify-dev`.
![connect](/images/2.Prerequiste/image8.png)

- Chọn **Attach policies directly** và chọn **AdministratorAccess-Amplify** làm Permissions policy. Chọn **Next**.
![connect](/images/2.Prerequiste/image9.png)

- Trên trang **Review**, hãy kiểm tra xem mọi thứ có ổn không và chọn **Create user**.
![connect](/images/2.Prerequiste/image10.png)

- Thao tác này sẽ chuyển hướng đến trang danh sách người dùng. Chọn người dùng bạn vừa tạo.
![connect](/images/2.Prerequiste/image11.png)

- Trên trang chi tiết người dùng, điều hướng đến tab **Security credentials**, cuộn xuống **Access keys** và chọn **Create access keys**.
![connect](/images/2.Prerequiste/image12.png)

- Trên trang tiếp theo, chọn **Command Line Interface**, xác nhận cảnh báo và chọn **Next**.
![connect](/images/2.Prerequiste/image13.png)

- Trên trang tiếp theo, chọn **Create access key**.
![connect](/images/2.Prerequiste/image14.png)

- Sau đó, bạn sẽ thấy một trang có khóa truy cập cho người dùng. Sử dụng biểu tượng sao chép để sao chép các giá trị này vào khay nhớ tạm, chọn nút **Done**, sau đó quay lại CLI Khuếch đại.
![connect](/images/2.Prerequiste/image15.png)


## **Nhập khóa truy cập và khóa truy cập bí mật**

- Nhập các giá trị bạn vừa sao chép vào lời nhắc CLI tương ứng. Sử dụng làm tên hồ sơ `AmplifyWorkshop`

```
Enter the access key of the newly created user:
? accessKeyId:  # YOUR_ACCESS_KEY_ID
? secretAccessKey:  # YOUR_SECRET_ACCESS_KEY
This would update/create the AWS Profile in your local machine
? Profile Name:  # (default)

Successfully set up the new user.
```


  
