**Getting Started with DJI UI Library**
**启动 DJI UI库**

2018-01-16v4.4.1 4.4.1Github

If you come across any mistakes or bugs in this tutorial, please let us know using a Github issue, a post on the DJI forum. Please feel free to send us Github pull request and help us fix any issues.
如果您在本教程中遇到任何问题和BUG, 请在 Github 上告诉我们。请随时发送 Github 请求, 并帮助我们解决任何问题。

In this tutorial, you will learn how to use DJI Android UI Library and DJI Android SDK to create a fully functioning mini-DJI Go app easily, with standard DJI Go UIs and functionalities. By the end of this tutorial you will have an app that you can use to show the camera FPV view, check aircraft status, shoot photos, record videos and so on.
在本教程中, 您将学习如何使用 DJI Android UI Library 和 DJI Android SDK 来创建一个功能完善的迷你 DJI Go APP,并具有标准的 DJI Go UIs 和功能。在本教程的最后, 你将会有一个APP, 你可以用它来显示摄像头的 FPV 视图, 检查无人机状态, 拍照, 录像等等。

You can download the tutorial's final sample project from this Github Page.
您可以从这个 Github 页面下载教程的最终示例项目。

We use Mavic Pro and Nexus 5 as an example to make this demo. For more details of customizing the layouts for iPhone devices, please check the tutorial's Github Sample Project. Let's get started!
我们使用 Mavic Pro 和 Nexus 5作为示例来做这个演示。 如果想了解更多关于 iPhone 设备的详细信息, 请查看教程的 Github 示例项目。 我们开始吧！

**Introduction**
**引言**

DJI UI Library is a visual library consisting of UI Elements. It helps you simplify the creation of DJI Mobile SDK based apps in Android. With similar design to DJI Go,UI Elements allow you to create consistent UX between your apps and DJI apps.
DJI UI SDK是一个由UI元素组成的可视化SDK。它可以帮助您简化在Android中创建基于DJI Mobile SDK的APP。通过与DJI Go类似的设计，UI Elements允许您的APP和DJI应用程序之间创建一致的用户体验。

Additionally, with the ease of use, UILibrary let you focus more on business and application logic.
另外, 由于使用方便, UI Library 让您更加关注业务和APP逻辑。

As DJI UI Library is built on top of DJI Mobile SDK and VideoPreviewer, you need to use it with them together in your application development.
由于 DJI UI库是在 DJI Mobile SDK 和 VideoPreviewer 的基础上建立的, 你需要在应用开发中一起使用它。

For an in depth learning on DJI UI Library, please go to the UI Library Introduction.
有关 DJI UI 库的深入学习, 请访问用户UI库介绍。

**Application Activation and Aircraft Binding in China**
**中国APP激活与无人机绑定**

For DJI SDK mobile application used in China, it's required to activate the application and bind the aircraft to the user's DJI account.
对于中国使用的 DJI SDK APP, 需要激活APP并将无人机绑定到用户的 DJI 帐户。

If an application is not activated, the aircraft not bound (if required), or a legacy version of the SDK (< 4.1) is being used, all camera live streams will be disabled, and flight will be limited to a zone of 100m diameter and 30m height to ensure the aircraft stays within line of sight.
如果一个APP没有被激活, 无人机不受管制(如果需要) , 或 SDK (4.1)的历史版本, 所有摄像头实时流都将被禁用, 飞行范围将限制在100米直径和30米高度范围内, 以确保无人机保持在视线范围内。

To learn how to implement this feature, please check this tutorial Application Activation and Aircraft Binding.
要学习如何实现这一功能, 请检查本教程APP激活和无人机绑定。

**Importing DJI UI Library**
**导入 DJI UI库**

Now, open Android Studio and select File -> New -> New Project to create a new project, named "UILibraryDemo". Enter the company domain and package name (Here we use "com.dji.uilibrarydemo") you want and press Next. Set the minimum SDK version as API 19: Android 4.4 (KitKat) for "Phone and Tablet" and press Next. Then select "Empty Activity" and press Next. Lastly, leave the Activity Name as "MainActivity", and the Layout Name as "activity_main", press "Finish" to create the project.
现在, 打开Android Studio, 选择File-new-New Project创建一个新项目, 命名为"UILibraryDemo"。 输入公司域名和包名(这里我们使用"com.dji.uilibrarydemo")并按下一步。 将MINI SDK 版本设置为 API 19: Android 4.4(KitKat)的"手机和平板电脑", 然后按下一步。 然后选择"Empty Activity"并按下一步。 最后, 将Activity name设置为"MainActivity", 并将"layout name"设置为"activity_main", 按"Finish"来创建项目。

