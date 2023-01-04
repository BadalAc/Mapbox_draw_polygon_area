<!--
This README describes the package. If you publish this package to pub.dev,
this README's contents appear on the landing page for your package.

For information about how to write a good package README, see the guide for
[writing package pages](https://dart.dev/guides/libraries/writing-package-pages).

For general information about developing packages, see the Dart guide for
[creating packages](https://dart.dev/guides/libraries/create-library-packages)
and the Flutter guide for
[developing packages and plugins](https://flutter.dev/developing-packages).
-->

# Flutter Mapbox Polygon Area Calculator

 A Flutter package that allows you to calculate the area of a polygon drawn on a Mapbox map.
 
## Features

<img src="https://user-images.githubusercontent.com/57612587/210498372-60594a10-f78f-4521-8aa4-d042542f34ed.png" width="360" height="740">

## Getting started

This package is highly dependent on Get state management package.
Install latest getX pacakge from  pub dev.

```
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:mapbox_draw_polygon_area/src/mapbox_draw_polygon.dart'
    as myPacakge;
import 'package:mapbox_gl/mapbox_gl.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      home: MapboxMapExample(),
    );
  }
}

class MapboxMapExample extends StatefulWidget {
  @override
  _MapboxMapExampleState createState() => _MapboxMapExampleState();
}

class _MapboxMapExampleState extends State<MapboxMapExample> {
  var myController = Get.put(myPacakge.MapBoxGetController()); //<----to use Getx controller provided by the package .

  void _onMapCreated(MapboxMapController controller) {
    //Assigning mapbox controller to your getx controller instance 
    myController.mapBoxcontrollerInstance = controller; //<----Here
    //Add this function to use on symbol tap and feature taps 
    myController.onMapCreateFun(); //<----Here
  }

  @override
  void initState() {
      super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButtonLocation:
          FloatingActionButtonLocation.miniCenterDocked,
      floatingActionButton: Stack(
        fit: StackFit.expand,
        children: [
          
          myController.drawPad(), // <-------------Snapping sheet to draw points
          myController.centerTargetiIcon(), // <------Target icon that is placed in the center of the screen
         
        ],
      ),
      body: MapboxMap(
        styleString: MapboxStyles.LIGHT,
        accessToken: 'mapbox public token', // <------your publicmapbox token
        onMapCreated: _onMapCreated,
        trackCameraPosition: true,
        initialCameraPosition: const CameraPosition(
          target: LatLng(40.384950128422496, -85.56492779229464),
          zoom: 16,
        ),
        //This is a helper line that will guide you in the process
        onCameraIdle: (() {
          if (myController.listOfDrawLatLlongs.isNotEmpty && 
              !myController.isPolygonSaved.value &&
              !myController.isDiagonalSaved.value) {
            myController.drawActiveline(); // <------Here-------
          }
        }),
      ),
    );
  }
}
```




## Usage

To see an example of how to use the mapbox polygon area calculator, check out the example directory in the package source code.




## Additional information

You can checkout from github and contribute as much you want.
#   m a p b o x _ d r a w _ p o l y g o n _ a r e a 
 
 