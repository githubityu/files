[TOC]


##### 文章
[coderzheaven](https://www.coderzheaven.com/)

#####  1. widget

>widget  描述一个UI元素的配置信息
>不可变，配置信息变了就会刷新 widget-tree
>Element读取Widget中的配置信息创建RenderObject
>canUpdate
>如果runtimeType key相同就会用新的widget配置信息更新element的对象的配置信息，否则创建新的element
>createElement
>一个widget可以对应多个Element
>原因是同一个Widget对象可以被添加到UI树的不同部分
>因为一个widget可以多次插入widget树中
>就会针对每一个widget生成对应的element


##### element 复用 机制
>能复用就复用，不能复用直接暴力替换
>如果能服用，就通过新widget的配置信息更新widget
>updateChild



#####  2. Flutter中的四棵树
> widget树会生成对应的element树
> element树会生成对应的render树
> render树会生成layer树
> element是widget和render的中间代理
> 在树中widget和element是一一对应的
> 但是和render不是一一对应的
> 因为有些widget没有对应的RenderObject
>

#####  3. BuildContext
> 就是当前element
> 可以树中向上查找最近的父级普通widget或者state
> findAncestorWidgetOfExactType<Widget/State>
> 一般state不希望暴露，私有，如果要获取，提供一个xxx.of(context)
> 或者通过GlobalKey获取，由于开销比较大，避免使用

```java
    static ScaffoldState? of(BuildContext context) {
    final ScaffoldState? result = context.findAncestorStateOfType<ScaffoldState>();
    return result;
  }


//定义一个globalKey, 由于GlobalKey要保持全局唯一性，我们使用静态变量存储
static GlobalKey<ScaffoldState> _globalKey= GlobalKey();
...
Scaffold(
    key: _globalKey , //设置key
    ...
)

_globalKey.currentState.openDrawer()

```


######  3. 1 InheritedWidget InheritedElement
> getElementForInheritedWidgetOfExactType<>.widget
> 获取对应的 InheritedElement,再获取InheritedWidget
>
> dependOnInheritedWidgetOfExactType
> 获取对应的InheritedWidget并添加依赖关系（后面用到InheritedWidget中数据的widget）
>
> 一般在使用xxx.of(xxx)的时候会调用dependOnInheritedWidgetOfExactType添加到依赖关系中
> 如果只想使用而不添加依赖 使用getElementForInheritedWidgetOfExactType<>.widget


##### 4. widget构造方法
>key放在第一个，child/children放到最后一个,必传的标注 required
>属性值一般标注final，放在以外修改


##### 5. state
>每一个StatefulElement对应一个state
>从树中移除 State 对象”或“插入 State 对象到树中
>此时的树指通过 widget 树生成的 Element 树
>所以说一个 widget可以有多个element，每个element有一个state


###### 5.1 setState()
>本质 修改了widget的配置信息，然后标记数据脏了需要更新，然后框架就会重新调用build方法 来达到刷新的目的


##### 6. RenderObject  RenderObjectWidget
>RenderObject 积木   LeafRenderObjectWidget
>组合积木的组件StatefulWidget和StatelessWidget


##### 7. 补充
> 1. 组合
> StatefulWidget和StatelessWidget
> 2. 渲染  RenderObjectWidget
>  LeafRenderObjectWidget
SingleChildRenderObjectWidget
MultiChildRenderObjectWidget
>  3. 代理 ProxyWidget
>  InheritedWidget  ParentDataWidget

>又分为图文，容器，组合，功能，手势


##### 8. future
> 通过then来完成future
> Completer用提供的值完成future
> 可取消CancelableOperation里面也是用到了CancelableCompleter
> CancelableCompleter 用到了 Completer

>Completer->\_asyncComplete->\_chainFuture->\_chainCoreFuture
>->then->\_addListener



##### 9. GestureDetector 手势事件 竞技场
竞技场管理员

创建竞技场
关闭竞技场
打扫竞技场
加上竞技场锁
释放竞技场锁

竞技场成员
失败或者获胜方法通知

竞技场
通过管理员通知成员失败或者获胜


竞技场胜负标志



> 1. 竞技场管理员(GestureArenaManager)
> 1.1 add 添加成员到竞技场 如果没有对应的竞技场会创建一个 map<pointer, \_GestureArena>
> 1.2 close 关闭竞技场
> 2. 竞技场 (GestureArenaEntry/\_GestureArena)
> 3. 竞技场成员(GestureArenaMember)
> 4. 竞技场胜负标志(GestureDisposition)




##### 10. 原始事件

Listener原始指针
>\_handlePointerEventImmediately
触发新事件时，flutter 会调用此方法
flutter会调用_handlePointerEventImmediately方法，
该方法中会调用child.hitTest()相当于递归对自述进行命中测试

命中测试
>hitTest
一般hitTestChildren或者hitTextSelf返回true
可以通过重写hitTextSelf强制返回true或者重写hitTest方法来修改命中测试
通过命中测试的标志是渲染对象加入到HitTestResult列表当中

>hitTestChildren
通过遍历调用child.hitTest()来决定返回值，如果遇到有child.hitTest()返回true就会终止遍历，直接返回true,
后面的就不会参与命中测试，意味着无法相应事件

>hitTextSelf
决定渲染对象是否通过命中测试，无论子组件是否通过命中测试






##### 10. 序列化
>User user = User();
>序列化
>String userStr = json.encode(user)
>反序列化
>Map userMap = json.decode(userStr)
>User user = User.fromJson(userMap);
>Map userMap = User.toJson(user);


###### 10. 1 常用注解
>@JsonSerializable(createToJson: false)
>@JsonKey(includeIfNull: false,name: 'date-of-birth')
>@JsonKey(name: 'prep-time',fromJson: \_durationFromMilliseconds,toJson: \_durationToMilliseconds)
>@JsonLiteral('data.json')
>@JsonKey(fromJson: \_dataFromJson)
>JsonConverter


###### 10. 2 常用依赖
json_annotation: ^4.6.0
json_serializable: ^6.3.1
build_runner: ^2.2.0





























