**DJI Mobile SDK FAQ**
**Mobile SDK  常见问答**

2018-01-29

**Table of Contents**
**目录**

**Getting Started**
**开始**

How can I become a DJI Developer? 如何成为 DJI 开发人员？
Where are the DJI Mobile SDK Resources? Mobile SDK  资源在哪里？
Are there any tutorials for the DJI Mobile SDK? 有没有 DJI Mobile SDK  的教程？
Where can I get the DJI SDK API Reference? 我可以在哪里取得 DJI SDK API 参考资料？
If I have questions, where can I get help? 如果我有问题, 我在哪里可以得到帮助？
How can I import and activate the DJI Mobile SDK in my own project? 如何在我自己的项目中导入和激活 DJI Mobile SDK？
Why does application registration fail? 为什么申请注册失败？

**Product Related**
**无人机相关**

Can I access SD card data without an SD card reader? 我可否在没有 SD 卡阅读器的情况下查阅 SD 卡资料？
How can I update my DJI Aircraft or OSMO's firmware? 如何更新我的 DJI 无人机或 OSMO 的固件？
How can I Unlock Travel Mode for Inspire 1? 如何解锁 Inspire 1的旅行模式？
How do I link the Remote Controller to an aircraft? 如何将遥控器连接到无人机上？
Do DJI products use WGS84 or NAD83 as the coordinate system? Dji 无人机是否使用 WGS84或 NAD83作为坐标系？

**General SDK**
**一般可持续发展基金**

Does the DJI Mobile SDK give access to all the functionality in the DJI GO App? Mobile SDK  是否可以访问 DJI GO APP中的所有功能？
Is a flight simulator available to test applications? 有没有可供测试申请的飞行模拟器？
Where can I download the simulator for testing the Mobile SDK app? 我可以在哪里下载测试Mobile SDK  APP的模拟器？
Why can’t I use the existing simulator for the Phantom 4? 为什么我不能用现有的模拟器来模拟精灵4？
What path does the aircraft take in a curved waypoint mission? 无人机在弯道飞行任务中走哪条路？
Why does yaw rotation cause the drone to drift when using Virtual Stick APIs? 为什么 yaw 旋转使得无人机在使用虚拟粘贴 api 时会漂移？
Does DJIWaypointMission allow only one waypoint? Djiwaypointmission 是否只允许一个方向？
For DJIWaypointTurnMode, if I set one waypoint's 对于 DJIWaypointTurnMode, 如果我设置一个 waypointturnMode, when will it take effect? 什么时候生效？
How do I fix the Mission Error "Distance between two adjacent waypoints is too large." ? 如何修正任务错误"两个相邻的路点之间的距离太大了。" ？
How do I fix the Mission Error "The total distance of waypoints is too large." ? 我如何修正任务错误"总的航迹距离太大。" ？

**Android**
**安卓系统**

After upgrading to DJI Android SDK 4.4.1, my android project crashes with "java.lang.NoClassDefFoundError" error, how to fix it?
How can I run the Android SDK Sample Code 如何运行 Android SDK 示例代码
How do I reset the default app behavior for a USB Accessory (DJI Product) on Android devices? 如何在安卓设备上重置 USB 配件(DJI 无人机)的默认APP行为？
How do I reset the default app behavior for a USB Accessory (DJI Product) on Samsung devices? 如何在三星设备上重置 USB 配件(DJI 无人机)的默认APP行为？
Why does my application crash when I run on Android 6.0 Marshmallow？ 为什么我的APP在安卓6.0版本的 Marshmallow 上运行时会崩溃？
Why can't my Android application connect to a DJI Product when using the DJI Mobile SDK 3.2.1 and Android 6.0 Marshmallow with targetSdkVersion 23? 为什么我的 Android APP在使用 DJI Mobile sdk3.2.1和 Android 6.0 Marshmallow with targetSdkVersion 23时, 为什么我的 Android APP不能连接到 DJI 无人机？

**Getting Started**
**开始**

**How can I become a DJI Developer?**
**如何成为 DJI 开发人员？**

Becoming a DJI developer is easy. Please see here for details.
成为一个 DJI 开发者很容易。 详情请浏览此网页。

**Where are the DJI Mobile SDK Resources?**
**Mobile SDK  资源在哪里？**

All documentation can be found on the DJI developer website.

所有文档都可以在 DJI 开发者网站上找到。

The SDK can be downloaded from the website .

