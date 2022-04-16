# Routes & Navigation

````
Navigator :
.push => go to
.pop  <= back to
````

## Named Routes

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

## Routes with data

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

## Navigate and recieve data

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