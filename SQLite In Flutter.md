# SQLite In Flutter

## Steps

1. **Add Dependencies:**  Import  `sqflite`  and  `path`  dependencies to your  `pubspec.yaml`  file. 
https://pub.dev/packages/sqflite
https://pub.dev/packages/path
2. **Setup The Database:** Create a class, such as `DBUtils`, that initializes and creates the database.
https://dart.helpful.codes/tutorials/sqflite/Best-practices-for-using-Sqflite/
3. **Define A Schema:** Create a model class with  `toMap`  and  `fromMap`  methods. The data in SQLite will be saved in Dart Maps data type. The  `toMap`  method converts a  your  object to a Map, and the  `fromMap`  factory constructor converts a Map to a  your  object.
https://dart.helpful.codes/tutorials/sqflite/Best-practices-for-using-Sqflite/
https://docs.flutter.dev/cookbook/persistence/sqlite
4. **Implement CRUD Database Operations:**

## Useful Concepts To Know
### 1. Get Familiar With CRUD Operations:
- **Create**, **Read**, **Update**, and **Delete**. The four basic operations that can be performed on any persistent data storage. These operations often involve asynchronous operations, which is where **Futures** come in.
```dart
Future<void> createData(Data data) async {
  await database.insert('table', data.toMap());
}
```
### 2.  Asynchronous Programming: 
- Get familiar with **Futures** and **async/await** syntax for asynchronous programming.
- A **Future** represents a computation that doesn't complete immediately. Instead, it produces a value sometime in the future. 
- `async`  is used to declare a function that returns a Future
- `await`  is used to pause execution of the function until the Future completes. 
```dart
import 'dart:async';

void main() {
  startTimer();
}

Future<void> startTimer() async {
  print("Timer started");
  
  // Use the 'await' keyword to pause execution for 1 second
  await Future.delayed(Duration(seconds: 1));
  
  print("Timer completed after 1 second");
}
```

### 3.  State Management:
- StatefulWidgets maintain a mutable state over time.
- The  `setState()`  method tells Flutter that the state has changed and the widget needs to be rebuilt.
https://docs.flutter.dev/resources/architectural-overview#widget-state
- Try to avoid calling an empty `setState(){}` 
https://dcm.dev/docs/rules/flutter/avoid-empty-setstate/
	- Causes: Wasted Rebuilds, Performance Impact, Misleading Code, Maintenance Challenges.

### 4.  Navigation: 
- The Navigator maintains a stack of Route objects. 
- Each Route represents a screen in the application. 
- The Navigator provides methods for navigating between screens, `Navigator.push()` and  `Navigator.pop()`. 
https://docs.flutter.dev/cookbook/navigation/navigation-basics
- Routes can communicate with each other where you can pass data to and from screens.
```dart
// In the first page...
// 	Opens the second page and waits to come back to the first page
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const SecondPage()),
);

// In the second page...
// 	Passes 'Hello From The Second Page' to the `result` variable
Navigator.pop(
  context,
  'Hello From The Second Page',
);
```
https://docs.flutter.dev/cookbook/navigation/returning-data

### 5. initState() and FutureBuilders
- `initState()` is the first method called when a widget is created (after the constructor).
	- It's a good place to do initialization that depends on the `BuildContext`, such as creating a `Future`.
- `FutureBuilder` is a widget that builds itself based on the latest snapshot of interaction with a `Future`. It's a great way to work with `Future` and `async` operations.
```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  Future<String> _data;

  @override
  void initState() {
    super.initState();
    _data = fetchData(); // Assume fetchData() returns a Future<String>
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<String>(
      future: _data,
      builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return CircularProgressIndicator();
        } else if (snapshot.hasError) {
          return Text('Error: ${snapshot.error}');
        } else {
          return Text('Data: ${snapshot.data}');
        }
      },
    );
  }
}
```
https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html
