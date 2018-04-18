**Integrate SDK into Application**
**将 SDK 集成到APP中**

2017-12-29

The examples below import the DJI SDK into a new iOS and Android project. The same steps can be used for integration into an existing application.
下面的示例将 DJI SDK 导入一个新的 iOS 和 Android 项目。相同的步骤可以用于集成到现有的APP中。

**Android Studio Project Integration**
**Android Studio项目集成**

Screenshots in this section are generated using Android Studio 3.0.
本部分的截图是使用 Android Studio 3.0生成的。

**Create a New Application**
**新建APP**

A new application can be used to show how to integrate the DJI SDK into an Android Studio project.
可以使用新建APP来演示如何将DJI SDK集成到Android Studio项目中。

Open Android Studio and at the initial screen select Start a new Android Studio project 
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidNewProjectSplashScreen-64f03e4638.png)
In the New Project screen: 
Set the Application name to "ImportSDKDemo".
Set the Company Domain and Package name to "com.dji.ImportSDKDemo".
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidConfigureNewProject-016f6bc43c.png)
Note: Package name is the identifying string required to generate an App Key. The activity java, manifest xml and Gradle script code below assumes Package name is "com.dji.ImportSDKDemo"
注意:包名是生成APP密钥所需的识别字符串。The activity java, manifest xml and Gradle 脚本代码假定包名是"com.dji.ImportSDKDemo"

In the Target Android Devices screen:

Select Phone and Tablet form factor.
Choose API 19: Android 4.4 (KitKat).
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidSelectFormFactor-f85e43ef2f.png)
In the Add an Activity to Mobile screen choose Empty Activity.
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidAddAnActivityToMobile-6f25935987.png)

Set Activity Name: to "MainActivity".
Ensure Generate Layout File is checked.
Set Layout Name: to "activity_main".
Click Finish when done.
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidCustomizeTheActivity-44800303b4.png)
**Configure Gradle Script**
**配置 Gradle 脚本**

In Gradle Scripts double click on build.gradle (Module: app) 
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidConfigureGradleInitial-920e21018e.png)
Update the content with the following: 
更新内容如下:
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
    compile ('com.dji:dji-sdk:4.4.1')
    provided ('com.dji:dji-sdk-provided:4.4.1')
}
~~~

The main changes should be:
主要的变化应该是:

Add the packagingOptions to prevent any unexpected crash of the application. 
添加packagingOptions以防止应用程序意外崩溃。

Add the compile and 还有provided dependencies to import the latest DJI Android SDK Maven dependency. 添加compile和provided依赖项以导入最新的DJI Android SDK Maven依赖项。
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidConfigureGradleAfterChange-a85ab462c2.png)

Select Tools -> Android -> Sync Project with Gradle Files and wait for Gradle project sync to finish. 

Double Check Maven Dependency
再次检查 Maven 依赖项

Select File->Project Structure in the Android Studio menu to open the "Project Structure" window. Then select the "app" module and click the Dependencies tab. You should see the latest DJI SDK compile and provided denpendencies are already imported. 
![](https://devcn.djicdn.com/images/application-development-workflow/libraryDependency-9f6d54268f.png)

**Implement App Registration and SDK Callbacks**
**实现APP注册和SDK回调**

Right click on the com.dji.importSDKDemo, and select New->Java Class to create a new java class and name it as "MApplication".
右击dji.importSDKDem，然后选择 New->Java创建一个MApplication类
![](https://devcn.djicdn.com/images/application-development-workflow/createJavaClass-0f4351526a.png)
Open the MApplication.java file and replace the content with the following:
打开 MApplication.java 文件, 用以下内容替换:
~~~
package com.dji.importSDKDemo;
import android.app.Application;
import android.content.Context;
import com.secneo.sdk.Helper;
public class MApplication extends Application {
    @Override
    protected void attachBaseContext(Context paramContext) {
        super.attachBaseContext(paramContext);
        Helper.install(MApplication.this);
    }
}
~~~

Here we override the attachBaseContext() method to add the Helper.install(MApplication.this); line of code.
这里我们重写attachBaseContext()添加Helper.install(MApplication.this);代码行的方法。

Note: Since some of SDK classes now need to be loaded before using, the loading process is done by Helper.install(). Developer needs to invoke this method before using any SDK functionality. Failing to do so will result in unexpected crashes.
注意: 由于一些SDK类现在需要在使用之前加载,所以加载过程由 Helper.install ()来完成。开发人员需要在使用任何SDK 功能之前调用此方法。如果不这样做, 将会导致崩溃。
![](https://devcn.djicdn.com/images/application-development-workflow/mApplication-2f1876063d.png)
Double click on MainActivity.java in the app module.
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidImplementationMainActivity-899fa331b2.png)
The MainActivity class needs to register the application to get authorization to use the DJI Mobile SDK. It also needs to implement callback methods expected by the SDK.
Mainactivity 类需要注册APP以获得使用DJI Mobile SDK的授权。它还需要实现SDK所期望的回调方法。

The MainActivity class will first be modified to include several class variables including mProduct which is the object that represents the DJI product connected to the mobile device.
Mainactivity类将首先添加几个类变量,包括mProduct,它是表示连接到手机的DJI 无人机的对象。

Additionally the onCreate method will be modified to invoke the checkAndRequestPermissions method to check and request runtime permissions. Also, the checkAndRequestPermissions method will help to invoke the startSDKRegistration() method to register the application. Moreover, the override onRequestPermissionsResult method will help to check if the application has enough permission, if so, invoke the startSDKRegistration() method to register the application.
此外, onCreate 方法将被修改以调用checkAndRequestPermissions方法来检查和请求运行时权限。此外, checkAndRequestPermissions方法将有助于调用startSDKRegistration 方法来注册APP。此外,重写 requestpermissionsresult 方法将检查APP是否有足够的权限,如果有,则调用startSDKRegistration ()方法来注册APP。

Now, replace the MainActivity class with:
现在，将MainActivity类替换为：
~~~
public class MainActivity extends AppCompatActivity {
    private static final String TAG = MainActivity.class.getName();
    public static final String FLAG_CONNECTION_CHANGE = "dji_sdk_connection_change";
    private static BaseProduct mProduct;
    private Handler mHandler;
    private static final String[] REQUIRED_PERMISSION_LIST = new String[]{
            Manifest.permission.VIBRATE,
            Manifest.permission.INTERNET,
            Manifest.permission.ACCESS_WIFI_STATE,
            Manifest.permission.WAKE_LOCK,
            Manifest.permission.ACCESS_COARSE_LOCATION,
            Manifest.permission.ACCESS_NETWORK_STATE,
            Manifest.permission.ACCESS_FINE_LOCATION,
            Manifest.permission.CHANGE_WIFI_STATE,
            Manifest.permission.WRITE_EXTERNAL_STORAGE,
            Manifest.permission.BLUETOOTH,
            Manifest.permission.BLUETOOTH_ADMIN,
            Manifest.permission.READ_EXTERNAL_STORAGE,
            Manifest.permission.READ_PHONE_STATE,
    };
    private List<String> missingPermission = new ArrayList<>();
    private AtomicBoolean isRegistrationInProgress = new AtomicBoolean(false);
    private static final int REQUEST_PERMISSION_CODE = 12345;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // When the compile and target version is higher than 22, please request the following permission at runtime to ensure the SDK works well.
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            checkAndRequestPermissions();
        }
        setContentView(R.layout.activity_main);
        //Initialize DJI SDK Manager
        mHandler = new Handler(Looper.getMainLooper());
    }
    /**
     * Checks if there is any missing permissions, and
     * requests runtime permission if needed.
     */
    private void checkAndRequestPermissions() {
        // Check for permissions
        for (String eachPermission : REQUIRED_PERMISSION_LIST) {
            if (ContextCompat.checkSelfPermission(this, eachPermission) != PackageManager.PERMISSION_GRANTED) {
                missingPermission.add(eachPermission);
            }
        }
        // Request for missing permissions
        if (missingPermission.isEmpty()) {
            startSDKRegistration();
        } else if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            showToast("Need to grant the permissions!");
            ActivityCompat.requestPermissions(this,
                    missingPermission.toArray(new String[missingPermission.size()]),
                    REQUEST_PERMISSION_CODE);
        }
    }
    /**
     * Result of runtime permission request
     */
    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        // Check for granted permission and remove from missing list
        if (requestCode == REQUEST_PERMISSION_CODE) {
            for (int i = grantResults.length - 1; i >= 0; i--) {
                if (grantResults[i] == PackageManager.PERMISSION_GRANTED) {
                    missingPermission.remove(permissions[i]);
                }
            }
        }
        // If there is enough permission, we will start the registration
        if (missingPermission.isEmpty()) {
            startSDKRegistration();
        } else {
            showToast("Missing permissions!!!");
        }
    }
}
~~~

