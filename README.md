# Integrating AWS Amplify into Flutter Workshop

Đây là dự án workshop về việc tích hợp AWS Amplify vào ứng dụng Flutter. Workshop này cung cấp hướng dẫn từng bước để xây dựng một ứng dụng Flutter có sử dụng các dịch vụ của AWS thông qua Amplify.

## Mục đích

- Học cách tích hợp AWS Amplify vào ứng dụng Flutter
- Xây dựng một ứng dụng mẫu sử dụng các dịch vụ của AWS
- Hiểu cách triển khai các tính năng phổ biến như xác thực, lưu trữ dữ liệu, và thông báo đẩy

## Công nghệ sử dụng

- Flutter
- Dart
- AWS Amplify
- AWS services (Cognito, DynamoDB, S3)

## Cài đặt

1. Cài đặt Flutter và Dart
2. Cài đặt AWS CLI và cấu hình tài khoản AWS
3. Cài đặt Amplify CLI:
   ```
   npm install -g @aws-amplify/cli
   ```
4. Clone repository này:
   ```
   git clone https://github.com/YourUsername/amplify-flutter-workshop.git
   ```
5. Di chuyển vào thư mục dự án và cài đặt các dependencies:
   ```
   cd amplify-flutter-workshop
   flutter pub get
   ```

## Sử dụng

1. Khởi tạo Amplify trong dự án:
   ```
   amplify init
   ```
2. Thêm các dịch vụ AWS cần thiết:
   ```
   amplify add auth
   amplify add api
   amplify add storage
   ```
3. Push các thay đổi lên AWS:
   ```
   amplify push
   ```
4. Chạy ứng dụng Flutter:
   ```
   flutter run
   ```

## Cấu trúc dự án

Mô tả cấu trúc thư mục và file chính của dự án ở đây.
