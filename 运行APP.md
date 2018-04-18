**Run Application**
**运行APP**

2017-06-27

**Prepare Product**
**准备无人机**

The user manual for each product should be reviewed to understand the full product setup (visit http://www.dji.com and navigate to the downloads page for each product). This section details some of the key points to remember.
仔细查看无人机使用指南,以了解完整的无人机设置(访问 http: / / www.dji.com, 并导航到每个无人机的下载页面)。 这一部分详细介绍了一些需要记住的关键点。

**Charge Batteries**
**充电电池**

Generally, all batteries of a product should be charged before running an application for best experience. This can include aircraft batteries, remote controller batteries, handheld gimbal batteries, and aircraft mounted gimbal batteries (for the Ronin MX). When a battery is too low, an aircraft may return home or land early in the application, or might not take off at all.
通常，在运行APP以获得最佳体验之前，应先对无人机的所有电池进行充电。包括飞机电池，遥控器电池，手持式稳定器电池和无人机上安装的稳定器电池（用于Ronin MX）。当电池电量过低时，飞机可能会返航或在APP中提前降落，或者根本不能起飞。

**Activate Product**
**激活无人机**

Any new product will need to be activated through DJI GO before being used for the first time. DJI GO is available on the iOS App Store and Google Store and can be used to activate a product.
任何的新无人机在第一次使用之前都需要通过 DJI 启动。在iOS应用商店和谷歌商店上都有 DJI GO, 可以用来激活一个无人机。

**Upgrade Product Firmware**
**升级无人机固件**

Aircraft, remote controller and/or handheld controller firmware should be updated to the most recent release before beginning application testing and debugging. Different products sometimes have different processes for checking firmware version and upgrading firmware. Each product's page at http://www.dji.com has instructions in the Downloads section for upgrading firmware.
在开始APP测试和调试之前，应将飞机，遥控器固件更新到最新版本。不同的产品在检查固件版本和升级固件时有时会有不同。http://www.dji.com 上的每个产品页面都有关于升级固件的说明。

**Remote Controller Flight Mode Switch**
**遥控器飞行模式开关**

For aircraft, the remote controller FAP or ASP flight mode switch needs to be in a specific position to accept SDK commands that change flight orientation and automate flight. Remote controllers and aircraft can sometimes be interchanged making the FAP/ASP switch configuration have several options.
对于无人机，遥控器的FAP或ASP飞行模式开关需要处于特定位置才能接收改变航向和自动飞行的SDK命令。遥控器和飞机有时可以互换，使得FAP / ASP开关配置有多种选择。

**Internet Connectivity**
**连网**

Any SDK application will need internet connectivity the first time it runs to register with DJI and get authorization to use the SDK. After the first successful registration, the authorization will be stored locally, and internet connectivity will not be required for registration.
首次运行时，任何基于DJI SDK开发的APP都需要连网才能注册并获得使用SDK的授权。首次成功注册后，授权将存储在本地，并且不需要连网进行注册。

**Connect Mobile Device and Run Application**
**连接手机并运行APP**

There are several connection configurations between mobile device and product:
在手机和无人机之间有几种连接方法:

Mobile device -> USB -> Remote Controller -> Lightbridge/OcuSync -> Aircraft 
Mobile device -> WiFi -> Remote Controller -> WiFi -> Aircraft 
Mobile device -> WiFi -> Handheld Gimbal 

There are several ways to initialize all products and run an application. An example for USB and WiFi connection scenarios is given below.
有几种方法可以初始化所有无人机并运行APP。下面是一个关于 USB 和 WiFi 连接场景的示例。

**USB Connection Procedure**
**Usb 连接程序**

Mavic Pro, Phantom 4, Phantom 4 Professional, Phantom 3 Professional, Phantom 3 Advanced, Inspire series, Matrice Series:

1.Turn on the Remote Controller. 
1.打开遥控器

Turn on the Aircraft and wait until the Remote Controller has connected with the Aircraft. 
打开无人机,等待遥控器与无人机连接

Connect iOS/Android Mobile Device to the Remote Controller using a Lightning (iOS) or USB (Android) cable. 使用Lightning或 USB (Android)线将手机连接到遥控器

Run Application on the Mobile Device. 
在手机上运行APP

Note:
注意:

If using an Android device, the DJI Remote Controller needs to support AOA . All recent versions of the firmware support AOA. AOA is supported if when the Sample Application connects with the Android device, a dialog similar to that below appears:
如果使用安卓设备, DJI遥控器需要支持AOA。所有最新版本的固件支持AOA。DemoAPP安装到Android设备后,则会出现下面的对话框:
![](https://devcn.djicdn.com/images/application-development-workflow/android_dialog-674c5a5c67.png)
dialog

To learn how to change the default app for USB accessory, please check these two FAQs: Android Device, Samsung Device.
要了解如何更改 USB 配件的默认APP, 请检查这两个常见问答: Android 设备, 三星设备。

**WiFi Connection Procedure**
**Wifi 连接程序**

Phantom 3 Standard, Phantom 3 4K, Spark:
精灵3标准, 精灵34k, 晓:

Turn on the Remote Controller. 
打开遥控器

Connect Mobile Device to the WiFi network created by the Remote Controller. 
将手机连接到遥控器创建的 WiFi 网络

Turn on the Aircraft and wait until the Remote Controller has connected with the Aircraft. 
打开无人机,等待遥控器与无人机连接

Run Application on the Mobile Device. 
在手机上运行APP

Osmo, Mavic Pro, Spark:

Turn on the product (Osmo or aircraft). 
打开无人机(Osmo 或无人机)

Connect Mobile Device to the WiFi network created by the product. 
将手机连接到无人机创建的 WiFi 网络

Run Application on Mobile Device. 
在手机上运行APP


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)