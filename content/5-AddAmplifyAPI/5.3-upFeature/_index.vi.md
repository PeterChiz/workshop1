---
title : "Triển khai tính năng ứng dụng"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.3 </b> "
---

**Bước 1:** Tạo file lib/features/trip/services/trips_datastore_service.dart và cập nhật nó bằng mã sau để tạo tệp TripsDataStoreService chứa các hàm sau:
- Đoạn code dưới đây định nghĩa một dịch vụ TripsDataStoreService để quản lý dữ liệu chuyến đi trong ứng dụng, dịch vụ này cung cấp các phương thức để lắng nghe các thay đổi trong dữ liệu chuyến đi, thêm, xóa và cập nhật các chuyến đi (hiện tại chỉ có 'thêm') trong DataStore của Amplify.

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

**Bước 2:** Tạo file lib/features/trip/data/trips_repository.dart và cập nhật bằng mã sau:
- Đoạn mã dưới đây định nghĩa một TripsRepository để quản lý dữ liệu chuyến đi trong ứng dụng Flutter sử dụng AWS Amplify và Riverpod. 
- Dịch vụ này cung cấp các phương thức để lấy danh sách các chuyến đi, thêm chuyến đi mới và lấy thông tin chi tiết của một chuyến đi cụ thể. 
- Mình sử dụng Riverpod để quản lý trạng thái và cung cấp dữ liệu cho các widget trong ứng dụng.
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

**Bước 3:** Mở tệp lib/features/trip/controller/trips_list_controller.dart và cập nhật nó bằng mã sau:
- Đoạn code dưới đây cũng định nghĩa một TripsListController để quản lý việc thêm các chuyến đi mới vào ứng dụng Flutter sử dụng AWS Amplify và Riverpod.
- Dịch vụ này cung cấp phương thức để thêm các chuyến đi mới vào DataStore của Amplify
- Sử dụng Riverpod để quản lý trạng thái và cung cấp dữ liệu cho các widget trong ứng dụng
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


