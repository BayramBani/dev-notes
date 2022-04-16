# Events

## GestureDetector
 
> detecting user interacts

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