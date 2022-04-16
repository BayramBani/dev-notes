# Flutter

## Overview

- modern reactive framework
- Fast 2D rendreing engine

### Hot stateful Reload

The UI updates immediately when you make a code change.

## Widgets

Widgets are the foundation of Flutter apps. It is a description of part of user interface.

Everything in flutter is a widget.

### StatelessWidget

An immutable widget. All its fields are final after creation.

### StatefulWidget

A widget that creates a State object.

### Lifecycle

- Stateless 

Create / Destroy

- Stateful

````dart
void initState(){}

Widget build(BuildContext context){
	return null;
}

void desactivate(){}
````

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