# Darwin Camera <img src="https://user-images.githubusercontent.com/9272830/68128635-18c30500-ff3e-11e9-8a32-c32496d5856f.jpg" width="35%" align="right"></img> 

<img src="https://img.shields.io/badge/license-MIT-green"></img>

Darwin camera makes it super easy to add camera to your Flutter app. It uses the official camera plugin implementation underneath.

- Scales the preview based on the aspect ratio of the device.
  - Automatic output cropping to match the preview.
- Provides a toggle between front and back camera.
  - You can configure what it defaults to on opening.
- Provides compression for the captured image which can be configured.
  - Uses the [flutter_image_compress](https://pub.dev/packages/flutter_image_compress) library.
- Provides a minimal UI for the reviewing the capture before saving image.
- Supports both Android and iOS.


## Screenshots


| Camera Stream                  | Preview Captured Image         |
|     :---:       |     :---:       |
| <img src="https://user-images.githubusercontent.com/9272830/68597615-4ae6e080-04c3-11ea-9e1d-77b002827807.PNG" width="50%" ></img> | <img src="https://user-images.githubusercontent.com/9272830/68597699-69e57280-04c3-11ea-9faf-ef5bbdbf2c9f.PNG" width="50%" ></img> |
| Press the `White circular button` to capture image | Press the `Green button` to save image |
| Press the button at the bottom right to `toggle camera` | Press the close button to `discard captured image` |





## Getting Started

In your flutter project add `darwin_camera` as a dependency in `pubspec.yaml`:

```yml
dependencies:
  ...
  darwin_camera:
    git: https://github.com/atlanhq/darwin-camera
    
```
### iOS

Add two rows to the `ios/Runner/Info.plist`:

* one with the key `Privacy - Camera Usage Description` and a usage description.
* and one with the key `Privacy - Microphone Usage Description` and a usage description.

Or in text format add the key:

```xml
<key>NSCameraUsageDescription</key>
<string>Can I use the camera please?</string>
<key>NSMicrophoneUsageDescription</key>
<string>Can I use the mic please?</string>
```

### Android

Change the minimum Android sdk version to 21 (or higher) in your `android/app/build.gradle` file.

```
minSdkVersion 21
```



## Usage example
```dart
import 'package:darwin_camera/darwin_camera.dart';

 DarwinCameraResult result = await Navigator.push(
   context,
   MaterialPageRoute(
     builder: (context) => DarwinCamera(
       cameraDescription: cameraDescription,
       filePath: filePath,
       resolution: ResolutionPreset.high,
       defaultToFrontFacing: true,
       quality: 90,
     ),
   ),
 );

if (result != null && result.isFileAvailable) {
   /// File object returned by Camera.
   print(result.file);
   /// Path where the file is faced. 
   print(result.file.path);
 }

```

### Creating a Image capture Widget

This widget captures an image at a provided file path.

```dart
DarwinCamera({
  
  ///
  /// Flag to enable/disable image compression.
  bool enableCompression = false, 
  
  ///
  /// Disables native back functionality provided by iOS using the swipe gestures.
  bool disableNativeBackFunctionality = false,
  
  /// @Required
  /// List of cameras availale in the device.
  /// 
  /// How to get the list available cameras?
  /// `List<CameraDescription> cameraDescription = await availableCameras();`
  List<CameraDescription> cameraDescription, 
  
  /// @Required
  
  /// Path where the image file will be saved.
  String filePath, 
  
  /// 
  /// Resolution of the image captured
  /// Possible values:
  /// 1. ResolutionPreset.high
  /// 2. ResolutionPreset.medium
  /// 3. ResolutionPreset.low
  ResolutionPreset resolution = ResolutionPreset.high, 

  ///
  /// Open front camera instead of back camera on launch.
  bool defaultToFrontFacing = false;

  ///
  /// Decides the quality of final image captured.
  /// Possible values `0 - 100`
  int quality = 90;

})
```

### Complete example with handling permission
See the [example](https://github.com/atlanhq/darwin-camera/tree/master/example) directory in the github repository

### How to contribute?
See [CONTRIBUTING.md](https://github.com/atlanhq/darwin-camera/blob/master/CONTRIBUTING.md)


<img src="https://user-images.githubusercontent.com/408863/66741678-a78ab780-ee93-11e9-8d90-b274af222339.png" align="centre" />

