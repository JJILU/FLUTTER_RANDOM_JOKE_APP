# NBA Data Flutter App

This Flutter app reads data from the [balldontlie.io](https://www.balldontlie.io/#introduction) NBA API and displays NBA data, including teams, players, stats, and games.

## Features

- Fetch and display NBA teams, players, and game stats using the `balldontlie` API.
- Real-time data updates.
- User-friendly interface for navigating NBA information.
- Responsive design suitable for various screen sizes.

## Requirements

- Flutter SDK
- Dart 2.20 or later

## Installation

1. Clone this repository:
    ```bash
    git clone https://github.com/yourusername/nba-data-flutter-app.git
    ```

2. Navigate to the project directory:
    ```bash
    cd nba-data-flutter-app
    ```

3. Install dependencies:
    ```bash
    flutter pub get
    ```

4. Create a `consts.dart` file in the `lib` directory:
    - Add the following code to `consts.dart`:
      ```dart
      const String NBA_API_URL = 'https://www.balldontlie.io/api/v1';
      ```

5. Run the app:
    ```bash
    flutter run
    ```

## Usage

- Launch the app to fetch and display NBA data.
- View NBA teams, players, and game stats.
- Navigate through the app to see detailed information on games and players.

## API Integration

- The app uses the [balldontlie.io](https://www.balldontlie.io/#introduction) API to fetch NBA data.
- The base URL for the API is:
