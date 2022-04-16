# Flutter

## Overview

- modern reactive framework
- Fast 2D rendreing engine

### Hot stateful Reload

The UI updates immediately when you make a code change.

### Widget

Widgets are the foundation of Flutter apps. It is a description of part of user interface.

=> everything in flutter is a widget.

#### StatelessWidget

An immutable widget. All its fields are final after creation.

#### StatefulWidget

A widget that creates a State object.



## Widgets

### Text

````dart
Text(
	'Votre Partenaire Digitale',
	style: TextStyle(
    	color: Colors.white,
        fontSize: 20,
	),
),
````

### TextField

```dart
TextField(
	textAlign: TextAlign.center,
    keyboardType: TextInputType.emailAddress, // email => show @ in the keyborad
    onChanged: (value) {
    email = value;
    //Do something with the user input.
    },
    decoration:
    kInputDecoration.copyWith(hintText: 'enter your email'),
),

TextField(
    obscureText: true, // Password
	style: TextStyle(
    	color: Colors.black,
	),
    decoration: kTextFieldInputDecoration,
    onChanged: (value) {
    	print(value);
	},
),

const kTextFieldInputDecoration = InputDecoration(
  border: OutlineInputBorder(
    borderRadius: BorderRadius.all(
      Radius.circular(10.0),
    ),
    borderSide: BorderSide.none,
  ),
  /*labelText: 'your city',*/
  filled: true,
  fillColor: Colors.white,
  icon: Icon(
    Icons.location_city,
    color: Colors.white,
  ),
  hintText: 'city name',
  hintStyle: TextStyle(color: Colors.grey),
);
```

clear TextField

```dart
final messageTextController = TextEditingController();
***
TextField(
  controller: messageTextController,
  onChanged: (value) {
    messageText = value;
  },
  decoration: kMessageTextFieldDecoration,
),
// *** : Event
FlatButton(
	onPressed: () {
		messageTextController.clear();
	},
    child: Text('Send')
)
```

### DropDownButton (Android - Material)

```dart
String selectedCurrency = 'USD';
***
DropdownButton<String>(
  value: 'USD',
  items: [
    DropdownMenuItem(
      child: Text('EUR'),
      value: 'EUR',
    ),
    DropdownMenuItem(
      child: Text('USD'),
      value: 'USD',
    ),
    DropdownMenuItem(
      child: Text('GPB'),
      value: 'GPB',
    )
  ],
  onChanged: (value) {
	setState(() {
    	selectedCurrency = value.toString();
	});
  },
)
```

````dart
// Data
String selectedCurrency = 'USD';
const List<String> currenciesList = [
  'EUR',
  'USD',
  'GPB'  
];
// Method
List<DropdownMenuItem<String>> getDropDownItems() {
	List<DropdownMenuItem<String>> list = [];
    for (String item in currenciesList) {
      list.add(DropdownMenuItem(
        child: Text(item),
        value: item,
      ));
    }
    return list;
}
// widget
DropdownButton<String>(
    value: selectedCurrency,
    items: getDropDownItems(),
	onChanged: (value) {    	
        setState(() {
			selectedCurrency = value.toString();
		});
	},
),
````

### CupertinoPicker (IOS)

````dart
// Data
const List<String> currenciesList = [
  'EUR',
  'USD',
  'GPB'  
];
// Method
List<Text> getCurrenciesList() {
    List<Text> list = [];
    for (String item in currenciesList) {
      list.add(Text(item));
    }
    return list;
}
// widget
CupertinoPicker(
	itemExtent: 32,
    onSelectedItemChanged: (selectedIndex) {
    	print('selectedIndex: $selectedIndex');
	},
    children: getCurrenciesList(),
),
````

### Slider

```dart
Slider(
  activeColor: Colors.white,
  min: 120,
  max: 220,
  value: height.toDouble(),
  onChanged: (double value) {
    print(value);
    setState(() {
      height = value.round();
    });
  },
)
```

```dart
SliderTheme(
	data: SliderTheme.of(context).copyWith(
    	thumbColor: Color(0xFFEB1555),
        overlayColor: Color(0x29EB1555),
        inactiveTrackColor: Colors.grey,
        activeTrackColor: Colors.white,
        thumbShape: RoundSliderThumbShape(
        	enabledThumbRadius: 15.0,
		),
        overlayShape:
        	RoundSliderOverlayShape(overlayRadius: 30.0),
		),
        child: Slider(
	        /*activeColor: Colors.white,*/
        	min: 120,
    		max: 220,
           	value: height.toDouble(),
            onChanged: (double value) {
            	print(value);
                setState(() {
                	height = value.round();
			});
		},
	),
)
```

