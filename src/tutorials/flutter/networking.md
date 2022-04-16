# Networking

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
