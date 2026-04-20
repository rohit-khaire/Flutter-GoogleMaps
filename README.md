## Flutter-GoogleMaps
Integrate Google Maps for location-based services

 Clone Flutter SDK
git clone https://github.com/flutter/flutter.git -b stable

 Add Flutter to PATH
echo 'export PATH="$PATH:`pwd`/flutter/bin"' >> ~/.bashrc

 Reload bash
source ~/.bashrc

 Check installation
flutter doctor

-------------------------------------------------------------

Step 1: Create Flutter Project

flutter create osm_app
cd osm_app

2. Open pubspec.yaml → add:
dependencies:
  flutter:
    sdk: flutter
  flutter_map: ^6.0.0
  latlong2: ^0.9.0

3. 
flutter pub get

4. Replace lib/main.dart

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
      home: MapScreen(),
    );
  }
}

class MapScreen extends StatelessWidget {
  final LatLng center = LatLng(19.0760, 72.8777); // Mumbai

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("OSM Map")),
      body: FlutterMap(
        options: MapOptions(
          initialCenter: center,
          initialZoom: 13,
        ),
        children: [
          TileLayer(
            urlTemplate: "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
          ),
          MarkerLayer(
            markers: [
              Marker(
                point: center,
                width: 40,
                height: 40,
                child: Icon(Icons.location_on, color: Colors.red, size: 40),
              ),
            ],
          ),
        ],
      ),
    );
  }
}




# Run app (this is where magic happens)
flutter run

