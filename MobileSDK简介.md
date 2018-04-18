**Mobile SDK Introduction**
**Mobile SDK 简介**

2017-06-27

The DJI Mobile SDK is a software development kit designed to give developers access to the capability of DJI's aircraft and handheld camera products. The SDK simplifies the application development process by taking care of lower level functionality such as flight stabilization, battery management, signal transmission and communication. This way, the developer does not require a background in robotics or embedded systems and can instead focus on the application the DJI product is being integrated into.
Dji Mobile SDK 是一个软件开发工具包, 旨在让开发者获得编程 DJI 的无人机和手持稳定器的能力。 通过关注飞行稳定、电池管理、信号传输和通信等基础功能, SDK 简化了APP开发过程。 通过这种方式, 开发者不需要机器人或嵌入式系统的背景知识, 而是可以专注于开发DJI无人机相关APP。

The SDK includes:
Sdk 包括:

a library/framework that can be imported into an Android or iOS app that give access to the DJI product 
一个可以导入安卓或 iOS APP的库 / 框架, 用以访问 DJI 无人机

an aircraft simulator and visualization tool 
飞行模拟器和可视化工具

debugger and remote logger for iOS  
Ios 的debugger和远程logger

sample code and tutorials 
示例代码和教程

this developer guide and API documentation 
开发者指南和 API 文档

This introduction will describe how the SDK connects to the products, what functionality the SDK provides, and an introductory architecture of the SDK.
这个介绍将描述 SDK 如何连接到无人机, SDK 提供的功能, 以及 SDK 的架构。

**Feature Overview**
**功能概述**

Many of DJI's product features and capabilities are accessible to developers through the SDK. Developers can automate flight, control the camera and gimbal, receive real time video and sensor data, download saved media from the product, and monitor state of the other components.
开发人员可以通过DJI SDK访问无人机的许多功能。开发人员可以实现飞行自动化，控制摄像头和稳定器，接收实时视频和传感器数据，从无人机下载已保存的多媒体以及监视其他组件的状态。

**Flight Control**
**飞行控制**

The DJI Mobile SDK allows three ways to control aircraft flight:
Mobile SDK 允许三种控制无人机飞行的方法:

  1.Manually: User pilots aircraft with remote controller while SDK allows monitoring live video and sensor data. 
  1.手动: 用户操控无人机与遥控器, SDK监测实时视频和传感器数据

  2.Virtual Stick Commands: SDK allows generation of remote controller stick movements virtually, simulating a pilot. 
  2.虚拟摇杆命令: SDK 允许虚拟摇杆生成真实遥控器摇杆操作, 模拟飞手

  3.Missions: Convenient, easy to implement high level control of the aircraft. For example, defined flight paths can be executed with a Waypoint mission. 
  3.编程任务: 操作方便, 易于实现对无人机的高度控制。 例如, 可以使用 Waypoint 任务执行自定义的飞行路线

Virtual stick commands and missions allow simple but powerful automated flight control of DJI aircraft.
虚拟摇杆命令和编程任务允许简单但强大的自动化控制 DJI 无人机。

**Camera**
**摄像头**

Camera and gimbal functionality is highly programmable and allows:
摄像头和稳定器功能是可编程的, 并且允许:

  Camera mode: Video and still image capture 
  摄像头模式: 视频和图片拍摄

  Exposure: Shutter, ISO, aperture and exposure compensation are all available to customize for maximum flexibility 
  曝光: 快门、 ISO、光圈和曝光补偿都可以自定义, 以达到最大的灵活性
  
  Image Parameters: Aspect ratio, contrast, hue, sharpness, saturation and filters 
  图像参数: 长宽比、对比度、色调、锐度、饱和度和滤镜
  
  Video Parameters: Resolution and frame rate 
  视频参数: 分辨率和帧率
  
  Direction: Using the gimbal, camera direction and motion can be automated 
  方向: 使用云台, 摄像头的方向和运动可以编程

**Live Video**
**实时视频**

The live video broadcast by the aircraft of the main camera feed is available through the DJI Mobile SDK. Live video is available even when the camera is capturing images or video to it's storage media.
无人机通过 DJI Mobile SDK  播放主摄像头的实时视频。 即使在摄像头拍摄图像或视频到SD卡时也可以获得实时视频。

**Sensor Data**
**传感器数据**

Rich sensor data is available through the SDK. GPS position, compass, barometer, flight velocity and altitude are some of the sensor readings available at up to 10 Hz through the Mobile SDK.
丰富的传感器数据可以通过 SDK 获取。 Gps 位置, 指南针, 气压计, 飞行速度和高度可通过Mobile SDK  提供的最高达10赫兹的传感器数据流。

**Download Media**
**下载多媒体**

