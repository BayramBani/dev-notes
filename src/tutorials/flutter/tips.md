# Tips

## Android Studio shortcuts

- Hot Reload : Ctrl + S
- Hot Restart : Maj + F10
- Show doc : Ctrl + Q

## Reuse widgets

### Extract widget

Android studio => Flutter outline => (select widget) => Extract Widget => (give a name)

### Constants

> register.dart

```
TextField(
  onChanged: (value) {
    //Do something with the user input.
  },
  decoration: kInputDecoration.copyWith(hintText: 'enter your email'),
),
```

> constants.dart

```dart
const kInputDecoration = InputDecoration(
  hintText: '', // @Note Replace this with => copyWith
  contentPadding: EdgeInsets.symmetric(vertical: 10.0, horizontal: 20.0),
  border: OutlineInputBorder(
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
  enabledBorder: OutlineInputBorder(
    borderSide: BorderSide(color: Colors.blueAccent, width: 1.0),
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
  focusedBorder: OutlineInputBorder(
    borderSide: BorderSide(color: Colors.blueAccent, width: 2.0),
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
);
```

## Observation

- pass value to the StatefulWidget and fetch it from The State Class
- search

````
public, private, protected, static, final, const, 
````

- static

````dart
class Car {
  String? color = 'white';
  static int wheel = 4;
}

void main() {
    
  print('color: ${Car().color}'); // => initialise an object : instantiate the whole class  
    
  print('wheel: ${Car.wheel}'); // => call a variable without instantiate the class
    
}
````