可以从网站下载 SDK。

All sample code referenced in the tutorials is available on Github .

教程中引用的所有示例代码都可以在 Github 上获取。

**Are there any tutorials for the DJI Mobile SDK?**
**有没有 DJI Mobile SDK  的教程？**

Several tutorials for Android and iOS are available.

有几个关于 Android 和 iOS 的教程是可用的。

**Where can I get the DJI SDK API Reference?**
**我可以在哪里取得 DJI SDK API 参考资料？**

iOS API Reference

的 API 参考

Android API Reference

安卓 API 参考

**If I have questions, where can I get help?**
**如果我有问题, 我在哪里可以得到帮助？**

You can use the following methods to get help:

你可以使用下面的方法来获得帮助:

StackOverFlow

堆栈溢出

Post questions in StackOverFlow with DJI SDK tag: dji-sdk

在 StackOverFlow 发布 DJI SDK 标签的问题: DJI-SDK

DJI SDK Forum

Dji SDK 论坛

http://forum.dev.dji.com/forum-90-1.html

90-1. html

Github Issues

Github 问题

iOS Github Issues

Android Github Issues

安卓 Github 问题

Send Email

发送电子邮件

If you prefer email, please send to dev@dji.com for help.

如果你喜欢电子邮件, 请发送到 dev@dji. com 寻求帮助。

**How can I import and activate the DJI Mobile SDK in my own project?**
**如何在我自己的项目中导入和激活 DJI Mobile SDK？**

The following two links from the documentation can help here:

下面两个文档链接可以帮助你:

Xcode Project Integration

项目集成

Android Studio Project Integration

Android Studio项目集成

**Why does application registration fail?**
**为什么申请注册失败？**

The first time the application is initialized after installation, it connects to a DJI Server to verify it's authorized to use the DJI Mobile SDK by sending the Application Key. This process is called registration. Reasons for why it might fail include:

第一次在安装后初始化APP, 它连接到 DJI 服务器, 以验证它是否被授权通过发送APP密钥来使用 DJI Mobile SDK。 这个过程叫做注册。 其失败的原因包括:

Application needs internet connectivity the first time it is run after installation (successful registration is locally cached, so internet connectivity is not required after the first initialization). APP在安装后第一次运行时需要互联网连接(成功的注册是局部缓存的, 因此在第一次初始化后不需要互联网连接)
App key is incorrect. Check in the APP键是错误的。 检查一下 User Center 用户中心 to confirm the application key, or 确认APP的密码匙create 创建 one if it hasn't been created yet. 如果它还没有被创造出来的话
Bundle Identifier (iOS) or Package Name (Android) isn't the same as the one associated with the App Key. See how to Bundle Identifier (iOS)或者包名(Android)不同于与APP密钥相关的标识符。 看看怎么做create 创建 an application key and associate it with the correct application identifier. 一个APP密钥, 并将其与正确的APP标识符关联起来
If you are using iOS 10, please check 如果你正在使用 iOS 10, 请检查here 给你 to enable "Data Protection" in your Xcode project. 在您的 Xcode 项目中启用"数据保护"

**Product Related**
**无人机相关**

**Can I access SD card data without an SD card reader?**
**我可否在没有 SD 卡阅读器的情况下查阅 SD 卡资料？**

Yes, you can use a USB cable to connect between DJI Products and your computer to access the SD card data directly. Each product's manual illustrates the location of the USB port on the product.

可以, 您可以使用 USB 电缆连接 DJI 无人机和您的计算机直接访问 SD 卡数据。 每个无人机的手册都说明了无人机上的 USB 接口的位置。

**How can I update my DJI Aircraft or OSMO's firmware?**
**如何更新我的 DJI 无人机或 OSMO 的固件？**

Each product's web page at www.dji.com has a firmware installation manual in the Downloads section.

每个无人机的网页在 www.dji.com 有一个固件安装手册在下载部分。

**How can I Unlock Travel Mode for Inspire 1?**
**如何解锁 Inspire 1的旅行模式？**

The aircraft is in Travel Mode during delivery. In this mode, the landing gear is half way between the retracted (up) and deployed (down) state. The landing gear needs to be deployed to attach a camera. Follow these steps to deploy the landing gear (put the aircraft in Landing Mode):

无人机在交付过程中处于旅行模式。 在这种模式下, 脚架在回缩(上升)和部署(下)状态之间的一半。 脚架需要安装在摄像头上。 按照这些步骤部署脚架(将无人机置于降落模式) :

Place the Inspire on a flat surface clear of any obstructions (the propellors do not need to be installed). 将激发器放置在一个没有任何障碍物的平面上(动力不需要安装)
Insert the battery into the battery compartment. 将电池插入电池室
Power on the Remote Controller and the Inspire. 遥控器和悟器的动力
Toggle the Transformation Switch up and down at least four times. 切换转换开关至少上下四次
The aircraft body will slowly raise as the landing gear deploys. 随着脚架部署, 无人机机身将缓慢地升起
Power off the aircraft. 关闭无人机


Note:

注意:

If you have purchased the dual remote controller version, you must use the Master remote controller to deactivate Travel Mode. 如果您购买了双遥控器版本, 则必须使用主遥控器来关闭旅行模式
Be sure to remove the camera from the aircraft before switch from Landing Mode to Travel Mode. 在从降落模式切换到旅行模式之前, 一定要把摄像头从无人机上移开
The ultrasonic sensor underneath the aircraft is used to determine when the landing gear is at the right position. Smooth reflective surfaces will work better than rough, sound-absorbing surfaces (e.g. carpet). 无人机下方的超声波传感器用来确定脚架在正确的位置。 光滑的反光表面比粗糙的、吸音的表面(如地毯)更有效

**How do I link the Remote Controller to an aircraft?**
**如何将遥控器连接到无人机上？**

The remote controller is linked to your aircraft before delivery. Linking is only required when using a remote controller with an aircraft it did not ship with for the first time. Follow these steps to link a new remote controller:

遥控器在交付之前与您的无人机相连。 只有当使用遥控器使用第一次没有使用的无人机时, 才需要连接。 按照以下步骤链接一个新的遥控器:

Turn on the remote controller and connect to the mobile device. Launch the DJI GO app. 打开遥控器并连接到手机。 启动 DJI GO APP
Turn on the aircraft. 打开无人机
Enter “Remote Controller Settings” and tap “Linking Remote Controller” button as shown below. 输入"遥控器设置", 点击"连接遥控器"按钮, 如下所示


The remote controller is ready to link. The Remote Controller Status Indicator blinks blue and a beep is emitted. 遥控器已准备好连接。 遥控器状态指示灯闪烁蓝色, 并发出哔哔声


Locate the linking button on the side of the aircraft. The figures below show the Phantom 3, Phantom 4 and Inspire button positions. The M100 and M600 positions can be found in their respective manuals. Press the link button to start linking. The Remote Controller Status Indicator LED will display a solid green once the remote controller is successfully linked to the aircraft. 找到无人机侧面的链接按钮。 下面的图片显示了 Phantom 3, Phantom 4和 Inspire 按钮的位置。 M100和 M600职位可以在各自的手册中找到。 按下链接按钮开始链接。 一旦遥控器成功地与无人机连接, 遥控器状态指示灯将显示一个纯绿色
Phantom 3 Series 精灵3系列


Phantom 4 精灵4


Inspire Series 悟系列


Note: The remote controller will un-link itself from an aircraft if a new remote controller is linked to the same aircraft.

注: 如果新的遥控器与同一架无人机相连, 遥控器将自动脱离无人机。

**Do DJI products use WGS84 or NAD83 as the coordinate system?**
**Dji 无人机是否使用 WGS84或 NAD83作为坐标系？**

DJI products use WGS84 as the coordinate system.

Dji 无人机以 WGS84为坐标系。

**General SDK**
**一般可持续发展基金**

**Does the DJI Mobile SDK give access to all the functionality in the DJI GO App?**
**Mobile SDK  是否可以访问 DJI GO APP中的所有功能？**

Almost all of the functionality found in DJI GO is exposed in the Mobile SDK.

在 DJI 中发现的几乎所有的功能都在Mobile SDK  中暴露出来。

**Is a flight simulator available to test applications?**
**有没有可供测试申请的飞行模拟器？**

Yes, a flight simulator is available for all products and can be used both as visual verification that flight behavior is correct, and as an automated tool for CI systems.

是的, 所有无人机都可以使用飞行模拟器, 可以作为飞行行为正确性的可视化验证, 也可以用作 CI 系统的编程工具。

Documentation describing setup and use of the simulator.

描述模拟器设置和使用的文档。

**Where can I download the simulator for testing the Mobile SDK app?**
**我可以在哪里下载测试Mobile SDK  APP的模拟器？**

