
# Animation

## Hero

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

## AnimationController

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
