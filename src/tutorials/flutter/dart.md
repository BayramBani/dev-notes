# Dart

## Hello World

> scratch.dart

```dart
void main() {
   print('Hello Dart');
}
```

> terminal
````shell
dart scratch.dart
````

## enum

```dart
enum Gender { male, female }

void updateColor(Gender gender) {
	if (gender == Gender.male) {
      maleCardColor = activeCardColor;
      femaleCardColor = inactiveCardColor;
    } else if (gender == Gender.female) {
      maleCardColor = inactiveCardColor;
      femaleCardColor = activeCardColor;
    }
}
```

## Dart Ternary Operator

````dart
condition ? do : else
    
color: selectedGender == Gender.male ? activeCardColor: inactiveCardColor,
````

## Null Aware Operator

````dart
variable ?? default_value

color: kColor ?? Colors.red,

=> if kColor != null (color: kColor ) else (color : Colors.red)
````

## Map

````dart
Map<KeyType, ValueType> mapName = {
	key: value,
}

print(mapName[key]);
print(mapName.values);
print(mapName.keys);    
````

## Synchronous & Asynchronus

```dart
import 'dart:io';

void main() {
  performTasks();
}

void performTasks() async {
  task1();
  String task2Result = await task2();
  task3(task2Result);
}

void task1() {
  String result = 'task 1 data';
  print('Task 1 complete');
}

Future<String> task2() async {
    
  //sync
  //sleep(Duration(seconds: 3));

  String result = "";

  // async
  await Future.delayed(Duration(seconds: 3), () {
    result = 'task 2 data';
    print('Task 2 complete');
  });

  return result;
}

void task3(String task2Data) {
  String result = 'task 3 data';
  print('Task 3 complete with $task2Data');
}
```

> terminal

````shell
dart scratch.dart
````

The **await** operator allows you to wait for the resolution of a Future (Promise). It can only be used within an asynchronous function (defined with the async function instruction).

Future = a promise that you will get something in the future

### loop

```dart
for (int i = 0; i < 10; i += 2) print(i);
```

```dart
List<String> numbers = ['one', 'two', 'three'];
for (String n in numbers) print(n);
```

### mixin

Mixins are a way of reusing a class’s code in different class hierarchies

```dart
void main() {
  Duck().fly();
  Duck().swim();
}

class Animal {
  void move() {
    print('changed position');
  }
}

class Bird extends Animal {
  void move() {
    super.move();
    print('by flying');
  }
}

class Fish extends Animal {
  void move() {
    super.move();
    print('by swimming');
  }
}

mixin CanFly {
  void fly() {
    print('Change position by flying');
  }
}

mixin CanSwim {
  void swim() {
    print('Change position by swimming');
  }
}

class Duck extends Animal with CanFly, CanSwim {}
```



## Functions

Functions are first class objects



## import

> import only {Platform} Class from {dart:io} package

````dart
import 'dart:io' show Platform;
````

> import all Class except {Platform} Class from {dart:io} package

```dart
import 'dart:io' hide Platform;
```

> rename package

````dart
import 'package:http/http.dart' as http;
````

## Callback

The Callback is a function or a method which we pass as an argument into another function or method and can perform an action when we require it.

## Dart Package

[pub.dev](https://pub.dev/)

- http : http call api
- flutter_spinkit : loader

