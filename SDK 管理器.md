**SDK Manager**
**SDK管理器**

2016-06-24

**Introduction**
**引言**

Application registration to use the DJI Mobile SDK, product connection, debugging and logging services are handled through the SDK manager class DJISDKManager.
APP注册使用 DJI Mobile SDK , 无人机连接,调试和日志输出通过SDK管理器类DJISDKManager处理。

The class also provides the instance of the product connected to the mobile device, from which control, state and components can be accessed.
该类还提供了连接到手机的无人机的实例,从中可以访问控件、状态和组件。

**Registration**
**注册**

Applications need permission to initialize the DJI Mobile SDK. During application development, a unique application key (App Key) needs to be generated and included in the source code. When the application is first run, this key will be sent to a DJI server to validate the application can use the SDK. If successful, the result will be locally cached on the mobile device. Every subsequent initialization of the application on the mobile device will check the local cache if there is no connection to the internet.
初始化 DJI Mobile SDK后获取Applications需要的权限。在APP开发过程中,需要生成一个唯一的APP KEY,并将其包含在源代码中。 当APP第一次运行时,KEY值将被发送到 DJI 服务器,以验证APP可以使用DJI Mobile SDK。如果成功,结果将在手机上进行缓存。 随后在手机上初始化APP时,如果与互联网没有连接,将检查本地缓存。

Therefore, the first time an application is run on a mobile device, the mobile device will need to have an internet connection. After that, an internet connection will not be required to initialize the DJI Mobile SDK, but connectivity will be used when available to confirm the application still has authorization to control DJI products.
因此,第一次在手机上运行APP时,手机需要联网。在此之后,不需要联网来初始化DJI Mobile SDK,但是APP再次连接到遥控器后需要确认APP仍然有权访问控制无人机。

This process is called registration, and is made available through the SDK Manager.
这个过程称为注册, 并通过 SDK Manager 提供。

Note: Some DJI products use WiFi as the connection between the mobile device and the product. The product is the access point and the mobile device is the client, which means no internet connectivity will exist through the WiFi connection for the mobile device. If using such a product, the first time the application is run should either be when the product is not connected to the mobile device, or the mobile device will need to have a cellular data connection. After the first successful registration, connectivity is not a requirement.
注意: 一些 DJI 无人机使用 WiFi 作为手机和无人机之间的连接。该无人机是接入点,手机是客户端,这意味着无法通过手机的 WiFi 连网。如果使用这样的无人机,第一次运行APP应该是当无人机未连接到手机时,同时手机需要有一个数据连接。在第一次成功注册之后, 就不需要再次注册了。

**Product Connection**
**无人机连接**

Once registered, the application can be connected to the product. The class method startConnectionToProduct can be used to initiate the connection between application and product assuming the mobile device is already physically connected to the product (through either USB or WiFi).
一旦注册成功,APP可以连接到无人机。如果手机已经物理连接到无人机（通过USB或WiFi），startConnectionToProduct方法可用于启动APP和无人机之间的连接。

The SDK manager can close the connection when desired. For iOS, the SDK manager can automatically close the connection when the application enters the background if desired.
SDK Manager可以在需要的时候关闭连接。对于 iOS设备,SDK管理器可以在APP进入后台时自动关闭连接。

Once connected, the SDK manager provides an instance to the connected product. The product instance can be used to control and receive state information about the components of the product.
一旦连接成功,SDK Manager为连接的无人机提供了一个实例。无人机实例可用于控制和接收关于无人机组件的状态信息。

**Debug Mode and Bridge App**
**调试模式和无线调试APP**

iOS development requires the mobile device be connected to Xcode directly through USB to use native debugging and profiling tools. As some DJI products use the USB port to connect to the remote controller, this can make application development difficult.
Ios 开发需要手机直接通过 USB 连接到 Xcode, 以使用本地的调试和分析工具。 由于一些 DJI 无人机使用 USB 接口连接到遥控器, 这会使APP开发变得困难。

DJI provides a Bridge App to resolve this. Debug mode can be turned on in the SDK Manager which will reroute all USB communication to WiFi. A second mobile device running the bridge app connects to the remote controller and relays WiFi communication. Alternatively, the iOS simulator can connect to the Bridge App over WiFi if only one mobile device is available.
使用Bridge APP来解决这个问题。调试模式可以在SDK Manager 中打开,它可以将所有USB通信重新路由到WiFi。运行Bridge APP的第二个手机连接到遥控器并且中继WIFI通信。或者,如果只有一个手机,iOS模拟器可以通过 WiFi 连接到 Bridge App。

The SDK Bridge App is available to be downloaded from Apple App Store and you can get the tutorial for using the Bridge App from here.
可以从苹果应用商店下载 SDK Bridge APP, 你可以从这里获取使用 Bridge APP的教程。

**Remote Logging**
**远程 Logging**

The SDK Manager also allows iOS applications to log remotely. Field testing is critical in application development, and remote logging allows simple ways to log events in real time to a remote server.
SDK Manager还允许iOS APP远程登录。在APP开发中,现场测试至关重要,远程Logging允许以简单的方法实时将事件记录到远程服务器。

A tutorial for using remote logging can be found here.
这里可以找到使用远程Logging的教程。


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)