# Firebase Firestore In Flutter

## Setup
1. Install Firebase CLI https://firebase.google.com/docs/cli#setup_update_cli
2. Open up terminal and enter 
	1. `firebase login`
	2. `flutter create lab07`
	3. `cd lab07`
	4. `dart pub global activate flutterfire_cli`
	6. `flutter pub add firebase_core`
	7. `flutter pub add cloud_firestore`
3. Go to Firebase Console https://console.firebase.google.com/
4. Create a new Firebase Project
5. Click `Build > Cloud Firestore`
6. Make a new collection 
7. Open up terminal and enter
	1. `flutterfire configure`
8. Open `lib/main.dart` modify
 ```dart
void main() async {
	runApp(const MyApp()); 
}
``` 
into
```dart
Future<void> main() async {
	WidgetsFlutterBinding.ensureInitialized();
	await Firebase.initializeApp( options: DefaultFirebaseOptions.currentPlatform, ); 
	runApp(const MyApp()); 
}
``` 
9. Add the following imports
```dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
```
10. Add code to interact with Firestore, e.g.
```dart
// Get Collection
final CollectionReference myCollection = FirebaseFirestore.instance.collection('myCollection');
// Get Document
DocumentSnapshot snapshot = await myCollection.doc('collectionDocument').get();
// Set Document Data
await counters.doc('collectionDocument').set({'value': 1});
```
11. Voila!
