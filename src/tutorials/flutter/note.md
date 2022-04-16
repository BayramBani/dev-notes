# Flutter

- pre-built widget (bloc)
- widget tree
- Packages
- [code magic](https://codemagic.io/start/)
- [app icon](https://appicon.co/)
- [dribbble](https://dribbble.com/)
- [Flutter Course resources](https://github.com/londonappbrewery/Flutter-Course-Resources)

## Section 3

Hello world

````dart
import 'package:flutter/material.dart';

void main() { // starting point
  runApp(MaterialApp(home: Text("Hello world")));
}
````

---

````dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: Text("Hello World")));
````

---

````dart
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
      home: Center(
        child: Text('Hello 23 '),
      ),
    ));

````

---

````dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('U.W.S'),
          backgroundColor: Colors.red,
        ),
        body: Center(
          child: Image(
            image: NetworkImage(
                'https://universalwebsoft.com/assets/img/logo.png'),
          ),
        ),
      ),
    ),
  );
}
````

---

### section 3 / 26

1- add image :

/app/images/logo.png

2 - edit /app/pubspec.yaml

````yaml
  assets:
    - images/logo.png
````

-- Or -- all content

````yaml
  assets:
    - images/
````

3 - ( Android studio ) => pub get

4 - /app/lib/main.dart

````dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('U.W.S'),
          backgroundColor: Colors.red,
        ),
        body: Center(
          child: Image(
            image: AssetImage('images/logo.png'),
          ),
        ),
      ),
    ),
  );
}
````

### Section 6 /40

- Hot reloading => StatelessWidget

````
Android studio => stless
````

````dart
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.white,
        appBar: AppBar(
          title: Text('U.W.S'),
          backgroundColor: Colors.red,
        ),
        body: Center(
          child: Image(
            image: AssetImage('images/logo.png'),
          ),
        ),
      ),
    );
  }
}
````

- Hot restart => rest the state of the app

---

- SafeArea() : visible to the user

````
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: Container(
          color: Colors.white,
          child: Text('Hello'),
        ),
      ),
    );
  }
}
````

````dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea( // <()>=---------------------------------------------------|
          child: Container(
            color: Colors.white,
            child: Text('Hello'),
          ),
        ),
      ),
    );
  }
}
````

- Position :Margin (outside) & Padding (inside)

````
body: SafeArea(
          child: Container(
            height: 100,
            width: 100,
            margin: EdgeInsets.symmetric(vertical: 20, horizontal: 50),
            color: Colors.white,
            child: Text('Hello'),
          ),
        ),
````

````dart
margin: EdgeInsets.fromLTRB(100, 50, 10, 10),
````

````dart
margin: EdgeInsets.only(left: 30, top: 30),
````

````
padding: EdgeInsets.all(10),
````

- Multi-child layout widgets

