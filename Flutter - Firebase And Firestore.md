# Firebase Firestore In Flutter

## Setup
1. Install Firebase CLI https://firebase.google.com/docs/cli#setup_update_cli
	* If you're on Windows, stereotypically the Firebase CLI gets installed into `C:\Users\YOUR_USERNAME\AppData\Roaming\npm`, don't forget to add Firebase to your path environment variable. https://stackoverflow.com/questions/43592018/windows-10-cant-see-firebase-in-my-path
2. Setup A Firestore Collection
	1. Go to Firebase Console https://console.firebase.google.com/
	2. Create a new Firebase Project
	3. Click `Build > Cloud Firestore > Create Database`
	4. Leave name and location as default, no real reason to change any of that
	5. Click `Start in test mode` for Secure Rules
	6. Click `Start Collection` to make a new collection, give it whatever collection id you want to give it, e.g. `grades`
	7. Create a sample document, e.g. generate an Auto-ID for the document and give it the fields `sid` and `grade` with whatever values. 
3. Open up terminal and enter 
	1. `firebase login`
		* If you experience `firebase command not found`, check your path!  
	2. `flutter create lab07`
	3. `cd lab07`
	4. `dart pub global activate flutterfire_cli`
		* If you experience `flutterfire command not found`, check your path! 
	5. `flutter pub add firebase_core`
	6. `flutter pub add cloud_firestore`
	7. `flutterfire configure` 
4. Open `lib/main.dart` and modify
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
5. Voila! You can now implement Firestore into your app!
	* Dont forget to add the following imports as well as whatever necessary Firestore functions **wherever needed in your code**, e.g.
```dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
```
```dart
// Get Collection
final CollectionReference myCollection = FirebaseFirestore.instance.collection('myCollectionId');
// Get Document
DocumentSnapshot snapshot = await myCollection.doc('collectionDocumentId').get();
// Set Document Data
await counters.doc('collectionDocumentId').set({'value': 1});
```
**(Note this is just example code showing off example interactions with Firestore)**