Videos saved to the camera's storage media (SD card or solid state drive) is accessible to view and download through the DJI Mobile SDK. Both previews and full image data can be accessed.
存储在摄像头SD卡(或SSD)的视频可以通过 DJI Mobile SDK 进行查看和下载。还可以访问预览和完整图像数据。

**Remote Controller, Battery, Wireless Link**
**遥控器, 电池, 无线通信**

The remote controller, battery and wireless link can all be accessed through the SDK. Mostly these components provide state information, but some control is also possible.
遥控器、电池和无线链路都可以通过 SDK 访问。 大多数组件提供状态信息, 但也可能提供一些控制功能。

**Differences with Other SDKs**
**与其他 sdk 的差异**

Most iOS and Android applications will either create, manipulate and/or visualize data. However applications using DJI's Mobile SDK can be fundamentally different as they can interact with the world around the user.
大多数 iOS 和 Android APP会创建、操作和可视化数据。然而,使用DJI的Mobile SDK的APP可能有根本的不同, 因为它们可以与用户周围的世界进行交互。

Kinetic Energy: An aircraft can have a mass of several kilograms and move at speeds of up to 20 m/s. While the ability to programmatically change position is tremendously powerful, it also means an application can potentially damage the product it is controlling, or the environment the product is being controlled in. 
动能: 无人机的重量可以达到几公斤, 速度可达每秒20米。虽然以编程方式更改位置的能力是非常强大的, 但它也意味着APP可能会损毁无人机或者无人机的周围环境

Share Space: DJI's aircraft move in space shared by other people, structures and aircraft. DJI provides a geofencing system to prevent aircraft from entering critical space, but developers and users must still understand the local and federal rules of the environment the aircraft moves in. 
空域: DJI的无人机进入公共空域时。为防止无人机进入禁飞区, DJI 提供了一个禁飞区系统, 但是开发者和用户仍然必须理解当地政府相关的无人机规则

Highly Asynchronous: Wireless connectively can be unpredictable in challenging wireless environments. Sometimes it can take hundreds of milliseconds for a command to be transferred (assuming it ever does). While many developers are familiar with asynchronous programming techniques in networking, when commands aren't communicated on a robotic system, behavior in the physical world can be unexpected. 
高度异步: 无线通信在复杂的无线电环境中行为是不可预测的。有时, 一个命令传送可能需要几百毫秒。虽然许多开发人员熟悉网络中的异步编程技术, 当命令没有通过无线通信传递时, 真实世界中的行为可能是意想不到的

It is not possible as a developer to predict or programmatically assess the environment a user will operate in. An easy maneuver in an open environment, can be difficult in a confined space. Environments can be dynamic and might be sometimes safe, and other times not. Therefore it is important that both developers and users understand the capabilities and limitations of the products and their controlling applications.
作为开发人员, 不可能预测或以编程方式评估用户的飞行环境。 在一个开放的飞行环境中, 执行一个简单的操作,同样的操作在一个封闭的空间里是很困难的。环境可以是变化的, 有时可能是安全的, 有时则不是。 因此, 开发者和用户都必须了解无人机的能力和局限性以及它们的控制应用。

**Connection to Application and Product**
**连接到APP和无人机**

The following diagram illustrates how the DJI Mobile SDK fits into a mobile application, and how it is connected to a DJI aircraft.
下图说明 DJI Mobile SDK  如何与移动APP相匹配,以及它如何连接到DJI无人机。
![](https://devcn.djicdn.com/images/mobile-sdk-introduction/SDKBlockDiagram-1faf3c4b8c.png)

For a handheld camera product, the Remote Controller is replaced with a Handheld Controller and there is no aircraft or additional wireless link.
对于手持稳定器设备, 遥控器用手持式控制器取代, 没有无线链路。

A mobile application is built with the DJI Mobile SDK, the platform SDK (iOS or Android) and is run on the Mobile Device (Apple iPhone, iPad, Nexus phone, Nexus tablet etc).
APP由 DJI Mobile SDK和Android SDK构建, 运行在手机(苹果 iPhone、 iPad、 Nexus 手机、 Nexus tablet 等)上。

The mobile device connects to a DJI product either wirelessly with WiFi or through a USB cable depending on the product. For aircraft products, the mobile device connects to the remote controller, which connects wirelessly to the aircraft through another wireless link (for the Phantom 3 Standard, two wireless links connect the remote controller and aircraft). Detailed connectivity for each product is shown below.
手机通过WiFi或USB线无线连接到DJI无人机，具体取决于产品。对于无人机，手机连接到遥控器，遥控器通过另一条无线链路与无人机无线连接。下面详细显示了每种无人机的连接方式。
![](images/捕获.PNG)
Therefore, depending on the product, when a command is sent from the DJI Mobile SDK to an aircraft, the command might pass through several wireless links and cable connections.
因此, 根据无人机的不同, 当一个命令从 DJI Mobile SDK  发送到无人机上时, 该命令可能会通过几个无线链路和数据线连接。


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)