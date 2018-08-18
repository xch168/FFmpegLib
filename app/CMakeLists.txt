# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)


add_library( FFmpegUtil
        SHARED
        src/main/cpp/native-lib.cpp )


find_library( log-lib
        log )

find_library( android-lib
        android )

# 设置ffmpeg库所在路径的目录
set(distribution_DIR ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI})

add_library( libffmpeg
        SHARED
        IMPORTED )
set_target_properties( libffmpeg
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libffmpeg.so)


# 添加ffmpeg头文件路径
include_directories(src/main/jniLibs/include)


target_link_libraries( FFmpegUtil
        libffmpeg
        ${log-lib}
        ${android-lib} )