**Configure Gradle Script**
**配置 Gradle 脚本**
Double click on the "build.gradle(Module: app)" in the project navigator to open it and add the following code:
在项目导航中双击"build.gradle (moudle: APP)"来打开它并添加以下代码:
~~~
apply plugin: 'com.android.application'
android {
    ...
    defaultConfig {
        ...
    }
    ...
    packagingOptions{
        doNotStrip "*/*/libdjivideo.so"
        doNotStrip "*/*/libSDKRelativeJNI.so"
        doNotStrip "*/*/libFlyForbid.so"
        doNotStrip "*/*/libduml_vision_bokeh.so"
        doNotStrip "*/*/libyuv2.so"
        doNotStrip "*/*/libGroudStation.so"
        doNotStrip "*/*/libFRCorkscrew.so"
        doNotStrip "*/*/libUpgradeVerify.so"
        doNotStrip "*/*/libFR.so"
    }
}
dependencies {
   ...
    compile ('com.dji:dji-uilibrary:4.4.1')
    provided ('com.dji:dji-sdk-provided:4.4.1')
}
~~~
In the code above, we implement the following features:
在上面的代码中, 我们实现了以下特性:

  1.Add the packagingOptions to prevent any unexpected crash of the application.
  1.添加packagingOptions 以防止APP出现意外崩溃
  
  2.Add the compile and provided dependencies to import the latest DJI Android UILibrary and SDK Maven dependency.
  2.添加compile 和 provided 依赖以导入最新的 DJI Android UILibrary 和 SDK Maven 依赖项

Once you finished the steps above, select Tools -> Android -> Sync Project with Gradle Files and wait for Gradle project sync to finish.
一旦完成上面的步骤, 选择 Tools-Android-Sync Project with Gradle Files, 然后等待 Gradle 项目同步完成。

**Double Check Maven Dependency**
**再次检查 Maven 依赖项**

Select File->Project Structure in the Android Studio menu to open the "Project Structure" window. Then select the "app" module and click the Dependencies tab. You should see the latest DJI Android UILibrary compile and sdk provided dependencies are already imported.
在 Android Studio 菜单中选择File-Project Structure打开"Project Structure"窗口。 然后选择"APP"模块并单击"依赖项"选项卡。 您应该看到最新的 DJI Android UILibrary 编译和 sdk 提供的依赖已经导入。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/libraryDependency-b2a9c974df.png)

**Building the Default Layout using UI Library**
**使用 UI 库构建默认布局**

