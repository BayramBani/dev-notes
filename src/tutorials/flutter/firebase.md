# Firebase

## Authentication

###  Register user

```dart
final _auth = FirebaseAuth.instance;
***
child: MaterialButton(
  onPressed: () async {
    //Implement registration functionality.
    //print('email: $email ; password: $password');
    try {
      final newUser =
          await _auth.createUserWithEmailAndPassword(
              email: email, password: password);
      if (newUser != null) {
        Navigator.pushNamed(context, ChatScreen.id);
      }
    } catch (e) {
      print(e);
    }
  },
),
```

### SignIn User

```dart
final _auth = FirebaseAuth.instance;
***
child: MaterialButton(
  onPressed: () async {
    //Implement login functionality.
    try {
      final user = await _auth.signInWithEmailAndPassword(
          email: email, password: password);
      if (user != null) {
        Navigator.pushNamed(context, ChatScreen.id);
      }
    } catch (e) {
      print(e);
    }
  },
  child: Text(
    'Log In',
  ),
),
```

### Logout

```dart
final _auth = FirebaseAuth.instance;
User? loggedInUser;

void getCurrentUser() async {
    final user = await _auth.currentUser;
    if (user != null) {
      loggedInUser = user;
      print(loggedInUser!.email);
    }
}
***
IconButton(
    icon: Icon(Icons.close),
    onPressed: () {
      //Implement logout functionality
      _auth.signOut();
      Navigator.pop(context);
}),
```
## Firestore Database

### save to database

```dart
final _firestore = FirebaseFirestore.instance;
final _auth = FirebaseAuth.instance;
late User loggedInUser;
late String messageText;
***   
onPressed: () {
  //Implement send functionality.
  _firestore.collection('messages').add(
      {'text': messageText, 'sender': loggedInUser.email});
},
```

### Fetch data from database

```dart
  void getMessages() async {
    final messages = await _firestore.collection('messages').get();
    for (var message in messages.docs) {
      print(message.data());
    }
  }
***
onPressed: () {
	getMessages();
}
```

stream of data snaphot : database cahges listner

```dart
void messagesStream() async {
  await for (var snapshot in _firestore.collection('messages').snapshots()) {
    for (var message in snapshot.docs) {
      print(message.data());
    }
  }
}
```