The registerApp() method of DJISDKManager has a callback that needs to process two methods for processing the application registration result, and for when the product connected to the mobile device is changed.
Djisdkkmanager 的 registerApp ()方法有一个回调,需要处理两种APP注册结果的方法,以及当连接到手机的无人机发生更换时。

Continue to add the startSDKRegistration() method as shown below and implement the onRegister() and onProductChange methods of the SDKManagerCallback:
继续添加startSDKRegistration()如下所示的方法并实现以下方法onRegister()和onProductChange方法和SDKManagerCallback：
~~~
private void startSDKRegistration() {
    if (isRegistrationInProgress.compareAndSet(false, true)) {
        AsyncTask.execute(new Runnable() {
            @Override
            public void run() {
                showToast("registering, pls wait...");
                DJISDKManager.getInstance().registerApp(MainActivity.this.getApplicationContext(), new DJISDKManager.SDKManagerCallback() {
                    @Override
                    public void onRegister(DJIError djiError) {
                        if (djiError == DJISDKError.REGISTRATION_SUCCESS) {
                            showToast("Register Success");
                            DJISDKManager.getInstance().startConnectionToProduct();
                        } else {
                            showToast("Register sdk fails, please check the bundle id and network connection!");
                        }
                        Log.v(TAG, djiError.getDescription());
                    }
                    @Override
                    public void onProductChange(BaseProduct oldProduct, BaseProduct newProduct) {
                        mProduct = newProduct;
                        if(mProduct != null) {
                            mProduct.setBaseProductListener(mDJIBaseProductListener);
                        }
                        notifyStatusChange();
                    }
                });
            }
        });
    }
}
~~~

Finally methods for BaseProductListener, ComponentListener, notifyStatusChange, Runnable and showToast need to be implemented:
最后, BaseProductListener、 ComponentListener、 notifatin statuschange、 Runnable 和 showToast 的方法需要实现:
~~~
private BaseProduct.BaseProductListener mDJIBaseProductListener = new BaseProduct.BaseProductListener() {
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
private BaseComponent.ComponentListener mDJIComponentListener = new BaseComponent.ComponentListener() {
    @Override
    public void onConnectivityChange(boolean isConnected) {
        notifyStatusChange();
    }
};
private void notifyStatusChange() {
    mHandler.removeCallbacks(updateRunnable);
    mHandler.postDelayed(updateRunnable, 500);
}
private Runnable updateRunnable = new Runnable() {
    @Override
    public void run() {
        Intent intent = new Intent(FLAG_CONNECTION_CHANGE);
        sendBroadcast(intent);
    }
};
private void showToast(final String toastMsg) {
    Handler handler = new Handler(Looper.getMainLooper());
    handler.post(new Runnable() {
        @Override
        public void run() {
            Toast.makeText(getApplicationContext(), toastMsg, Toast.LENGTH_LONG).show();
        }
    });
}
~~~

The application must be granted permissions to in order for the DJI SDK to operate.
为了使 DJI SDK 运行, 必须授予APP权限。

Double click on AndroidManifest.xml in the app module. 
在APP模块中双击 AndroidManifest.xml。
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidManifest-7951a3b7c1.png)
After package=com.dji.ImportSDKDemo and before <application insert:
在package=com.dji.ImportSDKDemo和<application>之前插入:
~~~
<!-- Permissions and features -->
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
<!-- Permissions and features -->
~~~