Now, let's continue to open the "activity_main.xml" file, and replace the code with the following:
现在, 让我们继续打开"活动 main.xml"文件, 并重写:
~~~
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/background_blue"
    android:orientation="horizontal"
    tools:context=".MainActivity">
    <!--1-->
    <!-- Widget to see first person view (FPV) -->
    <dji.ui.widget.FPVWidget
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    <dji.ui.widget.FPVOverlayWidget
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    <!--2-->
    <!-- Widgets in top status bar -->
    <LinearLayout
        android:id="@+id/signal"
        android:layout_width="match_parent"
        android:layout_height="25dp"
        android:background="@color/dark_gray"
        android:orientation="horizontal">
        <dji.ui.widget.PreFlightStatusWidget
            android:id="@+id/status"
            android:layout_width="238dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.FlightModeWidget
            android:layout_width="103dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.GPSSignalWidget
            android:layout_width="44dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.VisionWidget
            android:layout_width="22dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.RemoteControlSignalWidget
            android:layout_width="38dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.VideoSignalWidget
            android:layout_width="38dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.WiFiSignalWidget
            android:layout_width="22dp"
            android:layout_height="20dp"/>
        <dji.ui.widget.BatteryWidget
            android:layout_width="56dp"
            android:layout_height="22dp"/>
        <dji.ui.widget.ConnectionWidget
            android:layout_marginTop="5dp"
            android:layout_width="22dp"
            android:layout_height="22dp"/>
    </LinearLayout>
    <!--3-->
    <LinearLayout
        android:id="@+id/camera"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/signal"
        android:layout_centerHorizontal="true"
        android:layout_margin="12dp"
        android:background="@color/dark_gray"
        android:orientation="horizontal">
        <dji.ui.widget.AutoExposureLockWidget
            android:layout_width="25dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.FocusExposureSwitchWidget
            android:layout_width="25dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.FocusModeWidget
            android:layout_width="25dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.config.CameraConfigISOWidget
            android:layout_width="50dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.config.CameraConfigShutterWidget
            android:layout_width="50dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.config.CameraConfigApertureWidget
            android:layout_width="50dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.config.CameraConfigEVWidget
            android:layout_width="50dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.config.CameraConfigWBWidget
            android:layout_width="50dp"
            android:layout_height="25dp"/>
        <dji.ui.widget.CameraConfigStorageWidget
            android:layout_width="108dp"
            android:layout_height="25dp"/>
    <!--4-->
    </LinearLayout>
    <dji.ui.widget.RemainingFlightTimeWidget
        android:layout_alignParentTop="true"
        android:layout_marginTop="18dp"
        android:layout_width="match_parent"
        android:background="@color/transparent"
        android:layout_height="20dp"/>
    <!--5-->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:padding="12dp">
        <dji.ui.widget.dashboard.DashboardWidget
            android:id="@+id/Compass"
            android:layout_width="405dp"
            android:layout_height="91dp"
            android:layout_marginRight="12dp"/>
    </LinearLayout>
    <!--6-->
    <!--Take off and return home buttons on left -->
    <LinearLayout
        android:layout_width="40dp"
        android:layout_height="wrap_content"
        android:layout_centerVertical="true"
        android:layout_marginStart="12dp"
        android:orientation="vertical">
        <dji.ui.widget.TakeOffWidget
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:layout_marginBottom="12dp"/>
        <dji.ui.widget.ReturnHomeWidget
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:layout_marginTop="12dp"/>
    </LinearLayout>
    <!--7-->
    <dji.ui.widget.controls.CameraControlsWidget
        android:id="@+id/CameraCapturePanel"
        android:layout_alignParentRight="true"
        android:layout_below="@id/camera"
        android:layout_width="50dp"
        android:layout_height="213dp"/>
    <!--8-->
    <dji.ui.panel.CameraSettingExposurePanel
        android:id="@+id/CameraExposureMode"
        android:layout_width="180dp"
        android:layout_below="@id/camera"
        android:layout_toLeftOf="@+id/CameraCapturePanel"
        android:background="@color/transparent"
        android:gravity="center"
        android:layout_height="263dp"
        android:visibility="invisible"/>
    <!--9-->
    <dji.ui.panel.CameraSettingAdvancedPanel
        android:id="@+id/CameraAdvancedSetting"
        android:layout_width="180dp"
        android:layout_height="263dp"
        android:layout_below="@id/camera"
        android:layout_toLeftOf="@+id/CameraCapturePanel"
        android:background="@color/transparent"
        android:gravity="center"
        android:visibility="invisible"/>
    <!--10-->
    <!-- Pre-flight checklist panel -->
    <dji.ui.panel.PreFlightCheckListPanel
        android:id="@+id/PreflightCheckView"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/signal"
        android:visibility="gone"/>
