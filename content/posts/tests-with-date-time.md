---
title: "Testing with dates in Dart"
date: 2023-07-05T19:57:26+01:00
draft: false
---

When working with `DateTime` types it can quickly become awkward to keep methods testable.
For example, consider the following code
```dart
  void someMethodWithDate() {
    final today = DateTime.now();

    // code that uses today
  }
```
If we need to test this function for a fixed time, then we would have to inject `DateTime.now()` into the method as an argument.
This gets quite messy, either making it `nullable` and only using it for testing, which feels like a hack
```dart
  void someMethodWithDate(DateTime? time) {
    final today = time ?? DateTime.now();

    // code that uses today
  }
```
or requiring the argument, but then we generate extra bloat whenever calling the method outside of tests
```dart
  void someMethodWithDate(DateTime time) {
    final today = time;

    // code that uses today
  }
```
Neither seem ideal, so we can use the [clock package](https://pub.dev/packages/clock) developed by the Dart team instead.
```dart
  import 'package:clock/clock.dart';

  void someMethodWithDate() {
    final today = clock.now();

    // code that uses today
  }
```
With this in place, we can easily fix dates as needed when writing tests
```dart
  test('some unit test that requires fixed time', () {
    // set up
    final date = DateTime.now();
    final dummyTime = DateTime(date.year, date.month, date.day, 15, 0, 0);

    final result = withClock(
      Clock.fixed(dummyTime),
      () => someClass.someMethodWithDate(),
    );
  });

```