Add the android:name=".MApplication" at the beginning of the application element:
在application元素开头添加android:name=".MApplication"
~~~
<application
    android:name=".MApplication"
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/AppTheme" >
~~~

Insert the following after <android:theme="@style/AppTheme"> and before <activity android:name=".MainActivity">:
在android:theme="@style/AppTheme">和<activity android:name=".MainActivity">之间插入以下代码
~~~
<!-- DJI SDK -->
<uses-library android:name="com.android.future.usb.accessory" />
<meta-data
    android:name="com.dji.sdk.API_KEY"
    android:value="Please enter your App Key here." />
<activity
    android:name="dji.sdk.sdkmanager.DJIAoaControllerActivity"
    android:theme="@android:style/Theme.Translucent" >
    <intent-filter>
        <action android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED" />
    </intent-filter>
    <meta-data
        android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED"
        android:resource="@xml/accessory_filter" />
</activity>
<service android:name="dji.sdk.sdkmanager.DJIGlobalService" >
</service>
<!-- DJI SDK -->
~~~

Insert the android:configChanges="orientation" and android:screenOrientation="portrait" in the activity element as shown below to prevent the activity restarts when the screen orientation changes and also set the activity's screen orientation as portrait mode:
如下所示，插入android:configChanges="orientation" 和"android:screenOrientation="portrait" 以防止屏幕方向改变时重新开始活动，并将活动屏幕的方向设置为纵向
~~~
<activity android:name=".MainActivity"
          android:configChanges="orientation"
          android:screenOrientation="portrait">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
~~~

Generate an App Key, and replace "Please enter your App Key here." with the App Key string.
生成一个APP密钥,使用APP KEY替换"Please enter your App Key here" 。

**Run Import SDK Demo**
**运行导入 SDK 演示**

The ImportSDKDemo project can now be run. You can download the sample code of this project from Github.
现在可以运行 ImportSDKDemo 项目。 您可以从 Github 下载此项目的示例代码。

As this application is only checking for registration and not interacting directly with a product, no product needs to be connected to the application for this to run. Therefore, the application can either be run on a mobile device (with or without a DJI product connected) or in the Android simulator. The application will need internet connectivity to perform registration successfully.
由于此APP只是检查注册和不与无人机直接交互,因此无需将任何无人机连接到APP就可以运行这个APP。因此,APP可以在手机上运行(连接或不连接 DJI 无人机)或者在Android模拟器上运行。该APP需要互联网连接才能成功地进行注册。

If the App Key was generated correctly and the Android simulator or mobile device has internet connectivity, then the following should be seen:
如果APP密钥生成正确, Android模拟器或手机具有互联网连接性, 那么应该看到以下内容:
![](https://devcn.djicdn.com/images/application-development-workflow/AndroidRunSuccess-dd10bb07d7.png)

**FFmpeg License**
**Ffmpeg 许可证**

The DJI Android SDK is dynamically linked with unmodified libraries of FFmpeg licensed under the LGPLv2.1. The source code of these FFmpeg libraries, the compilation instructions, and the LGPL v2.1 license are provided in Github.
Dji Android SDK 与 LGPLv2.1下授权的未修改的 FFmpeg 库动态链接。 这些 FFmpeg 库的源代码、编译命令和 LGPL v2.1许可在 Github 提供。


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)