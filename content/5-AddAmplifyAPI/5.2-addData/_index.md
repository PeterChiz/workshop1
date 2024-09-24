---
title : "Add the session data model to the application"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.2 </b> "
---

**Step 1:** Run the command below in the root directory of your application to create the session model file.

```
amplify codegen models
```

The Amplify CLI will generate Dart files in the *lib/models* directory.

![connect](/images/5.AddAmplifyAPI/image3.png)

**Step 2:** Run the `amplify push` command to create the resources in the cloud.
![connect](/images/5.AddAmplifyAPI/image4.png)

**Step 3:** Press **Enter**. The Amplify CLI will deploy the resources and display a confirmation, as shown in the screenshot.
![connect](/images/5.AddAmplifyAPI/image5.png)

**Step 4:** Open the *main.dart* file and update it as below to add the Amplify API plugin to the `_configureAmplify()` function.

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
