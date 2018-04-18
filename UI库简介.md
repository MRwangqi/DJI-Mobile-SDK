**UI Library Introduction**
**UI库简介**

2017-05-11

Many applications that control DJI products using the DJI Mobile SDK share similar core functionalities. They will typically:
许多使用 DJI Mobile SDK  控制 DJI 无人机的APP拥有相似的核心功能。 他们通常会:

Show a live view of the camera feed 
显示摄像头的实时画面

Show product state (aircraft telemetry, battery level, signal strength, etc.) 
显示无人机状态(无人机状态监测、电池水平、信号强度等)

Allow the user to review and change product settings 
允许用户检查和更改无人机设置

Have basic functionalities such as automatic take off, land, go home. 
具备自动起飞、降落、返航等基本功能

To make an application, a developer typically has to provide this set of core functionalities before adding some unique ones.
在添加一些特殊的功能之前, 开发人员通常需要提供这一组核心功能。

The DJI UI Library provides UI elements that have these core functionalities, hence can be used to speed up development time. In fact, by using the default UI Library, an application can be created with no additional lines of code. It looks like:
Dji UI 库提供具有这些核心功能的 UI 元素, 因此可以用来加快开发进度。 事实上, 通过使用默认的用户界面库, 可以创建一个没有附加代码行的APP。 它看起来像:
![](https://devcn.djicdn.com/images/product-introduction/defaultScreen-78218e7dc8.png)
DefaultScreen

Developers can pick and choose which parts of the UI Library they want to include, exclude and customize.
开发人员可以选择他们想要包含、排除和定制UI 库的某些部分。

UI Library is available in the DJI Mobile SDK v4.0 and later.
UI库可以在 DJI Mobile SDK v4.0和以后的版本中使用。

**Concepts Overview**
**概念概述**

UI Library has three main UI categories:
库有三个主要 UI 类别:

Widget: An independent UI element that gives state or simple control (e.g. battery indicator, or automatic take-off button) 
小工具: 单独的UI 元素, 它提供状态或简单的控制(例如电池指示器或自动起飞按钮)

Collection: (iOS only) An organized collection of widgets that are related to each other (e.g. camera exposure state) 
集合: (只有 iOS)一组相互关联的组织集合(例如摄像头曝光状态)

Panel: Complex menus and settings views with rich UI elements (e.g. camera settings) 
控制面板：具有丰富UI元素的复杂菜单和设置界面（例如摄像头设置）

All UI elements can simply be included in an application without extra maintenance. They are already tied to the DJI Mobile SDK, and will start updating themselves after instantiation.
所有 UI 元素都可以简单地包含在一个APP中, 而不需要额外的编码。 他们已经绑定到 DJI Mobile SDK  上, 并将在实例化之后开始初始化自己。

The Android and iOS UI Library API reference has the complete list of UI elements available.
Android UI 库 API 参考，可用的UI元素列表。

**Widget**
**小工具**

A widget is the simplest component of the UI Library. It typically represents a simple state element or gives a simple control. Some examples of widgets include:
小工具是 UI 库最简单的组件。 它通常表示一个简单的状态工具或给出一个简单的控件。 一些小工具的示例包括:
![](images/获.PNG)
			
**Customization**
**定制**

Widgets can be customized by either swapping the asset, or subclassing the widget.
可以更换UI来定制小工具, 也可以对小工具进行子类化。

**Asset Swap**
**定制UI**

Swapping the asset keeps the widget's behavior and logic, but changes its look.
定制UI保持了小工具的行为和逻辑, 但是改变了它的外观。

Android
安卓系统
Rename AAR file to have a zip extension 
将 AAR 文件重命名为 zip 扩展名

Unzip AAR file 
解压 AAR 文件

Replace assets in the following directories: 
在下列目录中更换UI:
- res/drawable
- res/drawable-hdpi-v4
- res/drawable-mdpi-v4
- res/drawable-xhdpi-v4
- res/drawable-xxhdpi-v4
- res/drawable-xxxhdpi-v4
Zip file and rename to replace the original AAR file 
压缩文件并重命名以替换原始 AAR 文件

Note: The image assets are required to be of the same pixel dimensions as the original ones.
注意: 图像必须与原始图像的像素尺寸相同。

**Subclassing**
**子类**

Android
安卓系统

In Android, subclassing can completely change the behavior and the look of Widgets. The steps are:
在 Android 中, 子类化可以完全改变 Widgets 的行为和外观。 这些步骤包括:

Override void initView(Context var1, AttributeSet var2, int var3) and inflate/initialize the custom layout. Remember, do not call super.initView().
重写 initView和 inflate/初始化自定义布局。 请记住, 不要调用 super.initView ()。

To get updated with information changes, override methods with the name following the onXXXChange pattern (for example, the onBatteryPercentageChange(int percentage) in BatteryWidget). This method will be called every time battery percentage changes. Overriding this method will give you the integer value of battery percentage. Remember, do not call super.initView().
要更新信息更改，请使用onXXXChange模式后面的名称覆盖方法（例如，onBatteryPercentageChange(int percentage)in BatteryWidget）。每次电池百分比发生变化时都会调用此方法。覆盖这个方法会返回给你电池百分比的整数值。请记住，不要调用 super.initView()。

To perform actions, use methods that follow the naming pattern performXXXAction.
要执行操作，请使用命名模式后面的方法performXXXAction。

**Collection**
**小工具组合**

A widget collection groups multiple, often related widgets together in an organized way. It controls the layout of the widgets relative to each other.
一个小工具组合以一种有组织的方式组合多个, 通常是相关的小工具。 它控制着相对于其他部件的布局。

Collections can also be created and used to organize pre-existing widgets.
还可以创建并使用小工具组合来组织预先存在的小工具。

Widget collections are used in iOS Only. Example of widget collections include:
只能 iOS 中使用小工具组合。 小工具组合的示例包括:

Status Bar Widget Collection
状态栏小工具组合
![](https://devcn.djicdn.com/images/ux-sdk-introduction/statusBarWidgetCollections-ccb6351fbb.png)

**Panels**
**控制面板**

Panels are more complex elements with rich information and control, such as settings menus or the pre-flight checklist.
控制面板是具有丰富信息和控制的更复杂的UI元素，例如设置菜单或飞行前检查清单。
![](images/捕.PNG)

		
**Customization**
**定制**

Due to the complexity of panels, customization is not currently provided.
由于面板的复杂性, 目前没有提供定制。

**Samples & Tutorials**
**示例和教程**

Sample projects are provided for the DJI UI Library:
为 DJI UI 库提供了示例项目:

Android UI Library Github Sample
Android UI 库 Github 示例


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)