**Application Activation and Aircraft Binding**
**APP激活和无人机绑定**

2018-01-15v4.4.1 4.4.1Github

Note: This tutorial only works for applications used in China. The same steps can be used for activating application and binding aircraft in an existing 注意：本教程仅适用于在中国使用的APP。在现有的应用程序中，可以使用相同的步骤激活APP和绑定飞机。

You can download the tutorial's final sample project from this Github Page.
您可以从这个 Github 页面下载教程的示例项目。

**Introduction**
**引言**

DJI aircraft firmware requires mobile applications that control DJI aircraft to be activated with the user's DJI account, if that application is being used in China. This will ensure operators use the correct set of geospatial information and flight functions for their aircrafts, as determined by their geographical location and user profile. A summary of the activation system is:
如果该APP在中国使用，则DJI飞机固件需要使用APP来控制DJI飞机，并使用DJI账户进行激活。这将确保DJI为其飞机使用修正后的地理空间信息和飞行功能，具体取决于其地理位置和用户信息。激活系统的总结来说：

Users in China are required to activate their application by logging into their DJI account at least once every three months within the application.
中国用户需要在APP中至少每三个月登录一次DJI账号来激活其APP。

Activation will be persistent in the application until the user logs out.
在用户注销之前, 激活将持续存在于APP中。

Internet connection will be required to log into a DJI account.
需要连网才能登录到 DJI 帐户。

Outside of China, the SDK will automatically activate the application without requiring the user to log in.
在中国之外, SDK 将自动激活APP而无需用户登录。

Additionally, users in China are required to bind their aircraft to their user account in DJI Go / DJI Go 4. This is required only once. If an application is not activated, the aircraft not bound (if required), or a legacy version of the SDK (< 4.1) is being used, all camera live streams will be disabled, and flight will be limited to a zone of 100m diameter and 30m height to ensure the aircraft stays within line of sight.
此外, 中国的用户被要求将他们的无人机绑定到 DJI Go / DJI Go 4的用户账户。这只需要一次。如果APP没有激活, 无人机不受管制(如果需要) , 或 SDK (4.1)的历史版本, 所有摄像头实时流都将被禁用, 飞行范围将限制在100米直径和30米高度范围内, 以确保无人机保持在视线范围内。

**Application Activation**
**激活APP**

Now, let's create a new project in Android Studio, open Android Studio and select File -> New -> New Project to create a new project, named 'ActivationDemo'. Enter the company domain and package name (Here we use "com.dji.activationDemo") you want and press Next. Set the minimum SDK version as API 18: Android 4.3 (Jelly Bean) for "Phone and Tablet" and press Next. Then select "Empty Activity" and press Next. Lastly, leave the Activity Name as "MainActivity", and the Layout Name as "activity_main", press "Finish" to create the project.
现在, 让我们在 Android Studio 中创建一个新项目, 打开Android Studio, 选择"File-New-New File"来创建一个名为"ActivationDemo"的新项目。 输入您想要的公司域名和包名(这里我们使用"com.dji.activationDemo")并按下一步。 将mini  SDK 版本设置为 API 18: Android 4.3(Jelly Bean) , 用于"Phone and Tablet", 然后按下一步。 然后选择"Empty Activity"并按下一步。最后, 设置Activity name 为"MainActivity", 并设置"layout name"为"activity_main", 按"Finish"来创建项目。

**Registering the Application**
**注册APP**

This demo is build based on the ImportSDKDemo Github Sample, you can check the Integrate SDK into Application tutorial to learn how to import the Android SDK Maven Dependency and register the application using DJI Mobile SDK.
这个演示是基于 ImportSDKDemo Github 示例, 您可以查看integrate SDK into Application 教程去 学习如何导入Android SDK Maven 依赖, 并使用 DJI Mobile SDK 注册APP。

**Implementing the UI of Application**
**实现APP UI界面**

**Working on the MApplication, DemoApplication and ConnectionActivity**
**重写MApplication、 DemoApplication 和 ConnectionActivity**

