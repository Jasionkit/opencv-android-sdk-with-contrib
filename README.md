# opencv-android-sdk-with-contrib
opencv341 android sdk with contrib341 module build on windows.

天知道在windows上编译这俩个库要趟过多少坑。

工作需要，目前主要编译了armeabi-v7a、x86、arm64-v8a的.so库.a库，主要用于jni编程，附带java应用层函数，并且已添加OPENCL支持。

## How to build yourself on windows.

Refer to [build opencv3.4.1 android sdk+contrib on windows](https://github.com/Mainvooid/opencv-android-sdk-with-contrib/wiki/build-opencv3.4.1-android-sdk-contrib-on-windows)

## How to use in your android project

you can refer to \Android.mk and \Application.mk
and see [Android Studio JNI层调用OpenCV进行图像处理](https://github.com/Mainvooid/opencv-android-sdk-with-contrib/wiki/Android-Studio-JNI%E5%B1%82%E8%B0%83%E7%94%A8OpenCV%E8%BF%9B%E8%A1%8C%E5%9B%BE%E5%83%8F%E5%A4%84%E7%90%86)

## See what the SDK build or support
 check \CMakeCache-XXXX.txt

## A templet build.gradle for armeabi-v7a and x86 with NDK

```
apply plugin: 'com.android.library'
android {
    ...
    defaultConfig {
        ...
        //配置NDK信息
        ndk {
            moduleName "opencv3"
            ldLibs "log", "jnigraphics", "m", "z"
            abiFilters "armeabi-v7a","x86"
        }
        //配置SO文件存放路径
        sourceSets {
            main {
                jni.srcDirs = []
                jniLibs.srcDirs = ['src/main/libs']
            }
        }
    }
    //设置构建脚本路径，会自动索引同目录下的Application.mk
    externalNativeBuild {
        ndkBuild {
            path 'src/main/jni/Android.mk'
        }
    }
}
...
```
