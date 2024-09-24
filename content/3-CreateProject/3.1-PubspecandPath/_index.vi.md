---
title : "Cấu hình file pubspec.yaml và các đường dẫn"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.1 </b> "
---

{{% notice tip %}}
Vì Amplify luôn luôn cập nhật các phiên bản mới nhất và phiên bản mới nhất lại có thể xung đột với các package khác nên phải cài đúng phiên bản để chạy ứng dụng được thuận lợi.
{{% /notice %}}

- Thêm các thư viện sau:

```
version: 1.0.0+1

environment:
  sdk: ^3.5.1

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.8
  amplify_api: ^2.4.0
  amplify_auth_cognito: ^2.4.0
  amplify_authenticator: ^2.1.2
  amplify_datastore: ^2.4.0
  amplify_flutter: ^2.4.0
  amplify_storage_s3: ^2.4.0
  cached_network_image: ^3.4.0
  flutter_hooks: ^0.20.5
  flutter_riverpod: ^2.5.1
  go_router: ^14.2.7
  hooks_riverpod: ^2.5.2
  image_picker: ^1.1.2
  intl: ^0.19.0
  file_picker: ^8.0.7
  timelines: ^0.1.0
  url_launcher: ^6.3.0

dev_dependencies:
  flutter_lints: ^4.0.0

  flutter_test:
    sdk: flutter

flutter:
#tạo một thư mục hình ảnh tên là images, bỏ một ảnh vào thư viện
  uses-material-design: true
  assets:
    - images/amplify.png

```
{{% notice tip %}}
Vì hay có sự xung đột giữa các phiên bản Amplify, Dart và Flutter nên mình sẽ cấu hình sẵn các file sau nếu các bạn có bị lỗi.{{% /notice %}}
- Đối với android
    - Cấu hình file android/app/build.gradle
    
    ```
    plugins {
        id "com.android.application"
        id "kotlin-android"
        // The Flutter Gradle Plugin must be applied after the Android and Kotlin Gradle plugins.
        id "dev.flutter.flutter-gradle-plugin"
    }
    
    android {
        namespace = "com.example.nameapp"
        compileSdk = flutter.compileSdkVersion
        ndkVersion = flutter.ndkVersion
    
        compileOptions {
            sourceCompatibility = JavaVersion.VERSION_1_8
            targetCompatibility = JavaVersion.VERSION_1_8
        }
    
        kotlinOptions {
            jvmTarget = '1.8'
            freeCompilerArgs += [
                    '-Xskip-metadata-version-check'
            ]
        }
    
        defaultConfig {
            // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
            applicationId = "com.example.nameapp"
            // You can update the following values to match your application needs.
            // For more information, see: https://flutter.dev/to/review-gradle-config.
            minSdkVersion 24
            targetSdk = flutter.targetSdkVersion
            versionCode = flutter.versionCode
            versionName = flutter.versionName
        }
    
        buildTypes {
            release {
                // TODO: Add your own signing config for the release build.
                // Signing with the debug keys for now, so `flutter run --release` works.
                signingConfig = signingConfigs.debug
            }
        }
    }
    
    flutter {
        source = "../.."
    }
    
    ```
    
    - Cấu hình file android/settings.gradle
    
    ```
    pluginManagement {
        def flutterSdkPath = {
            def properties = new Properties()
            file("local.properties").withInputStream { properties.load(it) }
            def flutterSdkPath = properties.getProperty("flutter.sdk")
            assert flutterSdkPath != null, "flutter.sdk not set in local.properties"
            return flutterSdkPath
        }()
    
        includeBuild("$flutterSdkPath/packages/flutter_tools/gradle")
    
        repositories {
            google()
            mavenCentral()
            gradlePluginPortal()
        }
    }
    
    plugins {
        id "dev.flutter.flutter-plugin-loader" version "1.0.0"
        id "com.android.application" version "7.3.0" apply false
        id "org.jetbrains.kotlin.android" version "2.0.20" apply false
    }
    
    include ":app"
    
    ```
    
- Đối với IOS:
    - Tạo file có tên là `Podfile`
    
    ```
    # Uncomment this line to define a global platform for your project
    platform :ios, '13.5'
    
    # CocoaPods analytics sends network stats synchronously affecting flutter build latency.
    ENV['COCOAPODS_DISABLE_STATS'] = 'true'
    
    project 'Runner', {
      'Debug' => :debug,
      'Profile' => :release,
      'Release' => :release,
    }
    
    def flutter_root
      generated_xcode_build_settings_path = File.expand_path(File.join('..', 'Flutter', 'Generated.xcconfig'), __FILE__)
      unless File.exist?(generated_xcode_build_settings_path)
        raise "#{generated_xcode_build_settings_path} must exist. If you're running pod install manually, make sure flutter pub get is executed first"
      end
    
      File.foreach(generated_xcode_build_settings_path) do |line|
        matches = line.match(/FLUTTER_ROOT\=(.*)/)
        return matches[1].strip if matches
      end
      raise "FLUTTER_ROOT not found in #{generated_xcode_build_settings_path}. Try deleting Generated.xcconfig, then run flutter pub get"
    end
    
    require File.expand_path(File.join('packages', 'flutter_tools', 'bin', 'podhelper'), flutter_root)
    
    flutter_ios_podfile_setup
    
    target 'Runner' do
      use_frameworks!
      use_modular_headers!
    
      flutter_install_all_ios_pods File.dirname(File.realpath(__FILE__))
    end
    
    post_install do |installer|
      installer.pods_project.targets.each do |target|
        flutter_additional_ios_build_settings(target)
      end
    end
    
    ```
    
- Tạo thư mục mẫu như sau:
![connect](/images/3.CreateProject/image1.png)
- Tạo file lib/common/navigation/router/routes.dart
    
```dart
enum AppRoute {
    home,
    trip,
    editTrip,
}

```
    
- Tạo file lib/common/utils/colors.dart

```dart
import 'package:flutter/material.dart';

const Map<int, Color> primarySwatch = {
  50: Color.fromRGBO(255, 207, 68, .1),
  100: Color.fromRGBO(255, 207, 68, .2),
  200: Color.fromRGBO(255, 207, 68, .3),
  300: Color.fromRGBO(255, 207, 68, .4),
  400: Color.fromRGBO(255, 207, 68, .5),
  500: Color.fromRGBO(255, 207, 68, .6),
  600: Color.fromRGBO(255, 207, 68, .7),
  700: Color.fromRGBO(255, 207, 68, .8),
  800: Color.fromRGBO(255, 207, 68, .9),
  900: Color.fromRGBO(255, 207, 68, 1),
};
const MaterialColor primaryColor = MaterialColor(0xFFFFCF44, primarySwatch);
const int primaryColorDark = 0xFFFD9725;

```