For Phantom 3 Series and Inspire 1 series, you can use the 对于精灵3系列和 Inspire 1系列, 您可以使用DJI PC Simulator Dji PC 模拟器 for testing. 为了测试
For Phantom 4 series, Inspire 2, M100, M600 and Mavic Pro, you can use 对于 Phantom 4系列, Inspire 2, M100, M600和 Mavic Pro, 您可以使用DJI Assistant 2 Dji 助手2 for testing. 为了测试
For more details of using the simulator, please refer to this tutorial: Aircraft Simulator.

有关使用模拟器的详细信息, 请参考本教程: 飞行模拟器。

**Why can’t I use the existing simulator for the Phantom 4?**
**为什么我不能用现有的模拟器来模拟精灵4？**

The Phantom 4 uses a different simulator application compared to Phantom 3, Inspire and Matrice series of aircraft.

与 Phantom 3、 Inspire 和 Matrice 系列无人机相比, Phantom 4使用了不同的模拟器APP。

The Phantom 4 simulator can be downloaded from here and an explanation of how to use it can be found here.

精灵4模拟器可以从这里下载和解释如何使用它可以在这里找到。

**What path does the aircraft take in a curved waypoint mission?**
**无人机在弯道飞行任务中走哪条路？**

Waypoint missions have two flight path modes:

Waypoint 任务有两种飞行路径模式:

Aircraft flies from waypoint to waypoint 无人机从一个路口飞到另一个地点
Aircraft flies a curved path where the waypoints define the curve, but the aircraft doesn't necessarily fly through the waypoint. 无人机在弯曲的路径上飞行, 但是无人机并不一定要飞过航道点
The curve is formed using a quadratic Bezier curve. The corner radius defines the start point of the Bezier curve.

曲线是用二次贝塞曲线形成的。 角半径定义了贝塞尔曲线的起点。

Consider three waypoints W0, W1, W2 where the curve is defined for W1. 考虑 W1曲线定义的三个 waypoint W0, W1, W2
P0 and P2 are the start and end points of the Bezier curve defined by P0,P1,P2 P0和 P2是由 P0, P1, P2定义的贝塞尔曲线的起始点和终点
d01 is the cornerRadiusInMeters. D01是基础辐射仪

**Why does yaw rotation cause the drone to drift when using Virtual Stick APIs?**
**为什么 yaw 旋转使得无人机在使用虚拟粘贴 api 时会漂移？**

This is a firmware bug. Virtual stick yaw angle can be set with either angle or angular velocity commands. This behavior is seen when using angle mode. As a temporary workaround, angular velocity can be used instead.

这是一个固件 bug。 无论是角度还是角速度, 都可以设置虚拟的偏航角。 使用角度模式时可以看到这种行为。 作为临时工作, 角速度可以代替。

**iOS:**

DJIFlightController *flightController = ...; //Get the flightController instance
flightController.yawControlMode = DJIVirtualStickYawControlModeAngularVelocity;
flightController.rollPitchControlMode = DJIVirtualStickRollPitchControlModeAngle;
flightController.verticalControlMode = DJIVirtualStickVerticalControlModeVelocity;
...
//Invoke the "sendVirtualStickFlightControlData:withCompletion:" method of DJIFlightController
...
Android:

**安卓系统:**

DJIFlightController flightController = ...; //Get the flightController instance
flightController.setYawControlMode(DJIFlightControllerDataType.DJIVirtualStickYawControlMode.AngularVelocity);
flightController.setRollPitchControlMode(DJIFlightControllerDataType.DJIVirtualStickRollPitchControlMode.Angle);
            flightController.setVerticalControlMode(DJIFlightControllerDataType.DJIVirtualStickVerticalControlMode.Velocity);         
...
//Invoke the "sendVirtualStickFlightControlData()" method of DJIFlightController
When yaw is controlled by angular velocity, the aircraft's yaw position can be controlled precisely by using a PID controller algorithm.

利用 PID 控制算法可以精确控制航空器的偏航位置, 使用 PID 控制算法可以精确控制偏航位置。

**Does DJIWaypointMission allow only one waypoint?**
**Djiwaypointmission 是否只允许一个方向？**

No, the minimum number of waypoints allowed in a DJIWaypointMission is 2.

不, 吉威特任务允许的最低运营点数是2个。

