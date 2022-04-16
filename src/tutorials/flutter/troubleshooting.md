# Troubleshooting

## [core/no-app] No Firebase App '[DEFAULT]' has been created - call Firebase.initializeApp()

[initializing-flutterfire](https://firebase.flutter.dev/docs/overview/#initializing-flutterfire)

```dart
import 'package:flutter/material.dart';

// Import the firebase_core plugin
import 'package:firebase_core/firebase_core.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      // Initialize FlutterFire
      future: Firebase.initializeApp(),
      builder: (context, snapshot) {
        // Check for errors
        if (snapshot.hasError) {
          return SomethingWentWrong();
        }

        // Once complete, show your application
        if (snapshot.connectionState == ConnectionState.done) {
          return MyAwesomeApp();
        }

        // Otherwise, show something whilst waiting for initialization to complete
        return Loading();
      },
    );
  }
}
```

## Cannot run with sound null safety, because the following dependencies don't support null safety:

```bash
dart --no-sound-null-safety run
flutter run --no-sound-null-safety
```

