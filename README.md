# multiple_stream_builder

Flutter widgets for avoiding nested StreamBuilder

## Usage example

```dart
var stream1 = Stream<int>.periodic(Duration(seconds: 1));
var stream2 = Stream<int>.periodic(Duration(seconds: 2));
var stream3 = Stream<int>.periodic(Duration(seconds: 3));

// Instead of writing out nested stream builders
Widget build(BuildContext context) {
  return StreamBuilder<int>(
    stream: stream1,
    initialData: 0,
    builder: (context, snapshot1) {
      return StreamBuilder<int>(
        stream: stream2,
        initialData: 0,
        builder: (context, snapshot2) {
          return StreamBuilder<int>(
            stream: stream3,
            initialData: 0,
            builder: (context, snapshot3) {
              return Text(
                'stream1: ${snapshot1.data} - stream2: ${snapshot2.data} - stream3: ${snapshot3.data}',
              );
            },
          );
        },
      );
    },
  );
}

// Pass multiple streams into a single StreamBuilder
Widget build(BuildContext context) {
  return StreamBuilder3<int, int, int>(
    streams: Tuple3(stream1, stream2, stream3),
    initialData: Tuple3(0, 0, 0),
    builder: (context, snapshots) {
      return Text(
        'stream1: ${snapshots.item1.data} - stream2: ${snapshots.item2.data} - stream3: ${snapshots.item3.data}',
      );
    },
  );
}
```