</RelativeLayout>
~~~
In the xml file above, we implement the following UIs:
在上面的 xml 文件中, 我们实现了以下 UIs:

  1.Firstly, we add the dji.ui.widget.FPVWidget and dji.ui.widget.FPVOverlayWidget elements to show the first person view (FPV).
  1.首先，我们添加dji.ui.widget.FPVWidget和dji.ui.widget.FPVOverlayWidget元素来显示第一人称视图（FPV）。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/fpvView-39271b502b.png)
  2.Next, on top of the screen, we create a LinearLayout to group the top status bar widgets, like PreFlightStatusWidget, FlightModeWidget, GPSSignalWidget, RemoteControlSignalWidget, etc.
  2.接下来，在屏幕的上方，我们创建一个LinearLayout中，以组合顶部的状态栏小工具，如PreFlightStatusWidget，FlightModeWidget，GPSSignalWidget，RemoteControlSignalWidget，等。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/topBar-ccb6351fbb.png)
  3.Moreover, we create another LinearLayout to group the camera configurations and config widgets below the status bar widgets, like AutoExposureLockWidget, FocusExposureSwitchWidget, CameraConfigISOWidget, CameraConfigStorageWidget, etc. Also we add the dji.ui.widget.RemainingFlightTimeWidget element to show the remaining flight time widget below the top status bar widgets too.
  3.另外，和顶部工具栏一样，我们创建另一个LinearLayout依次显示摄像头配置信息，例如AutoExposureLockWidget，FocusExposureSwitchWidget，CameraConfigISOWidget，CameraConfigStorageWidget，等。此外，我们添加dji.ui.widget.RemainingFlightTimeWidget显示顶部状态栏下方剩下的飞行时间窗口小部件元部件。

![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/cameraParams-24ed19290f.png)
  4.Below the top status bar, we add a RemainingFlightTimeWidget to show the remaining flight time.
  4.在顶部状态栏下方，我们添加一个RemainingFlightTimeWidget来显示剩余的飞行时间。

  5.At the bottom of the screen, we add another LinearLayout to group the DashboardWidget. It includes the circular CompassWidget, the DistanceHomeWidget, the HorizontalVelocityWidget, the DistanceRCWidget, the VerticalVelocityWidget and the AltitudeWidget as shown below:
  5.在屏幕的底部，我们添加另一个LinearLayout组合DashboardWidget。它包括CompassWidget，the DistanceHomeWidget，HorizontalVelocityWidgetthe DistanceRCWidget，the VerticalVelocityWidget和AltitudeWidget如下所示：
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/dashboard-25d1b9da5c.png)
  6.On the left side of the screen, we add a LinearLayout to group the TakeOffWidget and ReturnHomeWidget which will be shown as two buttons.
  6.在屏幕的左侧，我们添加了一个LinearLayout来将其分组，显示TakeOffWidget并将ReturnHomeWidget两个按钮。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/takeOff_backHome-314bb4a7ad.png)
  7.On the right side of the screen, we add the dji.ui.widget.controls.CameraControlsWidget element to create a CameraControlsWidget to show the camera control widget. Tapping the Menu button on top will toggle between show and hide CameraSettingAdvancedPanel. Tapping the switch button in the middle will toggle camera mode between shoot photo and record video. Tapping the bottom button will toggle between show and hide CameraSettingExposurePanel.
  7.在屏幕的右侧，我们添加dji.ui.widget.controls.CameraControlsWidget要创建的元素CameraControlsWidget以显示摄像头控件。点击顶部的菜单按钮将显示和隐藏CameraSettingAdvancedPanel。点击中间的滑动按钮将在拍照和视频之间切换。点击底部按钮将显示和隐藏CameraSettingExposurePanel。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/cameraControlWidget-59a45a760a.png)
  8.To add the CameraSettingExposurePanel, we add the dji.ui.panel.CameraSettingExposurePanel element and configure its attributes.
  8.为了添加CameraSettingExposurePanel，我们添加dji.ui.panel.CameraSettingExposurePanel元素并配置其属性。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/exposurePanel-135b70cc13.png)
  9.To add the CameraSettingAdvancedPanel, we add the dji.ui.panel.CameraSettingAdvancedPanel element and configure its attributes.
 9.为了添加CameraSettingAdvancedPanel，我们添加dji.ui.panel.CameraSettingAdvancedPanel元素并配置其属性。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/advancedPanel-f93803228c.png)
  10.Lastly, we add the dji.ui.panel.PreFlightCheckListPanel element to create the PreFlightCheckListPanel. When user press on the PreFlightStatusWidget, it will show up below the top status bar.
  10.最后，我们添加dji.ui.panel.PreFlightCheckListPanel元素来创建PreFlightCheckListPanel。当用户按下时PreFlightStatusWidget，它会显示在顶部状态栏下方。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/checklistPanel-e595671933.png)
Once you finished the steps above, open the "colors.xml" file and replace the content with the following:
一旦完成上面的步骤, 打开"colors.xml"文件, 并重写:
~~~
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="background_blue">#242d34</color>
    <color name="transparent">#00000000</color>
    <color name="dark_gray">#80000000</color>
