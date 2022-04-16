# Themes

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