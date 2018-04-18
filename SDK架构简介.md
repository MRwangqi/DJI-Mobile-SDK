**SDK Architectural Overview**
**SDK 架构概述**

2016-06-24

The architecture is designed to be highly extensible. Abstract product and component classes are used so applications can control different products with the same code. Features that are not consistent across all generations of supported products can be queried at runtime, and those that are consistent will simply work.
该体系结构旨在具有高度可扩展性。使用抽象产品和组件类，因此APP可以使用相同的代码来控制不同的产品。可以在运行时查询各代支持产品中不一致的功能，并且只有那些一致的功能才会被运行。

For example, the large majority of features of the Phantom and Inspire series of products are consistent. Therefore an application written to support the Phantom 4 will, with the exception of unique Inspire 1 features, fully support the Inspire 1.
例如, 精灵和悟系列无人机的大部分特性是一致的。 因此, 一个支持 Phantom 4的APP, 除了特殊的 Inspire 1功能, 完全支持 Inspire 1。

This also means when new products are released, they will already work with existing applications (when that application is rebuilt with the latest SDK that supports the new product). Any new features of the new product will need to be added to the application, but all existing features will not need modification.
这也意味着当新无人机发布时, 他们可以使用现有的APP(当这个APP用支持新无人机的最新 SDK 重新生成时)。只有新无人机的新功能需要添加到APP中, 但是所有现有的功能都不需要修改。

**Hierarchy**
**层次结构**

A mobile application accesses the DJI Mobile SDK through several main classes illustrated in the diagram below.
一个移动APP通过下图所示的几个主要类访问 DJI Mobile SDK。
![](https://devcn.djicdn.com/images/sdk-architectural-overview/Architecture-47cd8a771d.png)

SDK Manager: Manages registration of the SDK, product connection and provides access to the product itself. 
SDK Manager: 管理SDK的注册, 无人机连接, 并提供对无人机本身的访问权限

Product: The aircraft or handheld product, this class holds basic product properties and contains the main product components. 
Product类: 无人机或手持稳定器, 该类拥有基本的Product属性, 包含主要Product组件

Component: Component classes describe the gimbal, camera, flight controller, remote controller and wireless link. The classes provide component control, state information and contain subcomponents. 
Component类: Component类抽象描述了稳定器、摄像头、飞控、遥控器和无线链路。 该类提供组件控制、状态信息和子组件

Mission: Classes that describe different missions such as Waypoint and ActiveTrack missions and hold their setup properties and status. 
Mission类: 描述不同任务的类, 例如航线规划和智能跟随, 并保存其设置属性和状态

Mission Control: Mission Control handles execution of missions. Either single missions can be run through dedicated mission operators, or a series of missions and actions can be run serially using the Timeline. 
任务控制: 任务控制处理任务的执行。 任何一个任务都可以通过专门的任务操作进行, 可以使用时间轴连续运行一系列的任务和动作


**Aircraft Product**
**无人机**

A more detailed description of the aircraft product class is below. The aircraft product holds a number of components and the component holds a number of subcomponents, all of which are accessible when the mobile device is connected to the aircraft through the remote controller (if the SDK registration is successful). If the connection between the remote controller and aircraft is lost, the remote controller object will persist (if the mobile device is still connected to the remote controller), while the product and all remaining components physically on the aircraft will become null.
以下是无人机类的更详细描述。该无人机包含多个组件，该组件包含若干子组件，当移动设备通过遥控器连接到飞机时（如果SDK注册成功），所有这些组件都可以访问。如果遥控器和飞机之间的连接丢失，则遥控器对象将持续存在（如果移动设备仍连接至遥控器），而无人机和无人机上的组件(镜头等)将变为空。
![](https://devcn.djicdn.com/images/sdk-architectural-overview/SDKAircraftArchitecture-ffe48f7d7d.png)

**Missions**
**任务**

Missions can be used to easily automate flight. For more details, please check the Missions section. All missions inherit from DJIMission so they can be handled by the Mission Control.
任务可以用来轻松编程飞行。 有关更多细节, 请查看任务部分。 所有任务都从 DJIMission 继承, 以便 Mission Control可以处理他们。
![](https://devcn.djicdn.com/images/sdk-architectural-overview/SDKMissionArchitecture-ad43b78292.png)


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)