</resources>
~~~
Moreover, let's open the "styles.xml" file and replace the content with the following:
此外, 让我们打开"styles.xml"文件,并重写:
~~~
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="@style/Base.Theme.AppCompat.Light.NoActionBar">
    </style>
</resources>
~~~
With the help of DJI UI Library, it's simple and straightforward to implement the standard DJI Go UIs and functionalities in your own application.
在 DJI UI 库的帮助下, 在您自己的APP中实现标准 DJI Go UIs 和功能是非常简单和直接的。

**Application Registration**
**申请注册**
Now let's register our application with the App Key you apply from DJI Developer Website. If you are not familiar with the App Key, please check the Get Started.
使用你申请的APP密钥注册APP。如果您不知道APP密钥, 请检查 Get Started。

**Implementing MApplication and DemoApplication**
**实现 MApplication和DemoApplication **

Right click on the 'com.dji.uilibrarydemo' module in the project navigator and select "New -> Java Class" to create a new file, enter "MApplication" as the Name. Then replace the code with the following:
在项目导航中右击"com.dji.uilibrarydemo"模块, 然后选择"New-Java 类"创建一个新文件, 输入"MApplication"作为名称。 然后重写:
~~~
package com.dji.uilibrarydemo;
import android.app.Application;
import android.content.Context;
import com.secneo.sdk.Helper;
public class MApplication extends Application {
    private DemoApplication demoApplication;
    @Override
    protected void attachBaseContext(Context paramContext) {
        super.attachBaseContext(paramContext);
        Helper.install(MApplication.this);
        if (demoApplication == null) {
            demoApplication = new DemoApplication();
            demoApplication.setContext(this);
        }
    }
    @Override
    public void onCreate() {
        super.onCreate();
        demoApplication.onCreate();
    }
}
~~~
Here, we override the attachBaseContext() method to add the Helper.install(MApplication.this); line of code. Also, override the onCreate() method to invoke the same onCreate() method of DemoApplication class.
在这里, 我们重写 attachBasecontext 方法来添加 Helper.install (MApplication.this)。 此外, 重写 onCreate 方法来调用 DemoApplication 类的同一个onCreate方法。

Note: Since some of SDK classes now need to be loaded before using, the loading process is done by Helper.install(). Developer needs to invoke this method before using any SDK functionality. Failing to do so will result in unexpected crashes.
注意: 由于SDK 类现在需要在使用之前加载, 所以加载过程由 Helper.install ()来完成。 开发人员需要在使用任何 SDK 功能之前调用此方法。 如果不这样做, 将会导致意想不到的崩溃。

