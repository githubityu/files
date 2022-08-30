[TOC]

##### 1. pigeon

>Pigeon 是一个代码生成器工具，用于使 Flutter 和宿主平台之间的通信类型安全、更轻松、更快捷
>[pub地址](https://pub.flutter-io.cn/packages/pigeon)


##### 2. 定义接口
>创建pigeons/message.dart(lib同级目录创建)

```dart
import 'package:pigeon/pigeon.dart';

/// Description : 定义与原生通信--通过自动生成减少手写代码量
/// 请求参数和返回结果都必需是类结构 否则无法生成文件
/// - Flutter 调用 Native 方法 ( @HostApi() )
/// - Native 调用 Flutter 方法 ( @FlutterApi() )

///Flutter 调用原生代码
@HostApi()
abstract class  CalendarRemindApi {
  ///设置日历提醒
  int addCalendarEvent(String title,String description,int startTime,int  endTime,int minutes,String customAppUri);
  ///判断是否设置过
  bool checkCalendarEvent(String title,String description,int startTime,int  endTime);
}

```


##### 3.定义sh文件 pigeon.sh（lib同级目录创建）
>java_package   目录可以随便填写， 目录如果创建失败 就手动创建目录

```sh
flutter pub run pigeon \
  --input pigeons/message.dart \
  --dart_out lib/pigeon.dart \
  --objc_header_out ios/Runner/pigeon.h \
  --objc_source_out ios/Runner/pigeon.m \
  --experimental_swift_out ios/Runner/Pigeon.swift \
  --java_out ./android/app/src/main/java/io/flutter/plugins/Pigeon.java \
  --java_package "io.flutter.plugins"
```

##### 4. 运行sh文件 pigeon.sh 会生成一下文件
>android/app/src/main/java/io/flutter/plugins/Pigeon.java
>ios/Runner/pigeon.h


##### 5.  配置
```kotlin

class MainActivity: FlutterActivity() {
   inner class A : Pigeon.CalendarRemindApi{
        override fun addCalendarEvent(
            title: String,
            description: String,
            startTime: Long,
            endTime: Long,
            minutes: Long,
            customAppUri: String
        ): Long {
            Log.e("MainActivity-addCalendarEvent","title=$title description=$description startTime=$startTime endTime=$endTime minutes=$minutes")
           return com.app.antnft.util.addCalendarEvent(this@MainActivity,
                title,description,startTime,endTime,minutes,customAppUri)
        }

        override fun checkCalendarEvent(
            title: String,
            description: String,
            startTime: Long,
            endTime: Long
        ): Boolean {
            Log.e("MainActivity-checkCalendarEvent","title=$title description=$description startTime=$startTime endTime=$endTime")
            return com.app.antnft.util.checkCalendarEvent(this@MainActivity,
                title,description,startTime,endTime)
        }

    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Pigeon.CalendarRemindApi.setup(flutterEngine?.dartExecutor?.binaryMessenger,A())
    }

}



```

##### 6. 使用
```dart

CalendarRemindApi().addCalendarEvent().then()

```