**For DJIWaypointTurnMode, if I set one waypoint's turnMode, when will it take effect?**
**对于 DJIWaypointTurnMode, 如果我设置一个 waypoint 的转换模式, 它什么时候生效？**
When the headingMode value of DJIWaypointMission is set to DJIWaypointMissionHeadingUsingWaypointHeading (iOS) or UsingWaypointHeading (android), the turnMode of Waypoint N takes effect when flying between Waypoint N and Waypoint N+1.

当 waypointpoint 任务的标题模式值设置为在 Waypoint n 和 waypoinn + 1之间飞行时, waypointn 的转换模式就会起作用。

**How do I fix the Mission Error "Distance between two adjacent waypoints is too large."?**
**如何修正任务错误"两个相邻的路点之间的距离太大了。" ？**

The Waypoint Mission automates the aircraft to fly through a list of waypoints, visiting one after the other. A limitation of the mission is that consecutive waypoints must have a separation of less than 2km and greater than 0.5m. In addition, the first and last waypoint of the mission must also have a separation of less than 2km and greater than 0.5m. If the separation of any consecutive waypoints or the separation of the first and last waypoint is larger than 2km, then this error will be raised.

飞点任务使无人机自动飞过一系列航路点, 一个接着一个地访问。 任务的一个限制是, 连续的航点必须有不到2公里和大于0.5米的距离。 此外, 任务的第一个和最后一个方向也必须有不到2公里和大于0.5米的隔离。 如果将任何连续的航道点或第一和最后一个航点的分离大于2公里, 则这个错误将会被提出。

**How do I fix the Mission Error "The total distance of waypoints is too large." ?**
**我如何修正任务错误"总的航迹距离太大。" ？**

For a waypoint mission, the total planned flight distance must be less than 40km. The total planned flight distance includes the sum of the:

对于中途飞行任务, 计划中的总飞行距离必须小于40公里。 计划飞行总距离包括:

Distance from current aircraft location to first waypoint 从目前无人机位置到第一个航点的距离
Sum of all distances between waypoints in mission 任务地点之间所有距离的总和
Distance from last waypoint to the homepoint. 从最后一个路口到家乡的距离
Please check the following diagram for more details:

详情请参阅下列图表:

distanceTooLarge

Note: The blue line represents "Distance 1", red line represents "Distance 2", and green line represents "Distance 3".

注意: 蓝线表示"距离1", 红线表示"距离2", 绿线表示"距离3"。

The home location can be set using:

可以使用以下方式设置家庭位置:

iOS:
- (void)setHomeLocation:(CLLocationCoordinate2D)homePoint
         withCompletion:(DJICompletionBlock)completion;
- (void)setHomeLocationUsingAircraftCurrentLocationWithCompletion:(DJICompletionBlock)completion;
Android: 安卓系统:
public abstract void setHomeLocation (DJILocationCoordinate2D homePoint, DJICommonCallbacks.DJICompletionCallback callback)
public abstract void setHomeLocationUsingAircraftCurrentLocation (DJICommonCallbacks.DJICompletionCallback callback)
For iOS, the DJISDKMissionError will be DJISDKMissionErrorMissionTotalDistanceTooLarge, and for Android, the DJIMissionManagerError will be MISSION_RESULT_WAYPOINT_TOTAL_TRACE_TOO_LONG.

对于 iOS 系统, DJISDKMissionError 将是 DJISDKMissionErrorMissionTotalDistanceTooLarge, 而对于 Android, DJIMissionManagerError 将是 MISSION result waypoint total trace too long。

Generally the total distance couldn't be larger than 40km, if that error occurs, it might be something related to the improper settings for the homepoint.

一般来说, 总的距离不能超过40公里, 如果出现这种错误, 可能与该住宅点的设置不当有关。

**Android**
**安卓系统**

**How can I run the Android SDK Sample Code?**
**如何运行 Android SDK 示例代码？**

The following tutorial can help here: Run Android Sample Application.

下面的教程可以帮助你: 运行 Android 示例APP。

**After upgrading to DJI Android SDK 4.4.1, my android project crashes with "java.lang.NoClassDefFoundError" error, how to fix it?**

Since in the Android SDK 4.4.1, some of the SDK classes now need to be loaded before using. Loading process is done by Helper.install(). Developer needs to call this method before using any SDK functionality. Failing to do so will result in unexpected crashes.

