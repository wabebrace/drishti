# Drishti Face Filter Android App

This is an Android application that demonstrates real-time eye tracking and face filtering using the Drishti SDK.

## Features

- Real-time face detection and tracking
- Eye tracking and iris detection
- OpenGL ES 2.0/3.0 rendering
- Camera2 API integration
- Portrait orientation optimized

## Requirements

- Android Studio 3.2.1 or higher
- CMake 3.9.2 or higher
- Android NDK r17c or r18b (NDK r19+ not currently supported)
- Ninja build system
- Android SDK with API level 24 (Android 7.0) or higher
- Device with camera and autofocus support

## Setup

1. **Install Prerequisites**
   - Install Android Studio
   - Install CMake (3.9.2+)
   - Download Android NDK r17c or r18b

2. **Configure local.properties**

   Create a `local.properties` file in the `android-studio` directory with the following content:

   ```properties
   ndk.dir=/path/to/android-ndk-r18b
   sdk.dir=/path/to/Android/Sdk
   cmake.dir=/path/to/cmake
   ```

   The `cmake.dir` should point to the directory containing the `bin/cmake` executable.

3. **Open Project**
   - Open Android Studio
   - Select "Open an existing Android Studio project"
   - Navigate to `drishti/android-studio` directory
   - Wait for Gradle sync to complete

## Building

### Using Android Studio

1. Open the project in Android Studio
2. Select the target device or emulator
3. Click "Run" or press Shift+F10

### Using Command Line

```bash
cd android-studio
./gradlew assembleDebug
```

For a specific architecture:
```bash
./gradlew assembleDebug -Parch=arm64-v8a
```

Supported architectures:
- `arm64-v8a` (default)
- `armeabi-v7a`
- `x86_64`

## App Structure

```
app/
├── src/main/
│   ├── java/com/elucideye/facefilter/
│   │   ├── FaceFilterActivity.java       # Main activity
│   │   ├── FaceFilterFragment.java       # UI fragment
│   │   ├── FaceFilterRenderer.java       # OpenGL renderer
│   │   ├── FaceFilterGLSurfaceView.java  # GL surface view
│   │   ├── FaceFilterCameraManager.java  # Camera management
│   │   ├── FaceFilterCameraStateCallback.java
│   │   └── FaceFilterCameraSessionCallback.java
│   ├── res/
│   │   ├── layout/                       # UI layouts
│   │   ├── values/                       # Strings, styles
│   │   └── mipmap-*/                     # App icons
│   └── AndroidManifest.xml
└── build.gradle                          # App-level build config
```

## Permissions

The app requires the following permissions:
- `CAMERA` - For accessing device camera
- `android.hardware.camera` - Camera feature
- `android.hardware.camera.autofocus` - Autofocus feature

## Known Issues

- Android NDK r19 is not currently supported due to structural changes
- First Gradle build may take longer as it downloads dependencies
- Some Android Studio/Gradle communication issues may occur (see main README)

## Troubleshooting

### Build Failures

1. **NDK not found**: Verify `ndk.dir` in `local.properties` points to a valid NDK installation (r17c or r18b)
2. **CMake errors**: Ensure `cmake.dir` in `local.properties` points to CMake 3.9.2 or higher
3. **Gradle sync issues**: Try "File → Invalidate Caches / Restart"

### Runtime Issues

1. **Camera permission denied**: Grant camera permission in system settings
2. **App crashes on start**: Check logcat for native library loading errors

## Additional Information

For more details on the Drishti SDK and building options, see the main repository README.

## License

This project is released under the 3 Clause BSD License.

Copyright 2017-2018 Elucideye, Inc. All rights reserved.