### Container

````dart
Container(
	margin: EdgeInsets.all(15),
    decoration: BoxDecoration(
	    color: color,
        borderRadius: BorderRadius.circular(10), // 
    ),
    child: Center(
    	child: Text('Body Text 11'),
	),
)
````
### StreamBuilder

```dart
StreamBuilder<QuerySnapshot>(
  stream: _firestore.collection('messages').snapshots(),
  builder: (context, snapshot) {
    if (snapshot.hasData) {
      final messages = snapshot.data!.docs;
      List<Text> messageWidgets = [];
      for (var message in messages) {
        //final messageText = message.data['text'];
        final messageText = message['text'];
        final messageSender = message['sender'];
        final messageWidget =
            Text('$messageText from $messageSender');
        messageWidgets.add(messageWidget);
      }
      return Column(
        children: messageWidgets,
      );
    } else {
      return Center(
        child: CircularProgressIndicator(
          backgroundColor: Colors.lightBlueAccent,
        ),
      );
    }
  },
),
```

### ListView

```dart
return Expanded(
  child: ListView(
    children: messageWidgets,
  ),
);
```

- ListView.builder

```dart
class _TasksListState extends State<TasksList> {
  List<Task> tasks = [
    Task(name: 'this is the task 1'),
    Task(name: 'the task 2'),
    Task(name: 'and the 3 rd task'),
    Task(name: 'maybe 4'),
    Task(name: 'or 5'),
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemBuilder: (context, index) {
        return TaskTile(
            taskTitle: tasks[index].name ?? "",
            isChecked: tasks[index].isDone,
            checkboxCallback: (checkboxState) {
              setState(() {
                tasks[index].toggleDone();
              });
            });
      },
      itemCount: tasks.length,
    );
  }
}
```

### Expanded

match parent

```
Expanded(
  child: ListView(
    padding: EdgeInsets.symmetric(horizontal: 10.0, vertical: 20.0),
    children: messageBubbles,
  ),
)
```

### Flexible

responsive design in diffrent aspect ratio

```
Flexible(
  child: Hero(
    tag: 'logo',
    child: Container(
      height: 200.0,
      child: Image.asset('images/logo.png'),
    ),
  ),
),
```

### layout widget

#### Column

#### Row


### Lifecycle

#### Stateless :

````
Create / Destroy
````

#### Stateful

````dart
void initState(){}

Widget build(BuildContext context){
	return null;
}

void desactivate(){}
````

#### State Class

Access from State (_LocationScreenState)  to the StatefulWidget (LocationScreen)  via widget : `updateUI(widget.locationWeather);`

````dart
class LocationScreen extends StatefulWidget {
    
  LocationScreen({this.locationWeather});
  final locationWeather;
  @override
  _LocationScreenState createState() => _LocationScreenState();
}

class _LocationScreenState extends State<LocationScreen> {
   
  @override
  void initState() {
    super.initState();
      
    updateUI(widget.locationWeather);
    //print(widget.locationWeather);
  }
}
````

### Widget Based on Plateform

````dart
// Data
const List<String> currenciesList = [
  'EUR',
  'USD',
  'GPB'  
];

// Method
DropdownButton<String> getDropDownButton() {
    List<DropdownMenuItem<String>> list = [];
    for (String item in currenciesList) {
      list.add(DropdownMenuItem(
        child: Text(item),
        value: item,
      ));
    }
    return DropdownButton<String>(
      value: selectedCurrency,
      items: list,
      onChanged: (value) {
        print(value);
        setState(() {
          selectedCurrency = value.toString();
        });
      },
    );
  }

  CupertinoPicker getCupertinoPicker() {
    List<Text> list = [];
    for (String item in currenciesList) {
      list.add(Text(
        item,
        style: TextStyle(color: Colors.white),
      ));
    }

    return CupertinoPicker(
      itemExtent: 32,
      onSelectedItemChanged: (selectedIndex) {
        print('selectedIndex: $selectedIndex');
      },
      children: list,
    );
  }

// Widget
Container(
	child: Platform.isIOS ? getCupertinoPicker() : getDropDownButton(),
)
 
````

### Animation

> welcome screen

```dart
Hero(
  tag: 'logo',
  child: Container(
    child: Image.asset('images/logo.png'),
    height: 60.0,
  ),
)
```

> registration screen

```dart
Hero(
  tag: 'logo',
  child: Container(
    height: 200.0,
    child: Image.asset('images/logo.png'),
  ),
)
```

