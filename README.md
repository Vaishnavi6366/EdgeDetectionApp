# Real-Time Edge Detection Viewer (Skeleton with OpenCV Canny)

This repository is a ready-to-edit skeleton for the RnD assessment:
- Android app (Kotlin) + JNI -> OpenCV (C++) -> OpenGL ES 2.0
- TypeScript web viewer (static sample)

NOTE: To build the native code you must supply an Android OpenCV SDK or
prebuilt OpenCV libs and adjust CMakeLists accordingly. See the "Build" section.

## What's included
- `app/` : Android module skeleton (Kotlin activity, JNI bridge).
- `app/src/main/cpp/` : native C++ code with a real OpenCV-based Canny implementation.
- `gl/` : OpenGL shader & helper skeletons.
- `web/` : TypeScript web viewer (static sample image).
- `screenshots/` : placeholder images.

## Build notes (Android)
1. Install Android Studio, NDK, and CMake.
2. Download Android OpenCV SDK from https://opencv.org/releases/ and place the `sdk/native/jni/include` and `sdk/native/libs` (or adapt to your local layout).
3. In `app/CMakeLists.txt` make sure to locate OpenCV by:

   - Option A: specify `OpenCV_DIR` to the OpenCV Android SDK `sdk/native/jni`.
   - Option B: add include/library paths manually.

Example (add near top of CMakeLists):

    set(OpenCV_DIR /path/to/OpenCV-android-sdk/sdk/native/jni)
    find_package(OpenCV REQUIRED)
    include_directories(${OpenCV_INCLUDE_DIRS})
    target_link_libraries(native-lib ${log-lib} ${OpenCV_LIBS})

4. Build via Android Studio (Sync Gradle, then Run on device).

## How JNI expects frames (current skeleton)
- `NativeBridge.processFrame(byte[] rgba, int width, int height)` expects a byte array containing RGBA bytes (4 * width * height).
- The native code converts RGBA → grayscale → Canny → RGBA and returns a byte[] of the same length.

## Web viewer
- `web/` contains a minimal TypeScript page that displays a base64 sample image.
  Build with `npm install` then `npm run build`.

## Next steps you can ask me to do:
- Wire Camera2 frames to send NV21 or RGBA bytes to native code.
- Implement texture upload from native to OpenGL.
- Add FPS counter and toggle button.
