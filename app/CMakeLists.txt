cmake_minimum_required(VERSION 3.4.1)

# IMPORTANT: You must set OpenCV_DIR to your OpenCV-android-sdk/sdk/native/jni
# Example:
# set(OpenCV_DIR /home/user/Android/Sdk/OpenCV-android-sdk/sdk/native/jni)
#
# Then:
# find_package(OpenCV REQUIRED)
# include_directories(${OpenCV_INCLUDE_DIRS})
# target_link_libraries(native-lib ${log-lib} ${OpenCV_LIBS})

add_library(native-lib SHARED
            src/main/cpp/native-lib.cpp
            src/main/cpp/edge_detection.cpp)

find_library(log-lib log)

target_include_directories(native-lib PRIVATE ${CMAKE_SOURCE_DIR}/src/main/cpp)

target_link_libraries(native-lib ${log-lib})
