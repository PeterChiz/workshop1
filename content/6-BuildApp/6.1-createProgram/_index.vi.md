---
title : "Tạo ứng dụng lập kế hoạch chuyến đi cơ bản cơ bản"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---

Các đoạn code dưới đây sẽ tạo front end cho ứng dụng bạn có thể thay đổi các đoạn code này theo ý bạn thích

**Bước 1:** Tạo tệp lib/features/trip/ui/trips_list/add_trip_bottomsheet.dart và cập nhật nó bằng mã sau:

```dart
import 'package:amplify_2/features/trip/controller/trips_list_controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:hooks_riverpod/hooks_riverpod.dart';
import 'package:intl/intl.dart';

class AddTripBottomSheet extends HookConsumerWidget {
  AddTripBottomSheet({
    super.key,
  });

  final formGlobalKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final tripNameController = useTextEditingController();
    final destinationController = useTextEditingController();
    final startDateController = useTextEditingController();
    final endDateController = useTextEditingController();

    return Form(
      key: formGlobalKey,
      child: Container(
        padding: EdgeInsets.only(
          top: 15,
          left: 15,
          right: 15,
          bottom: MediaQuery.of(context).viewInsets.bottom + 15,
        ),
        width: double.infinity,
        child: Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            TextFormField(
              controller: tripNameController,
              keyboardType: TextInputType.name,
              autofocus: true,
              autocorrect: false,
              decoration: const InputDecoration(hintText: 'Tên chuyến đi'),
              textInputAction: TextInputAction.next,
              validator: (value) {
                const validatorError = "Vui lòng nhập chuyến đi";
                if (value == null || value.isEmpty) {
                  return validatorError;
                }
                return null;
              },
            ),
            const SizedBox(
              height: 20,
            ),
            TextFormField(
              keyboardType: TextInputType.name,
              controller: destinationController,
              autofocus: true,
              autocorrect: false,
              decoration: const InputDecoration(hintText: "Mô tả chuyến đi"),
              textInputAction: TextInputAction.next,
              validator: (value) {
                if (value == null || value.isNotEmpty) {
                  return null;
                } else {
                  return 'Vui lòng nhập mô tả chuyến đi';
                }
              },
            ),
            TextFormField(
              keyboardType: TextInputType.datetime,
              controller: startDateController,
              autofocus: true,
              autocorrect: false,
              decoration: const InputDecoration(hintText: "Ngày bắt đầu"),
              textInputAction: TextInputAction.next,
              validator: (value) {
                if (value != null && value.isNotEmpty) {
                  return null;
                } else {
                  return 'Vui lòng nhập ngày bắt đầu';
                }
              },
              onTap: () async {
                DateTime? pickedDate = await showDatePicker(
                  context: context,
                  initialDate: DateTime.now(),
                  firstDate: DateTime(2024),
                  lastDate: DateTime(2100),
                );

                if (pickedDate != null) {
                  String formattedDate =
                  DateFormat('yyyy-MM-dd').format(pickedDate);
                  startDateController.text = formattedDate;
                } else {}
              },
            ),
            TextFormField(
              keyboardType: TextInputType.datetime,
              controller: endDateController,
              autofocus: true,
              autocorrect: false,
              decoration: const InputDecoration(hintText: "Ngày kết thúc"),
              textInputAction: TextInputAction.next,
              validator: (value) {
                if (value != null && value.isNotEmpty) {
                  return null;
                } else {
                  return 'Vui lòng nhập ngày kết thúc';
                }
              },
              onTap: () async {
                if (startDateController.text.isNotEmpty) {
                  DateTime? pickedDate = await showDatePicker(
                    context: context,
                    initialDate: DateTime.parse(startDateController.text),
                    firstDate: DateTime.parse(startDateController.text),
                    lastDate: DateTime(2100),
                  );
                  if (pickedDate != null) {
                    String formattedDate =
                    DateFormat('yyyy-MM-dd').format(pickedDate);
                    endDateController.text = formattedDate;
                  }
                }
              },
            ),
            const SizedBox(
              height: 20,
            ),
            TextButton(
              child: const Text('OK'),
              onPressed: () async {
                final currentState = formGlobalKey.currentState;
                if (currentState == null) {
                  return;
                }
                if (currentState.validate()) {
                  ref.read(tripsListControllerProvider).add(
                      name: tripNameController.text,
                      destination: destinationController.text,
                      startDate: startDateController.text,
                      endDate: endDateController.text);
                  Navigator.of(context).pop();
                }
              },
            ),
          ],
        ),
      ),
    );
  }
}

```
**Bước 2:** Tạo tệp lib/features/trip/ui/trips_list/trip_card.dart và cập nhật nó bằng mã sau:

