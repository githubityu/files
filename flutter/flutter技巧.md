[TOC]
#### 状态栏文字颜色
##### 全局设置
```dart  
SystemChrome.setSystemUIOverlayStyle(const SystemUiOverlayStyle(
      statusBarColor: Colors.transparent,
      systemNavigationBarColor: Colors.black,
      statusBarIconBrightness: Brightness.dark));
```

##### 单独设置
> 通过AppBar的backgroundColor 来设置黑色或者白色
> |backgroundColor颜色|状态栏文字颜色|
> |--|--|
> | black|white|
> | transparent | white |
> | white | black |

