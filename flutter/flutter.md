
[TOC]



####  framework.dart

>ObjectKey
GlobalKey
LabeledGlobalKey
GlobalObjectKey
Widget
StatelessWidget
> StatefulWidget
>\_StateLifecycle
> StateSetter
> StateSetter
ProxyWidget
ParentDataWidget
InheritedWidget
RenderObjectWidget
LeafRenderObjectWidget
SingleChildRenderObjectWidget
MultiChildRenderObjectWidget
\_ElementLifecycle
\_InactiveElements
ElementVisitor
BuildContext
BuildOwner
NotifiableElementMixin
\_NotificationNode
\_isProfileBuildsEnbledFor
Element
\_ElementDiagnosticableTreeNode
ErrorWidgetBuilder
ErrorWidget
WidgetBuilder
IndexedWIdgetBuilder
NullableIndexedWIdgetBuilder
TransitionBuilder
ComponentElement
StatelessElement
StatefulElement
ProxyElement
ParentDataElement
InheritedElement
RenderObjectElement
LeafRenderObjectElement
SingleChildRenderObjectElement
MultiChildRenderObjectElement
IndexedSlot
\_NullElement
\_NullWidget



##### 1. Bindding
> FlutterWidgetsBinding
> WidgetsBinding
> RendererBinding
> ScheduerBinding
> PaintingBinding
> ServicesBinding
> GestureBinding
> SemanticsBinding

###### 1.1.  runApp 干了啥
> * root节点如何生成
    >BindingBase initInstances
    >重写initInstances
    > 构造方法调用了initInstances
    > 创建WidgetsBinding initInstances  
    > BuildOwner() \_handleBuildScheduled
    > 创建RendererBinding  initInstances  
    > \_pipelineOwner initRenderView
    > RenderObjectToWidgetAdapter
    > 通过传入的rootWidget和RenderObject生成对象
    > 调用attachToRenderTree createElement mount
    >  生成RenderViewElement
    > RenderViewElement 和Widget RenderObject就关联到一起了
> * 子节点如何生成的
    > mount 方法中用到了_rebuild
    > 然后调用了updateChild




###### 1.2.  GestureBinding 管理指针事件的 Flutter 框架类 干了啥

> 给
> platformDispatcher.onPointerDataPacket = _handlePointerDataPacket;
> _flushPointerEventQueue
> handlePointerEvent
> _handlePointerEventImmediately
> dispatchEvent








##### 2. Widget

###### 2.1.  framework中的widget
>Widget
>StatelessWidget
>StatefulWidget
>ProxyWidget
>ParentDataWidget
InheritedWidget
RenderObjectWidget
LeafRenderObjectWidget
SingleChildRenderObjectWidget
MultiChildRenderObjectWidget
ErrorWidget
ErrorWidgetBuilder
WidgetBuilder
IndexedWIdgetBuilder
NullableIndexedWIdgetBuilder
> \_NullWidget


###### 1.2 widget

```dart
abstract class Widget extends DiagnosticableTree {
  /// 为子类初始化 [key]
  const Widget({ this.key });
 
  /// 控制一个小部件如何替换树中的另一个小部件。如果两个小部件的 [runtimeType] 和 [key] 属性分别为 ///[operator==]，则新/小部件通过更新底层元素（即通过使用新小部件调用 [Element.update] ///）。否则，从树中删除旧元素，将新小部件膨胀为一个元素，并将新元素插入树中。此外，使用 [GlobalKey] 作为小部件的 [key] ///允许元素在树周围移动（更改父级）而不会丢失状态。当找到一个新的小部件（它的键和类型与同一位置的前一个小部件不匹配），但在前一帧的树中的其他地方有一
  ///个具有相同全局键的小部件，则该小部件的元素被移动到新位置。通常，作为另一个小部件的唯一孩子的小部件不需要显式键。另见：[Key] 和 [GlobalKey] 的讨论。
 
  final Key? key;

  /// 将此配置解析为具体实例。给定的小部件可以在树中包含零次或多次。特别是给定的小部件可以多次放置在树中。每次将一个小部件放入树中时，它都会膨胀为一个 ///[Element]，这意味着多次合并到树中的小部件将被解析多次
  
  @protected
  @factory
  Element createElement();

  @override
  @nonVirtual
  int get hashCode => super.hashCode;

	///`newWidget` 是否可用于更新当前具有 `oldWidget` 作为其配置的 [Element]。当且仅当两个小部件的 [runtimeType] 和 [key] ///属性为 [operator==] ///时，使用给定小部件作为其配置的元素可以更新为使用另一个小部件作为其配置。如果小部件没有键（它们的键为空），那么如果它们具有相同的类型，则它们被认为是匹配的，即使它们的子级完全不同
 static bool canUpdate(Widget oldWidget, Widget newWidget) {
    return oldWidget.runtimeType == newWidget.runtimeType
        && oldWidget.key == newWidget.key;
  }
}
```



##### 2. Element
##### 3. RenderObject