[Multi-child layout widgets](https://flutter.dev/docs/development/ui/widgets/layout#Multi-child%20layout%20widgets)

> Column / Row

````dart
Column(
	children: [
    	Container(
        	height: 50,
            width: double.infinity,
            color: Colors.white,
            child: Text('Container 1'),
        ),
        SizedBox( // for spacing
        	height: 5,
		),
        Container(
         	height: 50,
            width: double.infinity,
            color: Colors.red,
            child: Text('Container 2'),
        ),
        Container(
          	height: 50,
            width: double.infinity,
            color: Colors.blue,
            child: Text('Container 3'),
    	),
	],
),
````



````dart
Column(
    mainAxisAlignment: MainAxisAlignment.center, // column content position
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    mainAxisAlignment: MainAxisAlignment.spaceBetween,
    
    crossAxisAlignment: CrossAxisAlignment.start, // push columns children
    crossAxisAlignment: CrossAxisAlignment.end,
    crossAxisAlignment: CrossAxisAlignment.stretch, // (match_parent)
    
	verticalDirection: VerticalDirection.up, // column direction
    
	mainAxisSize: MainAxisSize.min, // column size
)
````

container width & heigth

````dart
Container(
	height: 50,
    width: double.infinity,
    color: Colors.white,
    child: Text('Container 1'),
),
````

> Row

````dart
Row(
    crossAxisAlignment: CrossAxisAlignment.stretch,
    children: [
    	Container(
        	color: Colors.white,
            child: Text('Container 1'),
		),
		Container(
			color: Colors.red,
			child: Text('Container 2'),
		),
		Container(
			color: Colors.blue,
			child: Text('Container 3'),
		),
	],
),
````

### Section 6 / 43 Challenge

```dart
class MyApp3 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea(
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Container(
                width: 100,
                height: double.infinity,
                color: Colors.red,
              ),
              Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Container(
                    width: 100,
                    height: 100,
                    color: Colors.yellowAccent,
                  ),
                  Container(
                    width: 100,
                    height: 100,
                    color: Colors.yellow,
                  ),
                ],
              ),
              Container(
                width: 100,
                height: double.infinity,
                color: Colors.blue,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Image

````dart
Image(
	image: AssetImage('images/logo.png'),
),
---
Image.asset('images/dice1.png')
---
Image(
    image: NetworkImage('https://universalwebsoft.com/assets/img/logo.png'),
),
---
CircleAvatar(
	radius: 75,
    backgroundColor: Colors.transparent,
    backgroundImage: AssetImage('images/uws.png'),
),
````

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

#### Fonts

[doc](https://flutter.dev/docs/cookbook/design/fonts)

1- download

[google fonts](https://fonts.google.com/)

/app/fonts/DancingScript-VariableFont_wght.ttf

2 - /app/pubspec.yaml

````yaml
  fonts:
    - family: DancingScript
      fonts:
        - asset: fonts/DancingScript-VariableFont_wght.ttf
````

3 -  ( Android studio ) => pub get

4 - main.dart

````dart
Text(
	'Votre partenaire digitale',
    style: TextStyle(
    	fontFamily: 'DancingScript',
        color: Colors.white70,
        fontSize: 20,
        fontWeight: FontWeight.bold,
        letterSpacing: 1.5,
	),
),
````

### Icons

[material icons](https://material.io/resources)

[google fonts/icon](https://fonts.google.com/icons)

````dart
Icon(
	Icons.call_outlined,
),
````



### Layout

- <Widget> Expanded() : Fill available space

````dart
Row(
	children: [
    	Expanded(
        	flex: 2,
			child: Image(
            	image: AssetImage('images/dice1.png'),
            ),
        ),
        Expanded(
        	flex: 1,
			child: Image(
            	image: AssetImage('images/dice1.png'),
			),
		),
	],
)
````

### Variables

Dart = Statically Typed Language

-> unable to change variable type

> Primitive Types

- string
- int
- double
- bool

### Section 7 Dicee

````dart
class DiceeApp extends StatelessWidget {
  const DiceeApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.red,
        appBar: AppBar(
          title: Center(
            child: Text('Dicee App'),
          ),
          backgroundColor: Colors.red,
        ),
        body: DiceePage(),
      ),
    );
  }
}

class DiceePage extends StatefulWidget {
  const DiceePage({Key? key}) : super(key: key);

  @override
  _DiceePageState createState() => _DiceePageState();
}

class _DiceePageState extends State<DiceePage> {
  int leftDiceNumber = 1;
  int rightDiceNumber = 1;

  void Play() {
    setState(() {
      leftDiceNumber = Random().nextInt(6) + 1;
      rightDiceNumber = Random().nextInt(6) + 1;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Row(
        children: [
          Expanded(
            child: TextButton(
              onPressed: () {
                Play();
              },
              child: Image.asset('images/dice$leftDiceNumber.png'),
            ),
          ),
          Expanded(
            child: TextButton(
              onPressed: () {
                Play();
              },
              child: Image.asset('images/dice$rightDiceNumber.png'),
            ),
          ),
        ],
      ),
    );
  }
}
````

## Section 9: Xylophone

[dart pakages](https://pub.dev/)

- installing package 

> pubspec.yaml

````yaml
dependencies:
  english_words: ^4.0.0
````

(Android Studio) => Pub Get

- Use it

> main.dart

````dart
import 'package:english_words/english_words.dart';

void main() {
  runApp(Xylophone());
}

// Section 9: Xylophone
// -----------------------------------------------------------------------------

class Xylophone extends StatelessWidget {
  const Xylophone({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Xylophone'),
        ),
        body: Container(
          child: Center(
            child: Text(
              nouns.first,
              style: TextStyle(
                fontFamily: 'Glory',
                fontSize: 50,
                color: Colors.blue,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
````

---

>pubspec.yaml

````yaml
dependencies:
  just_audio: ^0.9.11
  
assets:
    - assets/   
````

> main.dart

````dart
import 'package:just_audio/just_audio.dart';
/* ... */

void main() {
  runApp(Xylophone());
}

class Xylophone extends StatelessWidget {
  Future<void> playSound(int note) async {
    final player = AudioPlayer();
    var duration = await player.setAsset('assets/note$note.wav');
    player.play();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Xylophone'),
        ),
        body: SafeArea(
          child: Column(
            children: [
              TextButton(
                onPressed: () {
                  playSound(1);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade100,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(2);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade200,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(3);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade300,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(4);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade400,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(5);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade500,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(6);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade600,
                ),
              ),
              TextButton(
                onPressed: () {
                  playSound(7);
                },
                child: Container(
                  height: 70,
                  color: Colors.blue.shade700,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
````

## Section 10

### List

````dart
void main() {
  List <String> list = ['Ahmed', 'Salah' , 'Ali'];
  print(list[0]);
  print(list.indexOf('Salah'));
  list.add('Mohsen');
  list.insert(1,'Alex');
}
````

### Class

````dart
class Question { // class name
    
  late String questionText; // properties
  late bool questionAnswer;

  Question({String q = '', bool a = false}) { // constructor(same name)
    questionText = q;
    questionAnswer = a;
  }
    
  void showQ(){ // Methos
    print(questionText);
  }
}
````

#### OOP:  Object Oriented Programming

- Abstraction 
- encapsulation :

````
private questionBank => _questionBank
````

- Inheritance
- Polymorphism

````
@override

super 
````

---

instace variable = field = property

immutable = unchangeable

widgets are immutable

---

const vs final :

const : before compile

final : after compile : the point they are created

## Section 12

Refract widget : create re-useable widgets









