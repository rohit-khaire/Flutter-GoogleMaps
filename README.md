# Flutter Integration: OpenStreetMap (OSM)
Integrate OpenStreetMap for location-based services using the `flutter_map` package.

---

## 🛠️ Prerequisites
Ensure the following tools are installed before beginning the implementation:

* **Flutter SDK:** [Install Guide](https://docs.flutter.dev/get-started/install)
* **Android Studio:** For Android toolchain and emulators.
* **VS Code:** With the **Flutter** extension installed.

---

## ⚙️ Environment Setup (Optional)
Use these commands if you need to manually configure your Flutter environment:

```bash
# Clone Flutter SDK
git clone [https://github.com/flutter/flutter.git](https://github.com/flutter/flutter.git) -b stable

# Add Flutter to PATH
echo 'export PATH="$PATH:`pwd`/flutter/bin"' >> ~/.bashrc

# Reload bash
source ~/.bashrc

# Check installation
flutter doctor
```
---

<br>

## 🚀 Step-by-Step Implementation

### Step 1: Create Flutter Project
Open your terminal and run:
```bash
flutter create osm_app
cd osm_app
```

### Step 2: Add Dependencies
Open `pubspec.yaml` and add the following under `dependencies`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_map: ^6.0.0
  latlong2: ^0.9.0
```

Then, fetch the packages:
```bash
flutter pub get
```

### Step 3: Implement the Map
Replace the entire content of `lib/main.dart` with the code below:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_map/flutter_map.dart';
import 'package:latlong2/latlong.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(useMaterial3: true),
      home: MapScreen(),
    );
  }
}

class MapScreen extends StatelessWidget {
  // Coordinates for Mumbai
  final LatLng center = LatLng(19.0760, 72.8777);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("OSM Map"),
        centerTitle: true,
      ),
      body: FlutterMap(
        options: MapOptions(
          initialCenter: center,
          initialZoom: 13,
        ),
        children: [
          TileLayer(
            urlTemplate: "[https://tile.openstreetmap.org/](https://tile.openstreetmap.org/){z}/{x}/{y}.png",
            userAgentPackageName: 'com.example.app',
          ),
          MarkerLayer(
            markers: [
              Marker(
                point: center,
                width: 40,
                height: 40,
                child: const Icon(
                  Icons.location_on,
                  color: Colors.red,
                  size: 40,
                ),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
```

### Step 4: Run the Application
Connect your device or start an emulator and run:
```bash
flutter run