因为在 Android SDK 4.4.1中, 一些 SDK 类现在需要在使用之前加载。 装载过程由 Helper.install ()完成。 开发人员需要在使用任何 SDK 功能之前调用此方法。 如果不这样做, 将会导致意想不到的崩溃。

Please make sure you don't miss the following steps:

请确保你不会错过以下步骤:

In your project's build.gradle file, please add the packagingOptions to avoid unexpected crashes, and also add the compile and provided dependencies to to import the DJI Android SDK maven dependency as shown in this Integrate SDK into Application tutorial.

在您的项目的 build.gradle 文件中, 请添加 packagingOptions, 以避免意外崩溃, 并添加编译和提供的依赖来导入 DJI Android SDK maven 依赖项。

Create a new MApplication class and invoke the install() method of Helper class to load the SDK classes before using any SDK functionality. Failing to do so will result in unexpected crashes. Also, you should initialize SDK class objects (Like BaseProduct.BaseProductListener, BaseComponent.ComponentListener and DJISDKManager.SDKManagerCallback) inside the onCreate() method. For more details, please check the Creating a Camera Application tutorial.

创建一个新的 MApplication 类并调用 Helper 类的安装方法来在使用任何 SDK 功能之前加载 SDK 类。 如果不这样做, 将会导致意想不到的崩溃。 此外, 您应该在 onCreate ()方法中初始化 SDK 类对象(如 baseproduct.basproductlistener, BaseComponent.ComponentListener 和 djisdkmanagermanagercallback)。 更多的细节, 请查看创建一个摄像头APP教程。

**How do I reset the default app behavior for a USB Accessory (DJI Product) on Android devices?**
**如何在安卓设备上重置 USB 配件(DJI 无人机)的默认APP行为？**

DJI Products that connect to Android mobile devices over USB do so through the AOA (Android Open Accessory) protocol. DJI GO, and DJI Mobile SDK applications support this protocol. When a USB accessory (DJI Product) is connected to the Android mobile device, Android will automatically open the application which supports it, or has been designated the default application for that accessory.

连接到安卓手机的 DJI 无人机通过 AOA 协议(Android Open accessaccessory)协议连接到 Android 手机上。 和 DJI Mobile SDK APP支持这个协议。 当一个 USB 配件(DJI 无人机)连接到 Android 手机时, Android 将自动打开支持它的APP, 或者被指定为该配件的默认APP。

If there is more than one application that supports the accessory, and no application has been designated as the default, then the user will be given an option for which application to open. Usually, the user will also be able to select whether the application should only be opened for this connection, or should be considered the default application going forward.

如果有多个APP支持该配件, 而且没有指定APP作为默认, 那么将给用户一个打开APP的选项。 通常, 用户还可以选择是否只为此连接打开APP, 或者应该被视为未来的默认APP。

Once an application is tied as the default application to an accessory, no other applications will be able to use that accessory. For example, if DJI GO is the default application, then no other SDK based application will work the DJI products.

一旦将APP绑定为配件的默认APP, 则没有其他APP能够使用该配件。 例如, 如果 DJI GO 是默认的APP, 那么没有其他基于 SDK 的APP可以使用 DJI 无人机。

To solve this, the default behavior needs to be removed for the accessory. For example, if the DJI GO is the default application, navigate in Android to Settings->Apps->DJI GO->Open by default and you should see a similar screen to this:

为了解决这个问题, 需要为配件删除默认行为。 例如, 如果 DJI GO 是默认的APP, 默认情况下在 Android 中导航到 Settings-Apps-DJI GO-Open, 你应该会看到类似的屏幕:



Click on the CLEAR DEFAULTS button.

点击 CLEAR default 按钮。

If you want to change the default application from DJI GO to the SDK-based app, make sure both applications are completely terminated. Then, after clearing defaults as above, reconnect the remote controller and Android should ask which application to open and whether to make it default or not.

如果您想将 DJI GO 的默认APP更改为基于 sdk 的APP, 请确保两个APP都被完全终止。 然后, 在清除了上面的默认设置之后, 重新连接遥控器和安卓系统应该询问要打开哪个APP, 以及是否默认。

**How do I reset the default app behavior for a USB Accessory (DJI Product) on Samsung devices?**
**如何在三星设备上重置 USB 配件(DJI 无人机)的默认APP行为？**

DJI Products that connect to Android mobile devices over USB do so through the AOA (Android Open Accessory) protocol. DJI GO, and DJI Mobile SDK applications support this protocol. When a USB accessory (DJI Product) is connected to the Android mobile device, Android will automatically open the application which supports it, or has been designated the default application for that accessory.