---

#### AnimationController

````dart
class _WelcomeScreenState extends State<WelcomeScreen>
    with SingleTickerProviderStateMixin { 
    //@note : implement SingleTickerProviderStateMixin
    
    // @note : create AnimationController;
  late AnimationController controller;

  @override
  void initState() {
    super.initState();
      
    controller = AnimationController(
      vsync: this,
      duration: Duration(seconds: 1),
    );

    controller.forward();

    controller.addListener(() {
      setState(() {
        print(controller.value);
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.red.withOpacity(controller.value),
      body:[Widget]
        ....
     )
  }
````

````dart
controller = AnimationController(
	vsync: this,
    duration: Duration(seconds: 3),
    upperBound: 100.0, //@note
);
    
Text(
	'${controller.value.toInt()} %', // @note
    style: TextStyle(
    fontSize: 45.0,
    	fontWeight: FontWeight.w900,
),  
    
Hero(
	tag: 'logo',
    child: Container(
    	child: Image.asset('images/logo.png'),
        height: controller.value,  // @note
	),
),
````

```dart
animation =
    ColorTween(begin: Colors.black, end: Colors.white).animate(controller);
***
backgroundColor: animation.value,
```
## State

### Local State

```dart
class TaskCheckbox extends StatefulWidget {
  @override
  _TaskCheckboxState createState() => _TaskCheckboxState();
}

class _TaskCheckboxState extends State<TaskCheckbox> {
  bool? isChecked = false;

  @override
  Widget build(BuildContext context) {
    return Checkbox(
      activeColor: Colors.lightBlueAccent,
      value: isChecked,
      onChanged: (value) {
        setState(() {
          isChecked = value;
        });
      },
    );
  }
}
```

### Global State

```
import 'package:flutter/material.dart';

class TaskTile extends StatefulWidget {
  @override
  _TaskTileState createState() => _TaskTileState();
}

class _TaskTileState extends State<TaskTile> {
  bool isChecked = false;

  void checkboxCallback(bool checkboxState) {
    setState(() {
      isChecked = checkboxState;
    });
  }

  @override
  Widget build(BuildContext context) {
    return ListTile(
      title: Text(
        'this is the task 1',
        style: TextStyle(
          decoration: isChecked ? TextDecoration.lineThrough : null,
        ),
      ),
      trailing: TaskCheckbox(
        checkboxState: isChecked,
        toggleCheckboxState: checkboxCallback,
      ),
    );
  }
}

class TaskCheckbox extends StatelessWidget {
  final bool checkboxState;
  final Function toggleCheckboxState;

  TaskCheckbox({
    required this.checkboxState,
    required this.toggleCheckboxState,
  });

  @override
  Widget build(BuildContext context) {
    return Checkbox(
      activeColor: Colors.lightBlueAccent,
      value: checkboxState,
      onChanged: (value) => toggleCheckboxState(value),
    );
  }
}
```



## Themes

[flutter cookbook](https://flutter.dev/docs/cookbook)

[flutter theme](https://flutter.dev/docs/cookbook/design/themes)

[colorZilla](https://chrome.google.com/webstore/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp?hl=fr)

````dart
MaterialApp(
	title: 'Flutter Demo',
    theme: ThemeData(
    	primarySwatch: Colors.blue,
   	),     
    home: MyHomePage(title: 'Universal Web Soft'),
)
````

````
theme: ThemeData.dark(),
theme: ThemeData.light(),  
````

````dart
theme: ThemeData(
	primarySwatch: Color(0xFFd84315), // replace # with 0xFF in hex code
), 
````

````dart
theme: ThemeData(
	primaryColor: Colors.teal, // app bar
    accentColor: Colors.teal.shade500, // fab
    scaffoldBackgroundColor: Colors.teal.shade200, // body
    textTheme: TextTheme(
    	body1: TextStyle(
        	color: Colors.white,
      	),
	),
),
````

````dart
theme: ThemeData.dark().copyWith(
	primaryColor: Colors.blue.shade900,
    scaffoldBackgroundColor: Colors.blue.shade800,
),

// floating button color
floatingActionButton: Theme(
	data: ThemeData.light(),
    child: FloatingActionButton(
    	onPressed: _incrementCounter,
  		tooltip: 'Increment',
        child: Icon(Icons.add
	),
),
//-- OR --
floatingActionButton: Theme(
	data: ThemeData(
    	accentColor: Colors.red,
	),
    child: FloatingActionButton(
    	onPressed: _incrementCounter,
		tooltip: 'Increment',
        child: Icon(Icons.add),
	),
),
````

### Reuse widgets

#### 1) widgets

Android studio => Flutter outline => (select widget) => Extract Widget => (give a name)

#### 2) values

> register.dart

```
TextField(
  onChanged: (value) {
    //Do something with the user input.
  },
  decoration:
      kInputDecoration.copyWith(hintText: 'enter your email'),
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

## Events

- GestureDetector() : detecting user interacts

```dart
GestureDetector(
  onTap: () {
    print('GestureDetector: onTap');
  },
  child: MyCard(
    color: activeCardColor,
    cardChild: GenderWidget(
      icon: FontAwesomeIcons.mars,
      color: Colors.blue,
      text: 'Male',
    ),
  ),
)
```



## Routes & Navigation

````
Navigator :
.push => go to
.pop  <= back to
````

### Named Routes

[documentation](https://flutter.dev/docs/cookbook/navigation/named-routes)

> main

```dart
import 'package:flutter/material.dart';
import 'input_page.dart';
import 'result_page.dart';

void main() {
  runApp(BMICalculator());
}

class BMICalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => InputPage(),
        '/result': (context) => ResultPage(),
      },
      theme: ThemeData.dark(),
    );
  }
}
```

> input_page

```dart
GestureDetector(
  onTap: () {
    Navigator.pushNamed(context, '/result');
  },
  child: Container(
    color: kBottomContainerColor,
    margin: EdgeInsets.only(top: 10),
    height: kContainer_height,
    width: double.infinity,
    child: Center(child: Text('Calculate')),
  ),
)
```

### Routes with data

```dart
onTap: () {
  CalculatorBrain calc =
      CalculatorBrain(weight: weight, height: height);

  Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => ResultPage(
          bmiResult: calc.calculate(),
          resultText: calc.getResult(),
          interpretation: calc.getInterpretation(),
        ),
      ));
},
```

### Navigate and recieve data

navigate from location_screen to city_screen and get a value (cityName)

> Page 1 : location_screen

````dart
FlatButton(
	onPressed: () async {
    	var typedName = await Navigator.push(
        	context, MaterialPageRoute(                          
        		builder: (context) {
            		return CityScreen();
				},
            ),
		);
        print('typedName: $typedName');
    },
	child: Icon(Icons.location_city, size: 50.0,),
),
````

> Page 2 : city_screen

````dart
FlatButton(
	onPressed: () {
    	Navigator.pop(context, cityName);
  	},
    child: Text(
    	'Get Weather',
       	style: kButtonTextStyle,
	),
),
````





## API Calls

[fetch-data](https://flutter.dev/docs/cookbook/networking/fetch-data)

[http package](https://pub.dev/packages/http)

[openweathermap](https://openweathermap.org/)

[coinapi](https://www.coinapi.io/)



```dart
import 'package:http/http.dart' as http;

  void getData() async {
    try {
      http.Response response = await http.get(Uri.parse(
          'https://api.openweathermap.org/data/2.5/weather?lat=36.4696763&lon=10.744137&appid=c8e383babce097193c860f2ccbabf051'));
        
      if (response.statusCode == 200) {        
        String data = response.body;
          
        var decodedData = jsonDecode(data);
        var temperature = decodedData['main']['temp'];
        var condition = decodedData['weather'][0]['id'];
        var city = decodedData['name'];
        var weatherDescription = decodedData['weather'][0]['description'];

        print('weatherDescription: $weatherDescription');
        print('temperature: $temperature');
        print('condition: $condition');
        print('city: $city');
      } else {
        print(response.statusCode);
      }
    } catch (e) {
      print(e);
    }
  }
```



## Firebase

### Installation

todo

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

## Dart

### Hello World

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

### enum

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

### Dart Ternary Operator

````dart
condition ? do : else
    
color: selectedGender == Gender.male ? activeCardColor: inactiveCardColor,
````

### Null Aware Operator

````dart
variable ?? default_value

color: kColor ?? Colors.red,

=> if kColor != null (color: kColor ) else (color : Colors.red)
````

### Map

````dart
Map<KeyType, ValueType> mapName = {
	key: value,
}

print(mapName[key]);
print(mapName.values);
print(mapName.keys);    
````

### Synchronous & Asynchronus

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



### Functions

Functions are first class objects



### import

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

## Dart Package

[pub.dev](https://pub.dev/)

- http : http call api
- flutter_spinkit : loader



## Android Studio

###  shortcuts

- Hot Reload : Ctrl + S
- Hot Restart : Maj + F10
- Show doc : Ctrl + Q



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