Please check the Creating an Camera Application tutorial and the sample project of this tutorial for the detailed implementations.
请检查创建相机APP教程和本教程的示例项目, 以便获取详细的实现细节。

**Working on the MainActivity Class**
**重写MainActivity 类**

The MainActivity.java file is created by Android Studio by default. Let's replace the code of it with the following:
默认情况下, Android Studio 会创建 MainActivity.java 文件。 让我们重写它:
~~~
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    private static final String TAG = MainActivity.class.getName();
    protected Button loginBtn;
    protected Button logoutBtn;
    protected TextView bindingStateTV;
    protected TextView appActivationStateTV;
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
        initUI();
    }
    @Override
    public void onResume() {
        Log.e(TAG, "onResume");
        super.onResume();
    }
    @Override
    public void onPause() {
        Log.e(TAG, "onPause");
        super.onPause();
    }
    @Override
    public void onStop() {
        Log.e(TAG, "onStop");
        super.onStop();
    }
    public void onReturn(View view){
        Log.e(TAG, "onReturn");
        this.finish();
    }
    @Override
    protected void onDestroy() {
        Log.e(TAG, "onDestroy");
        super.onDestroy();
    }
    private void initUI(){
        bindingStateTV = (TextView) findViewById(R.id.tv_binding_state_info);
        appActivationStateTV = (TextView) findViewById(R.id.tv_activation_state_info);
        loginBtn = (Button) findViewById(R.id.btn_login);
        logoutBtn = (Button) findViewById(R.id.btn_logout);
        loginBtn.setOnClickListener(this);
        logoutBtn.setOnClickListener(this);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_login:{
                break;
            }
            case R.id.btn_logout:{
                break;
            }
            default:
                break;
        }
    }
}
~~~
In the code shown above, we implement the following features:
在上面的代码中, 我们实现了以下特性:

1. Create the layout UI elements variables, including two TextureView bindingStateTV and appActivationStateTV, two Buttons loginBtn, logoutBtn.
1. 创建UI 元素变量, 包括两个 TextureView，bindingStateTV 和 appActivationStateTV, 两个按钮 loginBtn, logoutBtn。

2. Then invoke the initUI() method to initialize UI variables. And implement the setOnClickListener() method of Button for all the Buttons.
2. 然后调用 initUI ()方法来初始化 UI 变量。 并实现所有按钮的 setOnClickListener ()方法。

3. Override the onClick() method to implement the three Buttons' click actions.
3. 重写 onClick ()方法来实现三个按钮的单击操作。

**Working on the MainActivity Layout**
**重写 MainActivity 布局**

Open the activity_main.xml layout file and replace the code with the following:
打开活动 main.xml 布局文件, 并重写:
~~~
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <TextView
        android:id="@+id/binding_state_label"
        android:layout_width="wrap_content"
        android:layout_height="60dp"
        android:layout_below="@+id/textView"
        android:layout_centerHorizontal="true"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="50dp"
        android:gravity="center"
        android:text="Binding State:"
        android:textColor="@color/black"
        android:textSize="17sp"
        android:textStyle="bold" />
    <TextView
        android:id="@+id/tv_binding_state_info"
        android:layout_width="220dp"
        android:layout_height="60dp"
        android:layout_below="@+id/binding_state_label"
        android:layout_centerHorizontal="true"
        android:layout_gravity="center_horizontal"
        android:gravity="center"
        android:text="Unknown"
        android:textColor="@color/black"
        android:textSize="17sp" />
    <Button
        android:id="@+id/btn_login"
        style="@style/common_button"
        android:layout_alignParentBottom="true"
        android:layout_alignStart="@+id/tv_activation_state_info"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="79dp"
        android:text="Login" />
    <Button
        android:id="@+id/btn_logout"
        style="@style/common_button"
        android:layout_alignParentBottom="true"
        android:layout_alignEnd="@+id/tv_activation_state_info"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="79dp"
        android:text="Logout" />
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="30dp"
        android:text="Application Activation Demo"
        android:textSize="17sp"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true" />
    <TextView
        android:id="@+id/activation_state_label"
        android:layout_width="wrap_content"
        android:layout_height="60dp"
        android:layout_below="@+id/tv_binding_state_info"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="11dp"
        android:text="App Activation State:"
        android:textColor="@color/black"
        android:textSize="17sp"
        android:textStyle="bold" />
    <TextView
        android:id="@+id/tv_activation_state_info"
        android:layout_width="220dp"
        android:layout_height="60dp"
        android:layout_alignEnd="@+id/tv_binding_state_info"
        android:layout_below="@+id/activation_state_label"
        android:text="Unknown"
        android:textAlignment="center"
        android:textColor="@color/black"
        android:textSize="17sp" />
</RelativeLayout>
~~~

In the xml file, we implement the followings:
在 xml 文件中, 我们重写了:

We implement the RelativeLayout element, then declare two TextView elements: (id:tv_binding_state_info) and (id:tv_activation_state_info) to show the activation and binding state infos. For the other three TextView elements, we declare them as labels to show titles.
我们实现了RelativeLayout, 然后声明两个TextView : (id: tv_binding_state_info)和(id: tv_activation_state_info) , 以显示APP激活和无人机绑定状态信息。其他三个 TextView, 我们用它们显示标题。

Then, we create the "Login" button(id: btn_login) and "Logout" button(id: btn_logout) buttons.
然后, 我们创建"Login"按钮(id: btn Login)和"Logout"按钮(id: btn Logout)按钮。

For more detail configurations of the layout, please check the activity_main.xml file of the tutorial's Github sample project.
有关布局的详细配置, 请检查教程的 Github 示例项目的activity_main.xml 文件。

**Configuring the Resources**
**配置资源**

Once you finish the above steps, let's add some resources files to the res folder on the left navigator of Android Studio.
一旦你完成了上面的步骤, 让我们把一些资源文件添加到 Android Studio 左侧导航器的 res 文件夹中。

Copy the following image and xml files from the tutorial Github Sample project's drawable folder to your project, they are used for the button's UI:
将下面的图片和 xml 文件从教程 Github 项目的drawable文件夹复制到您的项目,它们是用于按钮的 UI:

![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/drawable_images-4c6d4f7610.png)

Next, open the "colors.xml" file and add the following code at the bottom to declare the black color:
接下来, 打开"colors.xml"文件, 在底部添加下面的代码来声明黑色:
~~~
<color name="colorBlack">#ff000000</color>
<color name="colorWhite">#FFFFFF</color>
~~~
Moreover, open the "strings.xml" file and replace the content with the followings:
此外, 打开"strings.xml"文件, 并重写:
~~~
<resources>
    <string name="app_name">ActivationDemo</string>
    <string name="title_activity_connection">ConnectionActivity</string>
    <string name="action_settings">Settings</string>
    <string name="disconnected">Disconnected</string>
    <string name="product_information">Product Information</string>
    <string name="connection_loose">Status: No Product Connected</string>
    <string name="sdk_version">DJI SDK Version: 4.1.1</string>
</resources>
~~~
Here, we define string elements for showing text in the ConnectionActivity layout.
在这里, 我们定义了在 ConnectionActivity 布局中文字的格式。

Furthermore, open the "styles.xml" file and replace the content with the followings:
此外, 打开"styles.xml"文件, 重写:
~~~
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="@style/Theme.AppCompat.Light.NoActionBar">
    </style>
    <!-- Common button style -->
    <style name="common_button">
        <item name="android:layout_width">100dp</item>
        <item name="android:layout_height">45dp</item>
        <item name="android:layout_marginTop">10dp</item>
        <item name="android:background">@drawable/round_btn</item>
        <item name="android:paddingLeft">5dp</item>
        <item name="android:paddingRight">5dp</item>
        <item name="android:textAllCaps">false</item>
        <item name="android:textColor">@android:color/white</item>
        <item name="android:textSize">14sp</item>
    </style>
</resources>
~~~
In the code above, we change the AppTheme style and define a common button style.
在上面的代码中, 我们改变了 AppTheme 风格, 并定义了常见的按钮样式。

Now, if you check the activity_main.xml file, you can see the preview screenshot of the MainActivity as shown below:
现在, 如果你检查 main.xml 文件, 你可以看到 MainActivity 的预览截图如下:
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/previewScreenshot-a7c0f9fe80.png)

**Working on the AppActivationManager**
**重写 AppActivationManager**

In order to fetch the updated application activation state and aircraft binding state, we can use the AppActivationManager to add listeners to fetch this infos.
为了获取更新的APP激活状态和无人机绑定状态, 我们可以使用 AppActivationManager 添加侦听器来获取此信息。

Now, let's open the "MainActivity.java" file and create a AppActivationManager variable appActivationManager, a AppActivationStateListener listener activationStateListener and a AircraftBindingStateListener listener bindingStateListener:
现在，让我们打开“MainActivity.java”文件并创建一个AppActivationManager变量appActivationManager，一个AppActivationStateListener监听器activationStateListener和一个AircraftBindingStateListener监听器bindingStateListener：
~~~
private AppActivationManager appActivationManager;
private AppActivationState.AppActivationStateListener activationStateListener;
private AircraftBindingState.AircraftBindingStateListener bindingStateListener;
~~~
Next, create an initData() method as shown below and invoke it at the bottom of onCreate() method:
接下来, 创建一个 initData ()方法, 如下所示并在 onCreate ()方法的最后调用它:
~~~
private void initData(){
    setUpListener();
    appActivationManager = DJISDKManager.getInstance().getAppActivationManager();
    if (appActivationManager != null) {
        appActivationManager.addAppActivationStateListener(activationStateListener);
        appActivationManager.addAircraftBindingStateListener(bindingStateListener);
        MainActivity.this.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                appActivationStateTV.setText("" + appActivationManager.getAppActivationState());
                bindingStateTV.setText("" + appActivationManager.getAircraftBindingState());
            }
        });
    }
}
~~~
In the code above, we implement the following features:
在上面的代码中, 我们实现了以下特性:

  1.We initialize the appActivationManager variable by invoking the getAppActivationManager method of DJISDKManager.
  1.我们通过调用 DJISDKManager 的 getAppActivationManager 方法来初始化 appActivationManager 变量。

  2.Then we check if the appActivationManager variable exist and invoke the addAppActivationStateListener() method and pass the activationStateListener listener as param to add listener for the app activation state update. Similarly, we invoke the addAircraftBindingStateListener() method and pass the bindingStateListener listener as param to add listener for the aircraft binding state update.
  2.然后我们检查 appActivationManager 变量是否存在, 并调用 addAppActivationStateListener ()方法, 并通过 activationStateListener 作为参数传递给应用激活状态更新添加侦听器。 同样, 我们调用 addaircrafts bindingStateListener ()方法, 并将 bindingStateListener 侦听器作为参数传递给监听器, 以为无人机绑定状态更新添加侦听器。

  3.Lastly, we invoke the getAppActivationState() method of appActivationManager to get the current app activation state and update the text value of the appActivationStateTV. Similarly, we invoke the getAircraftBindingState() method of appActivationManager to get the current aircraft binding state and update the text value of bindingStateTV.
  3.最后, 我们调用 appActivationManager 的 getAppActivationState ()方法来获取当前应用激活状态, 并更新 appActivationStateTV 的 Text value。同样, 我们调用 appActivationManager 的 getaircrafts bindingstate ()方法来获取当前的无人机绑定状态, 并更新 bindingStateTV 的Text value。

Once you finished the steps above, let's add another two methods: setUpListener and tearDownListener to setup the listeners and invoke them in the onResume() and onDestroy() methods as shown below:
完成上面的步骤后, 我们再添加另外两个方法: setUpListener 和 tearDownListener 来安装侦听器并在 onResume ()和 onDestroy ()方法中调用它们, 如下所示:
~~~
private void setUpListener() {
    // Example of Listener
    activationStateListener = new AppActivationState.AppActivationStateListener() {
        @Override
        public void onUpdate(final AppActivationState appActivationState) {
            MainActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    appActivationStateTV.setText("" + appActivationState);
                }
            });
        }
    };
    bindingStateListener = new AircraftBindingState.AircraftBindingStateListener() {
        @Override
        public void onUpdate(final AircraftBindingState bindingState) {
            MainActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    bindingStateTV.setText("" + bindingState);
                }
            });
        }
    };
}
private void tearDownListener() {
    if (activationStateListener != null) {
        appActivationManager.removeAppActivationStateListener(activationStateListener);
        MainActivity.this.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                appActivationStateTV.setText("Unknown");
            }
        });
    }
    if (bindingStateListener !=null) {
        appActivationManager.removeAircraftBindingStateListener(bindingStateListener);
        MainActivity.this.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                bindingStateTV.setText("Unknown");
            }
        });
    }
}
@Override
public void onResume() {
    Log.e(TAG, "onResume");
    setUpListener();
    super.onResume();
}
@Override
protected void onDestroy() {
    Log.e(TAG, "onDestroy");
    tearDownListener();
    super.onDestroy();
}
~~~
Here, we implement the following features:
在这里, 我们实现了以下特性:

  1.In the setUpListener() method, we initialize the activationStateListener and bindingStateListener listeners and override their onUpdate() methods to fetch the updated AppActivationState and AircraftBindingState enum values. Then use them to update the text values of the appActivationStateTV and bindingStateTV text views.
  1.在 setUpListener ()方法中, 我们初始化 activationStateListener 和 bindingStateListener 侦听器, 并重写 onUpdate 方法来获取更新的 AppActivationState 和 AircraftBindingState 枚举值。 然后使用它们来更新 appActivationStateTV 和 bindingStateTV TextView的Text value。

  2.Next, since we have added the listeners for the app activation state and aircraft binding state update in the appActivationManager, we also need to remove them. So in the tearDownListener() method, we invoke the removeAppActivationStateListener and removeAircraftBindingStateListener methods of appActivationManager to remove the listeners. Moreover, update the text values of appActivationStateTV and bindingStateTV textViews to "Unknown".
  2.接下来, 由于我们已经为 appActivationManager 添加了APP激活状态和无人机绑定状态侦听器, 我们还需要删除它们。因此, 在拆除监听器方法中, 我们调用 removeAppActivationStateListener 和 removeaircrafts bindingstatelistener 方法来拆除侦听器。此外,更新 appActivationStateTV 和 bindingStateTV TextView的Text value。

  3.Lastly, override the onResume() method and invoke the setUpListener() to setup the listeners. Then override the onDestroy() method and invoke the tearDownListener() method to remove the listeners in appActivationManager.
最后, 重写 onResume ()方法, 调用 setUpListener ()来设置侦听器。然后重写 onDestroy ()方法, 并调用 tearDownListener() 方法来拆除appActivationManager 中的侦听器。

**Working on Login and Logout DJI User Account**
**登录和退出DJI 用户帐户**

In order to activate the application, we need to login a DJI user account. Now let's create the following methods and invoke them in the onClick() method:
为了激活APP, 我们需要登录一个DJI帐户。现在让我们创建下面的方法, 并在 onClick ()方法中调用它们:
~~~
private void loginAccount(){
    UserAccountManager.getInstance().logIntoDJIUserAccount(this,
            new CommonCallbacks.CompletionCallbackWith<UserAccountState>() {
                @Override
                public void onSuccess(final UserAccountState userAccountState) {
                    showToast("Login Success");
                }
                @Override
                public void onFailure(DJIError error) {
                    showToast("Login Error:"
                            + error.getDescription());
                }
            });
}
private void logoutAccount(){
    UserAccountManager.getInstance().logoutOfDJIUserAccount(new CommonCallbacks.CompletionCallback() {
        @Override
        public void onResult(DJIError error) {
            if (null == error) {
                showToast("Logout Success");
            } else {
                showToast("Logout Error:"
                        + error.getDescription());
            }
        }
    });
}
@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.btn_login:{
            loginAccount();
            break;
        }
        case R.id.btn_logout:{
            logoutAccount();
            break;
        }
        default:
            break;
    }
}
~~~
In the code above, we implement the following things:
在上面的代码中, 我们实现了:

  1.In the loginAccount() method, we invoke the logIntoDJIUserAccount() method of UserAccountManager to show the login dialog. And override the onSuccess() and onFailure() methods to show the result messages by invoking the showToast() method.
  1.在 loginAccount ()方法中, 我们调用 UserAccountManager 的 logintoDJIUserAccount ()方法来显示登录对话框。并且重写 onSuccess ()和 onFailure ()方法, 通过调用 showToast 方法来显示登陆结果。

  2.Next, in the logoutAccount() method, we invoke the logoutOfDJIUserAccount() method of UserAccountManager to logout the DJI user account. Also, override the onResult() method to show the result messages.
  2.接下来, 在 logoutAccount ()方法中, 我们调用 UserAccountManager 的 logoutOfDJIUserAccount ()方法来注销 DJI 用户帐户。此外, 重写 onResult 方法来显示退出结果。