Once we finished the steps above, let's continue to create the DemoApplication class, and replace the code with the same file in this tutorial's sample project, here we explain the important part of it:
一旦我们完成上面的步骤, 让我们继续创建 DemoApplication 类, 并在本教程的示例项目中重写, 这里我们将解释其中的重要部分:
~~~
@Override
    public void onCreate() {
        super.onCreate();
        mHandler = new Handler(Looper.getMainLooper());
        //Check the permissions before registering the application for android system 6.0 above.
        int permissionCheck = ContextCompat.checkSelfPermission(getApplicationContext(), android.Manifest.permission.WRITE_EXTERNAL_STORAGE);
        int permissionCheck2 = ContextCompat.checkSelfPermission(getApplicationContext(), android.Manifest.permission.READ_PHONE_STATE);
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.M || (permissionCheck == 0 && permissionCheck2 == 0)) {
            //This is used to start SDK services and initiate SDK.
            DJISDKManager.getInstance().registerApp(getApplicationContext(), mDJISDKManagerCallback);
        } else {
            Toast.makeText(getApplicationContext(), "Please check if the permission is granted.", Toast.LENGTH_LONG).show();
        }
        /**
         * When starting SDK services, an instance of interface DJISDKManager.DJISDKManagerCallback will be used to listen to
         * the SDK Registration result and the product changing.
         */
        mDJISDKManagerCallback = new DJISDKManager.SDKManagerCallback() {
            //Listens to the SDK registration result
            @Override
            public void onRegister(DJIError error) {
                if(error == DJISDKError.REGISTRATION_SUCCESS) {
                    DJISDKManager.getInstance().startConnectionToProduct();
                    Handler handler = new Handler(Looper.getMainLooper());
                    handler.post(new Runnable() {
                        @Override
                        public void run() {
                            Toast.makeText(getApplicationContext(), "Register Success", Toast.LENGTH_LONG).show();
                        }
                    });
                    loginAccount();
                } else {
                    Handler handler = new Handler(Looper.getMainLooper());
                    handler.post(new Runnable() {
                        @Override
                        public void run() {
                            Toast.makeText(getApplicationContext(), "Register Failed, check network is available", Toast.LENGTH_LONG).show();
                        }
                    });
                }
                Log.e("TAG", error.toString());
            }
            //Listens to the connected product changing, including two parts, component changing or product connection changing.
            @Override
            public void onProductChange(BaseProduct oldProduct, BaseProduct newProduct) {
                mProduct = newProduct;
                if(mProduct != null) {
                    mProduct.setBaseProductListener(mDJIBaseProductListener);
                }
                notifyStatusChange();
            }
        };
        mDJIBaseProductListener = new BaseProduct.BaseProductListener() {
            @Override
            public void onComponentChange(BaseProduct.ComponentKey key, BaseComponent oldComponent, BaseComponent newComponent) {
                if(newComponent != null) {
                    newComponent.setComponentListener(mDJIComponentListener);
                }
                notifyStatusChange();
            }
            @Override
            public void onConnectivityChange(boolean isConnected) {
                notifyStatusChange();
            }
        };
        mDJIComponentListener = new BaseComponent.ComponentListener() {
            @Override
            public void onConnectivityChange(boolean isConnected) {
                notifyStatusChange();
            }
        };
    }
~~~
Here, we implement several features:
在这里, 我们实现了几个特性:

  1.We override the onCreate() method to check the permissions and invoke the registerApp() method of DJISDKManager to register the application first.
我们重写 onCreate ()方法来检查权限并调用 DJISDKManager 的 registerApp 方法来注册APP。

  2.Initialize the SDKManagerCallback variable and implement its two interface methods. You can use the onRegister() method to check the Application registration status and show text message to inform users. Using the onProductChange() method, we can check the product connection status and invoke the notifyStatusChange() method to notify status changes.
初始化 SDKManagerCallback 变量并实现其两个接口方法。 您可以使用 onRegister ()方法来检查APP注册状态, 并提醒用户。使用 onProductChange ()方法, 我们可以检查无人机连接状态, 并调用 notifingstatuschange ()方法来通知状态更改。

  3.Initialize the BaseProductListener and ComponentListener variables and implement the interface methods of them. You can use the onComponentChange() method to check the product component change status and invoke the notifyStatusChange() method to notify status changes. Also, you can use the onConnectivityChange() method to notify the product and component connectivity changes.
初始化BaseProductListener and ComponentListener变量, 并实现它们的接口方法。 您可以使用 onComponentChange 方法来检查无人机组件的更改状态, 并调用 notifingstatuschange ()方法来通知状态更改。 此外, 您可以使用 onConnectivityChange 方法来通知无人机和组件的连接变化。

Please initialize the DJI Android SDK class variables inside the onCreate() method of DemoApplication class after the MApplication class is created, which finished loading the SDK classes by invoking the Helper.install().
请在创建 MApplication 类之后的 onCreate ()方法中初始化 DJI Android SDK 类变量, 该方法通过调用 Helper.install ()来完成 SDK 类的加载。

For more details, please check this tutorial's Github Sample project.
更多细节, 请查看本教程的 Github 示例项目。

**Modifying AndroidManifest file**
**修改 AndroidManifest 文件**

Once you finished the steps above, let's open the "AndroidManifest.xml" file and add the following elements on top of the application element:
一旦完成上面的步骤, 让我们打开"AndroidManifest.xml"文件, 添加以下元素:
~~~
<!-- DJI SDK need permission -->
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
<uses-feature
    android:name="android.hardware.usb.host"
    android:required="false" />
<uses-feature
    android:name="android.hardware.usb.accessory"
    android:required="true" />
~~~
Here, we request permissions that the application must be granted in order for it to register DJI SDK correctly. Also, we declare the camera and USB hardware which are used by the application.
在这里, 我们要求APP必须被授予权限才能地注册 DJI SDK。 同时, 我们声明APP使用摄像头和 USB 硬件。

