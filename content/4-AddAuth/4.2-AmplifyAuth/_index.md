---
title : "Implement the application authentication flow using Amplify Authenticator"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

**Step 1:** Create the file lib/features/trip/ui/trips_list/trips_list_page.dart nd update it with the following code. This will be the home page of the application.

```dart
import 'package:flutter/material.dart';
import 'package:hooks_riverpod/hooks_riverpod.dart';

import 'package:amplify_2/features/trip/data/trips_repository.dart';
import 'package:amplify_2/features/trip/ui/trips_list/trip_card.dart';
import 'package:amplify_2/features/trip/ui/trips_list/add_trip_bottomsheet.dart';
import 'package:amplify_2/common/utils/colors.dart' as constants;

class TripsListPage extends HookConsumerWidget {
  const TripsListPage({
    super.key,
  });

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final Orientation orientation = MediaQuery
        .of(context)
        .orientation;
    final tripListValue = ref.watch(tripsListStreamProvider);
    return Scaffold(
        appBar: AppBar(
          centerTitle: true,
          title: const Text(
            'Amplify Trips Planner',
          ),
          backgroundColor: const Color(constants.primaryColorDark),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
          },
          backgroundColor: const Color(constants.primaryColorDark),
          child: const Icon(Icons.add),
        ),
        body: const Center(
          child: Text('Danh sách chuyến đi'),
        )
    );
  }
}

```

**Step 2:** Create the file lib/trips_planner_app.dart .  Update the file with the following code to create the route for the application’s home page.
- The code below will set up the basic structure to display a list of trips and have a button (bottom/right) to add a new trip. The list of trips and the functionality to add a trip will be implemented in other parts of the application.

```dart
import 'package:amplify_2/features/trip/ui/trips_list/trips_list_page.dart';
import 'package:amplify_authenticator/amplify_authenticator.dart';
import 'package:amplify_2/common/navigation/router/routes.dart';
import 'package:amplify_2/common/utils/colors.dart' as constants;
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

class TripsPlannerApp extends StatelessWidget {
  const TripsPlannerApp({
    required this.isAmplifySuccessfullyConfigured,
    super.key,
  });

  final bool isAmplifySuccessfullyConfigured;
  @override
  Widget build(BuildContext context) {
    final router = GoRouter(
        routes: [
          GoRoute(
              path: '/',
              name: AppRoute.home.name,
              builder: (context, state) => isAmplifySuccessfullyConfigured
                  ? const TripsListPage()
                  : const Scaffold(
                body: Center(
                  child: Text('Đã cố gắng cấu hình Amplify'),
                ),
              )
          )
        ],
        errorBuilder: (context, state) => Scaffold(
          body: Center(
            child: Text(state.error.toString()),
          ),
        )
    );
    return Authenticator(
      child: MaterialApp.router(
        routerConfig: router,
        builder: Authenticator.builder(),
        theme: ThemeData(
          colorScheme:
          ColorScheme.fromSwatch(primarySwatch: constants.primaryColor)
              .copyWith(
            background: const Color(0xff82CFEA),
          ),
        ),
      ),
    );
  }
}
```

**Step 3:** Open the `main.dart` file and update it with the following code. This code contains the Amplify configuration logic for the Auth category.
- The code below is used to initialize and configure AWS Amplify services (AmplifyAuthCognito has been added).

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
  ]);
  await Amplify.configure(amplifyconfig);
}

```

**Step 4:** Use the command below to run the application on your phone, using the authentication flow to create a new account.
```
flutter run
```