For more implementation details, please check this tutorial's Github Sample Project.
有关更多的实现细节, 请查看本教程的 Github 示例项目。

Now, let's build and run the project, connect the demo application to your aircraft (Please check the Run Application for more details) and check the features we have implemented so far.
现在, 让我们建立和运行项目, 将示例APP连接到您的无人机(请检查Run Application更多的细节) , 并检查我们已经实现的功能。

Here are the steps to activate the application:
下面是激活APP的步骤:

  1.If the application is not activated, you may see the following screenshot:     
  1.如果APP没有被激活, 你可能看到下面的截图:
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/initialState-9021228126.png)
  2.Now, let's press the Login button and fill in your email address and password to login and activate the application:
  2.现在, 让我们按下登录按钮, 填写你的电子邮件地址和密码以登录和激活APP:
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/login-270d2911d4.png)
  3.If everything goes well, you may see the appActivationStateTV's text value changes to "Activated": 
  3.如果一切顺利, 你可能会看到Activated
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/activated-45d1ea8687.png)

**Aircraft Binding**
**绑定无人机**

After you finish activating the application, you can now connect your aircraft to DJI Go 4/DJI Go app and bind your aircraft to your DJI account. This is required only once. If you press the Enter Device button, you may see an alertView pop up as shown below:
当激活APP完成后,您现在可以将DJI Go 4 / DJI Go APP连接到您的无人机 ,并将您的无人机绑定到 DJI 帐户。这只需要一次。 如果你按下Enter Device按钮, 你可能会看到弹出框, 如下图所示:
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/linkPhoneNum-897605d479.png)

Now, press the Link button to finish the mobile phone link and verification process. After that, connect the aircraft back to the application, you may see the bindingStateTV's text value has changed to "Bound" as shown below:
现在, 按下 Link 按钮来完成手机验证。随后, APP再次连接到无人机时, 您可以看到 bindingStateTV 的文本值已经改为"Bound", 如下图所示:
![](https://devcn.djicdn.com/images/tutorials-and-samples/Android/ActivationAndBinding/activatedAndBound-909cc1c476.png)

Congratulations! Now, your mobile application and aircraft can be used in China without issues. In another word, your application can now see the aircraft's camera live streams and the flight will not be limited to a cylinder of 100m diameter and 30m height.
恭喜你！现在,你的APP和无人机可以在中国使用。或者说, 你的APP现在可以看到无人机的摄像头直播流, 而且飞行不仅限于一个直径为100米和30米高的圆柱体。

**Summary**
**摘要**

In this tutorial, you’ve learned how to use DJI Mobile SDK to activate the SDK mobile application and use DJI Go app to bind the aircraft to your DJI Acccount. The same steps can be used for activating application and binding aircraft in your application. Hope you enjoy this tutorial, and stay tuned for our next one!
在本教程中, 您已经学会了如何使用 DJI Mobile SDK 来激活基于DJI SDK 开发的APP, 并使用 DJI Go APP将无人机绑定到您的 DJI Acccount。相同的步骤也可以用于激活APP和绑定无人机在您的APP中。希望你喜欢这个教程, 并且为我们的下一篇教程做好准备！


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)