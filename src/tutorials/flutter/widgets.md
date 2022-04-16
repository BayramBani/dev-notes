# Widgets

## Text

````dart
Text(
	'Votre Partenaire Digitale',
	style: TextStyle(
    	color: Colors.white,
        fontSize: 20,
	),
),
````

## TextField

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

## DropDownButton (Android - Material)

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

## CupertinoPicker (IOS)

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

## Slider

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

## Container

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
## StreamBuilder

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

## ListView

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

## Expanded

match parent

```
Expanded(
  child: ListView(
    padding: EdgeInsets.symmetric(horizontal: 10.0, vertical: 20.0),
    children: messageBubbles,
  ),
)
```

## Flexible

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

## Column

## Row

## Widget Based on Plateform

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