```dart
import 'package:amplify_2/common/navigation/router/routes.dart';
import 'package:amplify_2/models/ModelProvider.dart';
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';
import 'package:cached_network_image/cached_network_image.dart';
import 'package:intl/intl.dart';
import 'package:amplify_2/common/utils/colors.dart' as constants;

class TripCard extends StatelessWidget {
  const TripCard({super.key, required this.trip, this.imageUrl});

  final Trip trip;
  final String? imageUrl;

  @override
  Widget build(BuildContext context) {
    return InkWell(
      splashColor: Theme.of(context).primaryColor,
      borderRadius: BorderRadius.circular(15),
      onTap: () {
        context.goNamed(
          AppRoute.trip.name,
          pathParameters: {'id': trip.id},
        );
      },
      child: Card(
        clipBehavior: Clip.antiAlias,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(15),
        ),
        elevation: 5.0,
        child: Column(
          children: [
            Expanded(
              child: Container(
                height: 500,
                alignment: Alignment.center,
                color: const Color(constants.primaryColorDark),
                child: Stack(
                  children: [
                    Positioned.fill(
                      child: trip.tripImageUrl != null
                          ? Stack(children: [
                              const Center(
                                child: CircularProgressIndicator(),
                              ),
                              CachedNetworkImage(
                                errorWidget: (context, url, dynamic error) =>
                                    const Icon(Icons.error_outline_outlined),
                                imageUrl: trip.tripImageUrl!,
                                cacheKey: trip.tripImageKey,
                                width: double.maxFinite,
                                height: 500,
                                alignment: Alignment.topCenter,
                                fit: BoxFit.fill,
                              )
                            ])
                          : Image.asset(
                              'images/amplify.png',
                              fit: BoxFit.contain,
                            ),
                    ),
                    Positioned(
                        bottom: 16,
                        left: 16,
                        right: 16,
                        child: FittedBox(
                          fit: BoxFit.scaleDown,
                          alignment: Alignment.centerLeft,
                          child: Text(
                            trip.destination,
                            style: Theme.of(context)
                                .textTheme
                                .headlineSmall!
                                .copyWith(
                                  color: Colors.white,
                                ),
                          ),
                        ))
                  ],
                ),
              ),
            ),
            Padding(
                padding: const EdgeInsets.fromLTRB(2, 8, 8, 4),
                child: DefaultTextStyle(
                    softWrap: false,
                    overflow: TextOverflow.ellipsis,
                    style: Theme.of(context).textTheme.titleMedium!,
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        Padding(
                          padding: const EdgeInsets.only(bottom: 8),
                          child: Text(
                            trip.tripName,
                            style: Theme.of(context)
                                .textTheme
                                .titleMedium!
                                .copyWith(color: Colors.black54),
                          ),
                        ),
                        Text(
                          DateFormat('dd MMM, yyyy')
                              .format(trip.startDate.getDateTime()),
                          style: const TextStyle(fontSize: 12),
                        ),
                        Text(
                          DateFormat('dd MMM, yyyy')
                              .format(trip.endDate.getDateTime()),
                          style: const TextStyle(fontSize: 12),
                        ),
                      ],
                    ))),
          ],
        ),
      ),
    );
  }
}

```

**Bước 3:** Quay lại tệp lib/features/trip/ui/trips_list/trips_list_page.dart và cập nhật nó bằng mã sau:

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

  void showAddTripDialog(BuildContext context) async {
    await showModalBottomSheet(
        isScrollControlled: true,
        elevation: 5,
        context: context,
        builder: (BuildContext context) {
          return AddTripBottomSheet();
        },
    );
  }

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
            showAddTripDialog(context);
          },
          backgroundColor: const Color(constants.primaryColorDark),
          child: const Icon(Icons.add),
        ),
        body: tripListValue.when(
            data: (trips) =>
            trips.isEmpty
                ? const Center(
              child: Text("Chưa có kế hoạch"),
            )
                : Column(
              children: [
                Flexible(
                    child: GridView.count(
                      crossAxisCount:
                      (orientation == Orientation.portrait) ? 2 : 3,
                      mainAxisSpacing: 4,
                      crossAxisSpacing: 4,
                      padding: const EdgeInsets.all(4),
                      childAspectRatio:
                      (orientation == Orientation.portrait) ? 0.9 : 1.4,
                      children: trips.map((tripData) {
                        return TripCard(trip: tripData!);
                      }).toList(),
                    ))
              ],
            ),
            error: (e, st) =>
            const Center(
              child: Text('Error'),
            ),
            loading: () =>
            const Center(
              child: CircularProgressIndicator(),
            )));
  }
}

```
