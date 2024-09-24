---
title : "Thêm mô hình dữ liệu phiên làm việc vào ứng dụng"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.2 </b> "
---

**Bước 1:** Chạy lệnh bên dưới trong thư mục gốc của ứng dụng để tạo tệp mô hình phiên làm việc.

```
amplify codegen models
```

Amplify CLI sẽ tạo các tệp dart trong *lib/models* như trong thư mục.

![connect](/images/5.AddAmplifyAPI/image3.png)

**Bước 2:** Chạy lệnh `amplify push` để tạo tài nguyên trên đám mây.
![connect](/images/5.AddAmplifyAPI/image4.png)

**Bước 3:** Nhấn **Enter.** Amplify CLI sẽ triển khai các tài nguyên và hiển thị xác nhận, như trong ảnh chụp màn hình.
![connect](/images/5.AddAmplifyAPI/image5.png)

**Bước 4:** Mở *main.dart* file và cập nhật như bên dưới để thêm plugin Amplify API vào hàm  `_configureAmplify()`.

```dart
import 'package:amplify_2/trips_planner_app.dart';
import 'package:amplify_api/amplify_api.dart';
import 'package:amplify_auth_cognito/amplify_auth_cognito.dart';
import 'package:amplify_flutter/amplify_flutter.dart';
import 'package:amplify_storage_s3/amplify_storage_s3.dart';
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'amplifyconfiguration.dart';

import 'package:amplify_api/amplify_api.dart';
import 'package:amplify_datastore/amplify_datastore.dart';
import 'package:amplify_2/models/ModelProvider.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  bool isAmplifySuccessfullyConfigured = false;
  try {
    await _configureAmplify();
    isAmplifySuccessfullyConfigured = true;
  } on AmplifyAlreadyConfiguredException {
    debugPrint('Amplify configuration failed.');
  }

  runApp(
    ProviderScope(
        child: TripsPlannerApp(
            isAmplifySuccessfullyConfigured: isAmplifySuccessfullyConfigured)),
  );
}

Future<void> _configureAmplify() async {
  await Amplify.addPlugins([
    AmplifyAuthCognito(),
    AmplifyDataStore(modelProvider: ModelProvider.instance),
    AmplifyAPI(),
  ]);
  await Amplify.configure(amplifyconfig);
}

```
