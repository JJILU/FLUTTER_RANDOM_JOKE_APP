# Random Joke Generator Flutter App

This is a simple Flutter mobile application that generates random jokes by making an HTTP GET request to the [Official Joke API](https://official-joke-api.appspot.com/random_joke). The response is in JSON format, and the app decodes it to display the joke's setup and punchline.

## Features

- Fetches random jokes from the Official Joke API.
- Displays the joke's type, setup, and punchline.
- Utilizes the `http` package for making GET requests.
- Implements `FutureBuilder` to handle asynchronous operations and display the joke once data is fetched.

## Requirements

- Flutter SDK (latest stable version recommended)
- Dart 2.12.0 or newer
- Android Studio/Visual Studio Code
- A connected mobile device or emulator

## Installation

1. Clone this repository:
    ```bash
    git clone https://github.com/your-username/random_joke_flutter.git
    ```

2. Change to the project directory:
    ```bash
    cd random_joke_flutter
    ```

3. Get the Flutter dependencies:
    ```bash
    flutter pub get
    ```

4. Run the app:
    ```bash
    flutter run
    ```

## Usage

Once the app is running, it will make an HTTP GET request to the Joke API and display a random joke. The joke is shown using the `FutureBuilder` widget, which handles the asynchronous nature of the request.

## Code Explanation

1. **HTTP Request**: The app uses the `http` package to send a GET request to the URL: `https://official-joke-api.appspot.com/random_joke`. The response is a JSON object containing the joke's `type`, `setup`, and `punchline`.

2. **Decoding JSON**: The JSON response is decoded using Dart's `json.decode()` method, which converts the JSON string into a Dart map.

3. **FutureBuilder**: The app implements a `FutureBuilder` widget to handle the future response from the HTTP request. It displays the joke when the data is successfully fetched.

### Example Code
Here's the main part of the app:

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Random Joke Generator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: JokePage(),
    );
  }
}

class JokePage extends StatelessWidget {
  Future<Map<String, dynamic>> fetchJoke() async {
    final response = await http.get(Uri.parse('https://official-joke-api.appspot.com/random_joke'));
    if (response.statusCode == 200) {
      return json.decode(response.body);
    } else {
      throw Exception('Failed to load joke');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Random Joke Generator'),
      ),
      body: Center(
        child: FutureBuilder<Map<String, dynamic>>(
          future: fetchJoke(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return CircularProgressIndicator();
            } else if (snapshot.hasError) {
              return Text('Error: ${snapshot.error}');
            } else if (snapshot.hasData) {
              final joke = snapshot.data!;
              return Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text('Type: ${joke['type']}', style: TextStyle(fontSize: 18)),
                  SizedBox(height: 20),
                  Text('${joke['setup']}', style: TextStyle(fontSize: 20)),
                  SizedBox(height: 10),
                  Text('${joke['punchline']}', style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
                ],
              );
            } else {
              return Text('No joke found');
            }
          },
        ),
      ),
    );
  }
}
