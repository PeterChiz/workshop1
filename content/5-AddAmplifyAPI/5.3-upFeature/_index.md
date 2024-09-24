---
title : "Deploy the application features"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.3 </b> "
---

**Step 1:** Create the file lib/features/trip/services/trips_datastore_service.dart and update it with the following code to create the TripsDataStoreService file containing the following functions:
- This code defines a TripsDataStoreService to manage trip data in the application. This service provides methods to listen for changes in trip data, add, delete, and update trips (currently only 'add') in Amplify's DataStore.
```dart
import 'dart:async';

import 'package:amplify_flutter/amplify_flutter.dart';
import 'package:amplify_2/models/ModelProvider.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

final tripsDataStoreServiceProvider = Provider<TripsDataStoreService>((ref) {
  final service = TripsDataStoreService();
  return service;
});

class TripsDataStoreService {
  TripsDataStoreService();

  Stream<List<Trip>> listenToTrips() {
    return Amplify.DataStore.observeQuery(
      Trip.classType,
      sortBy: [Trip.STARTDATE.ascending()],
    )
        .map((event) => event.items
            .where((element) =>
                element.endDate.getDateTime().isAfter(DateTime.now()))
            .toList())
        .handleError(
      (error) {
        debugPrint('listenToTrips: A Stream error happened');
      },
    );
  }

  Stream<List<Trip>> listenToPastTrips() {
    return Amplify.DataStore.observeQuery(
      Trip.classType,
      sortBy: [Trip.STARTDATE.ascending()],
    )
        .map((event) => event.items
        .where((element) =>
        element.endDate.getDateTime().isBefore(DateTime.now()))
        .toList())
        .handleError(
          (error) {
        debugPrint('listenToTrips: A Stream error happened');
      },
    );
  }

  Stream<Trip> getTripStream(String id) {
    final tripStream = Amplify.DataStore.observeQuery(Trip.classType, where: Trip.ID.eq(id)).map((event) => event.items.toList().single);
    return tripStream;
  }

  Future<void> addTrip(Trip trip) async {
    try {
      await Amplify.DataStore.save(trip);
    } on Exception catch (error) {
      debugPrint(error.toString());
    }
  }

  Future<void> deleteTrip(Trip trip) async {
    try {
      await Amplify.DataStore.delete(trip);
    } on Exception catch (error) {
      debugPrint(error.toString());
    }
  }

  Future<void> updateTrip(Trip updatedTrip) async {
    try {
      final tripsWithId = await Amplify.DataStore.query(Trip.classType, where: Trip.ID.eq(updatedTrip.id),);

      final oldTrip = tripsWithId.first;
      final newTrip = oldTrip.copyWith(tripName: updatedTrip.tripName,
      destination: updatedTrip.destination,
        startDate: updatedTrip.startDate,
        endDate: updatedTrip.endDate,
        tripImageKey: updatedTrip.tripImageKey,
        tripImageUrl: updatedTrip.tripImageUrl,
      );
      await Amplify.DataStore.save(newTrip);
    } on Exception catch (error) {
      debugPrint(error.toString());
    }
  }
}

```

**Step 2:** Create the file lib/features/trip/data/trips_repository.dart and update it with the following code:
- The code below defines a TripsRepository to manage trip data in the Flutter application using AWS Amplify and Riverpod.
- This service provides methods to retrieve the list of trips, add new trips, and get detailed information about a specific trip.
- We use Riverpod to manage state and provide data to widgets in the application.
```dart
import 'package:amplify_2/features/trip/services/trips_datastore_service.dart';
import 'package:amplify_2/models/Trip.dart';
import 'package:hooks_riverpod/hooks_riverpod.dart';

final tripsRepositoryProvider = Provider<TripsRepository>((ref) {
   TripsDataStoreService tripsDataStoreService =
      ref.read(tripsDataStoreServiceProvider);
  return TripsRepository(tripsDataStoreService);
});

final tripsListStreamProvider = StreamProvider.autoDispose<List<Trip?>>((ref){
  final tripsRepository = ref.watch(tripsRepositoryProvider);
  return tripsRepository.getTrips();
});


class TripsRepository {
  TripsRepository(this.tripsDataStoreService);

  final TripsDataStoreService tripsDataStoreService;

  Stream<List<Trip>> getTrips() {
    return tripsDataStoreService.listenToTrips();
  }

  Future<void> add(Trip trip) async {
    return tripsDataStoreService.addTrip(trip);
  }

  Stream<Trip> get(String id) {
    return tripsDataStoreService.getTripStream(id);
  }
}


```

**Step 3:** Open the file lib/features/trip/controller/trips_list_controller.dart and update it with the following code:
- The code below also defines a TripsListController to manage the addition of new trips to the Flutter application using AWS Amplify and Riverpod.
- This service provides a method to add new trips to Amplify's DataStore.
- It uses Riverpod to manage state and provide data to widgets in the application.
Copy

```dart
import 'package:amplify_flutter/amplify_flutter.dart';
import 'package:amplify_2/features/trip/data/trips_repository.dart';
import 'package:amplify_2/models/ModelProvider.dart';
import 'package:hooks_riverpod/hooks_riverpod.dart';

final tripsListControllerProvider = Provider<TripsListController>((ref) {
  return TripsListController(ref);
});

class TripsListController {
  TripsListController(this.ref);

  final Ref ref;

  Future<void> add({
    required String name,
    required String destination,
    required String startDate,
    required String endDate,
  }) async {
    final trip = Trip(
      tripName: name,
      destination: destination,
      startDate: TemporalDate(DateTime.parse(startDate)),
      endDate: TemporalDate(DateTime.parse(endDate)),
    );

    final tripsRepository = ref.read(tripsRepositoryProvider);

    await tripsRepository.add(trip);
  }
}

```