连接到安卓手机的 DJI 无人机通过 AOA 协议(Android Open accessaccessory)协议连接到 Android 手机上。 和 DJI Mobile SDK APP支持这个协议。 当一个 USB 配件(DJI 无人机)连接到 Android 手机时, Android 将自动打开支持它的APP, 或者被指定为该配件的默认APP。

If there is more than one application that supports the accessory, and no application has been designated as the default, then the user will be given an option for which application to open. Usually, the user will also be able to select whether the application should only be opened for this connection, or should be considered the default application going forward. However, some Samsung devices do not give this additional option, and will instead make the selected application the default application.

如果有多个APP支持该配件, 而且没有指定APP作为默认, 那么将给用户一个打开APP的选项。 通常, 用户还可以选择是否只为此连接打开APP, 或者应该被视为未来的默认APP。 然而, 一些三星设备没有提供这个附加选项, 而是将选定的APP作为默认APP。

Once an application is tied as the default application to an accessory, no other applications will be able to use that accessory. For example, if DJI GO is the default application, then no other SDK based application will work the DJI products.

一旦将APP绑定为配件的默认APP, 则没有其他APP能够使用该配件。 例如, 如果 DJI GO 是默认的APP, 那么没有其他基于 SDK 的APP可以使用 DJI 无人机。

To solve this, the default behavior needs to be removed for the accessory. For example, if the DJI GO is the default application, navigate in Android to Settings->Apps->DJI GO->Set as default and you should see a similar screen to this:

为了解决这个问题, 需要为配件删除默认行为。 例如, 如果 DJI GO 是默认APP, 则在 Android 中导航到设置-APP-DJI GO-Set 作为默认设置, 您应该看到类似的屏幕:



Click on the CLEAR DEFAULTS button. The next time the DJI product is connected to the mobile device, the user will be given the option to select the application to open with it.

点击 CLEAR default 按钮。 下一次 DJI 无人机连接到手机时, 用户将被赋予选择使用它的APP的选项。

**Why does my application crash when I run on Android 6.0 Marshmallow?**
**为什么我的APP在安卓6.0版本的 Marshmallow 上运行时会崩溃？**
Please update your application‘s Android SDK to the latest 3.2.2 version. You can download it from here .

请将您的APP的 Android SDK 更新到最新的3.2.2版本。 你可以在这里下载。

For more details, please check the Importing and Activating DJI SDK in Android Studio Project tutorial.

有关更多细节, 请查看Android Studio项目教程中的导入和激活 DJI SDK。

**Why can't my Android application connect to a DJI Product when using the DJI Mobile SDK 3.2.1 and Android 6.0 Marshmallow with targetSdkVersion 23?**
**为什么我的 Android APP在使用 DJI Mobile sdk3.2.1和 Android 6.0 Marshmallow with targetSdkVersion 23时, 为什么我的 Android APP不能连接到 DJI 无人机？**
Runtime Permissions are a new feature of Android 6.0.

运行时权限是 Android 6.0的一个新特性。

You can add the following code to request permissions before you connect to the internet to register your application to use the DJI SDK:

您可以在连接到互联网之前添加以下代码请求权限, 以注册您的APP, 以使用 DJI SDK:

// When the compile and target version is higher than 22, request the following permissions at runtime.
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
          ActivityCompat.requestPermissions(this,
                  new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.VIBRATE,
                          Manifest.permission.INTERNET, Manifest.permission.ACCESS_WIFI_STATE,
                          Manifest.permission.WAKE_LOCK, Manifest.permission.ACCESS_COARSE_LOCATION,
                          Manifest.permission.ACCESS_NETWORK_STATE, Manifest.permission.ACCESS_FINE_LOCATION,
                          Manifest.permission.CHANGE_WIFI_STATE, Manifest.permission.MOUNT_UNMOUNT_FILESYSTEMS,
                          Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.SYSTEM_ALERT_WINDOW,
                          Manifest.permission.READ_PHONE_STATE,
                  }
                  , 1);
      }
Then build and run your application, press "Allow" in the permission request alert as shown below:

然后构建并运行您的APP, 在权限请求提醒中按"允许", 如下所示:

requestPermission

After restarting the application, it should now. This process only needs to be completed once.

重新启动APP后, 现在应该可以了。 这个过程只需要完成一次。


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)