Moreover, add the android:name=".MApplication" at the beginning of the application element:
此外, 在application的开头添加android:name=".MApplication"：
~~~
<application
    android:name=".MApplication"
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:supportsRtl="true"
    android:theme="@style/AppTheme">
~~~
Furthermore, let's add the following elements as childs of element on top of the "MainActivity" activity element as shown below:
另外, 添加以下内容到"MainActivity"
~~~
<!-- DJI SDK -->
<uses-library android:name="com.android.future.usb.accessory" />
<meta-data
    android:name="com.dji.sdk.API_KEY"
    android:value="Please enter your App Key here." />
<activity
    android:name="dji.sdk.sdkmanager.DJIAoaControllerActivity"
    android:theme="@android:style/Theme.Translucent">
    <intent-filter>
        <action android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED" />
    </intent-filter>
    <meta-data
        android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED"
        android:resource="@xml/accessory_filter" />
</activity>
<service android:name="dji.sdk.sdkmanager.DJIGlobalService"></service>
<!-- DJI SDK -->
~~~
In the code above, you should substitute your App Key of the application for "Please enter your App Key here." in the value attribute under the android:name="com.dji.sdk.API_KEY" attribute. For the "accessory_filter.xml" file, you can get it from this tutorial's Github Sample project.
在上面的代码中, 您应该用APP KEY替换"Please enter your App Key here" 。 "accessfil.xml"文件, 您可以从这个教程的 Github 示例项目得到它。

Lastly, update the "MainActivity" activity elements as shown below:
最后, 更新"MainActivity", 如下所示:
~~~
<activity android:name=".MainActivity"
    android:screenOrientation="landscape">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
~~~
In the code above, we add the attributes of "android:screenOrientation" to set "MainActivity" as landscape and add an intent filter for it.
在上面的代码中, 我们添加了"android: screenOrientation"的属性来将"MainActivity"设置为landscape, 并为其添加一个意图过滤器。

**Working on the MainActivity**
**MainActivity**

Finally, let's open the "MainActivity.java" file, replace the code with the following:
最后, 让我们打开"MainActivity.java"文件, 并重写:
~~~
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // When the compile and target version is higher than 22, please request the
        // following permissions at runtime to ensure the
        // SDK work well.
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
        setContentView(R.layout.activity_main);
    }
}
~~~
In the onCreate() method, we request several permissions at runtime to ensure the SDK works well when the compile and target SDK version is higher than 22(Like Android Marshmallow 6.0 device and API 23).
在 onCreate ()方法中, 我们在运行时请求多个权限, 以确保 SDK 在编译和目标 SDK 版本高于22(如 Android M 6.0设备和 API 23)的设备上运行。

Now, let's build and run the project and install it to your Android device. If everything goes well, you should see the "Register Success" textView like the following screenshot when you register the app successfully.
现在, 让我们构建并运行这个项目, 并把它安装到你的 Android 手机上。 如果一切顺利, 当你成功注册APP时, 你应该会看到"注册成功"文本, 就像下面的截图一样。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/registerSuccess-94535c6afe.png)

**Connecting to the Aircraft and Run the Project**
**连接无人机和运行项目**

Now, please check this Connect Mobile Device and Run Application guide to run the application and try the mini-DJI Go features of UILibrary based on what we've finished of the application so far!
现在, 请检查这个连接手机和运行APP指南, 以运行APP并尝试 UILibrary 的mini dji Go 功能！

If you can see the live video feed and test the features like this, congratulations! Using the DJI UI Library is that easy.
如果你可以看到实时视频, 并能测试这样的功能, 祝贺你！ 使用 DJI UI库就是这么简单。
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/UILibraryDemo/connectToAircraft-a48f58d7ec.gif)

**Summary**
**摘要**
In this tutorial, you have learned how to use the DJI Android UI Library and DJI Android SDK to create a fully functioning mini-DJI Go app easily, with standard DJI Go UIs and functionalities. Hope you enjoy it!
在本教程中, 您已经学习了如何使用 DJI Android UI 库和 DJI Android SDK 来创建一个功能完善的mini DJI Go APP, 标准的 DJI Go UIs 和功能。 希望你喜欢！


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)