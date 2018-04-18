**DJI GEO System Tutorial**
**Dji GEO 系统教程**

2018-01-31v4.4.1 4.4.1Github

If you come across any mistakes or bugs in this tutorial, please let us know using a Github issue, a post on the DJI Forum. Please feel free to send us Github pull request and help us fix any issues.
如果您在本教程中遇到任何错误或错误, 请使用 DJI 论坛上的 Github 问题来告诉我们。 请随时发送 Github 拉请求, 并帮助我们解决任何问题。

In this tutorial, you will learn how to use the FlyZoneManager and FlyZoneInformation of DJI Mobile SDK to get the fly zone information, and unlock authorization fly zones.

在本教程中, 您将学习如何使用 DJI Mobile SDK 的 flyzyemanager 和 FlyZoneInformation 来获取飞区信息, 并解锁授权飞行区域。

You can download the tutorial's final sample project from this Github Page.

您可以从这个 Github 页面下载教程的最终示例项目。

We use Phantom 4 as an example to make this demo. Let's get started!

我们用 Phantom 4作为示例来制作这个演示。 我们开始吧！

**Introduction**
**引言**

The Geospatial Environment Online (GEO) system is a best-in-class geospatial information system that provides drone operators with information that will help them make smart decisions about where and when to fly. It combines up-to-date airspace information, a warning and flight-restriction system, a mechanism for unlocking (self-authorizing) drone flights in locations where flight is permitted under certain conditions, and a minimally-invasive accountability mechanism for these decisions.

地理空间环境在线系统是一个最佳的地理空间信息系统, 为无人机操作员提供信息, 帮助他们在何时何地飞行方面做出明智决定。 它将最新空气空间信息、警报和飞行限制系统、在某些条件下允许飞行的地点解锁(自行授权)无人机飞行的机制, 以及这些决定的微创问责机制。

**Application Activation and Aircraft Binding in China**
**中国应用激活与无人机装订**

For DJI SDK mobile application used in China, it's required to activate the application and bind the aircraft to the user's DJI account.

对于中国使用的 DJI SDK 移动APP, 需要激活APP并将无人机绑定到用户的 DJI 帐户。

If an application is not activated, the aircraft not bound (if required), or a legacy version of the SDK (< 4.1) is being used, all camera live streams will be disabled, and flight will be limited to a zone of 100m diameter and 30m height to ensure the aircraft stays within line of sight.

如果一个APP没有被激活, 无人机不受约束(如果需要) , 或 SDK (4.1)的遗留版本, 所有摄像头实时流都将被禁用, 飞行范围将限制在100米直径和30米高度范围内, 以确保无人机保持在视线范围内。

To learn how to implement this feature, please check this tutorial Application Activation and Aircraft Binding.

要学习如何实现这一特性, 请检查本教程APP激活和无人机绑定。

**Implementing the UI of the Application**
**实现APP的 UI**

In the Importing and Activating DJI SDK in Android Studio Project tutorial, you have learned how to import the DJI Android SDK into your Android Studio project and activate your application. If you haven't read that previously, please take a look at it. Once you've done that, let's continue to create the project.

在Android Studio项目教程中导入和激活 DJI SDK 中, 你已经学会了如何将 DJI Android SDK 导入到你的 Android 工作室项目中并激活你的APP。 如果你以前没有读过这篇文章, 请看一下。 一旦你做到了, 让我们继续创建这个项目。

**Importing Maven Dependency**
**导入 Maven 依赖项**

Open Android Studio and select File -> New -> New Project to create a new project, named 'DJIGEODemo'. Enter the company domain and package name (Here we use "com.dji.geodemo") you want and press Next. Set the minimum SDK version as API 19: Android 4.4 (KitKat) for "Phone and Tablet" and press Next. Then select "Empty Activity" and press Next. Lastly, leave the Activity Name as "MainActivity", and the Layout Name as "activity_main", Press "Finish" to create the project.

打开Android Studio并选择文件-新-新项目创建一个新项目, 命名为"DJIGEODemo"。 输入您想要的公司域名和包名(这里我们使用"com.dji.geodemo")并按下一步。 将最小 SDK 版本设置为 API 19: Android 4.4(KitKat)的"手机和平板电脑", 然后按下一步。 然后选择"空活动"并按下一步。 最后, 将活动名留作"MainActivity", 并将"布局名称"作为"活动主体", 按"完成"来创建项目。

In our previous tutorial Importing and Activating DJI SDK in Android Studio Project, you have learned how to import the Android SDK Maven Dependency and activate your application. If you haven't read that previously, please take a look at it and implement the related features. Once you've done that, continue to implement the next features.

在我们之前的教程中, 你已经学会了如何导入 Android SDK Maven Dependency 并激活你的APP。 如果您以前没有读过这篇文章, 请看一看并且实现相关的功能。 一旦这样做了, 继续实现下一个功能。

**Configurating Google Maps API Key**
**配置 Google 地图 API 密钥**

Since we create this demo project using "Google Maps Activity" of Android Studio, the Google Play Services is set up automatically for you. You can now start using the Google Maps Android APIs to develop your app.

自从我们使用Android Studio的"谷歌地图活动"创建这个演示项目, Google Play 服务就会自动为您设置。 你现在可以开始使用谷歌地图 Android api 来开发你的APP。

To learn how to generate SHA-1 key and how to apply for an Google Maps API key in Google Developer Console, please refer to the Setting Up Google Play Services section of Creating a MapView and Waypoint Application tutorial.

要了解如何生成 SHA-1键以及如何在谷歌开发者控制台中应用谷歌地图 API 密钥, 请参阅创建 MapView 和 Waypoint APP教程的设置谷歌播放服务部分。

Once you finish the above step, please open the "google_maps_api.xml" file in the values folder and replace the YOUR_KEY_HERE with the Google Maps API key you just get as shown below:

一旦你完成上面的步骤, 请在值文件夹中打开"Google 地图 API.xml"文件, 并用 Google 地图 API 密钥替换您的 key here, 如下图所示:

<string name="google_maps_key" translatable="false" templateMergeStrategy="preserve">YOUR_KEY_HERE</string>
Now build and run the project and install it on an Android device(We use Nexus 5 here), you should see the Google Map loads successfully as shown below:

现在建立并运行这个项目并安装在安卓设备上(我们在这里使用 Nexus 5) , 你应该可以看到 Google Map 的成功载荷, 如下图所示:

googleMap

**Building the Layouts of Activity**
**建立活动的布局**

**1. Implementing MApplication and GEODemoApplication**
**1. 实现 MApplication 和 GEODemoApplication**
 
You can check the Creating an Camera Application tutorial and the sample project of this tutorial for the detailed implementations of the MApplication and GEODemoApplication.

您可以检查创建摄像头APP教程和本教程的示例项目, 以详细实现 MApplication 和 GEODemoApplication。

**2. Implementing the ConnectionActivity**
**2. 实现连接活动**

**Implementing UI Elements in ConnectionActivity Class**
**在 ConnectionActivity 类中实现 UI 元素**

To improve the user experience, we had better create an activity to show the connection status between the DJI Product and the SDK, once it's connected, the user can press the OPEN button to enter the MainActivity.

为了改善用户体验, 我们最好创建一个活动来显示 DJI 无人机和 SDK 之间的连接状态, 一旦连接, 用户可以按开放按钮进入 MainActivity。

Now let's Right-click on the package com.dji.geodemo in the project navigator and choose New -> Activity -> Basic Activity, Type in "ConnectionActivity" in the "Activity Name" field and press "Finish" button.

现在让我们在"活动名称"字段中右键单击"com.dji.geodemo"包, 然后在"活动名称"字段中选择"New-Activity-Basic Activity, 输入"ConnectionActivity", 然后按"完成"按钮。

Next, replace the code of the "ConnectionActivity.java" file with the following:

接下来, 将"ConnectionActivity.java"文件的代码替换为:

public class ConnectionActivity extends Activity implements View.OnClickListener {
    private static final String TAG = ConnectionActivity.class.getName();
    private TextView mTextConnectionStatus;
    private TextView mTextProduct;
    private Button mBtnOpen;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        setContentView(R.layout.activity_connection);
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
    private void initUI() {
        mTextConnectionStatus = (TextView) findViewById(R.id.text_connection_status);
        mTextProduct = (TextView) findViewById(R.id.text_product_info);
        mBtnOpen = (Button) findViewById(R.id.btn_open);
        mBtnOpen.setOnClickListener(this);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_open: {
                Intent intent = new Intent(this, MainActivity.class);
                startActivity(intent);
                break;
            }
            default:
                break;
        }
    }
}
In the code shown above, we implement the following features:

在上面显示的代码中, 我们实现了以下特性:

Create the layout UI elements variables, including two TextureViews mTextConnectionStatus, mTextProduct, and one Button mBtnOpen.

创建布局 UI 元素变量, 包括两个 TextureViews mTextConnectionStatus, mTextProduct 和 one Button mBtnOpen。

In the onCreate() method, we request several permissions at runtime to ensure the SDK works well when the compile and target SDK version is higher than 22(Like Android Marshmallow 6.0 device and API 23). Then invoke the initUI() methods to initialize the UI elements.

在 onCreate ()方法中, 我们在运行时请求多个权限, 以确保 SDK 在编译和目标 SDK 版本高于22(如 Android M 6.0设备和 API 23)。 然后调用 initUI ()方法来初始化 UI 元素。

Next, implement the initUI() method to initialize the three TextViews and the Button. Then invoke setOnClickListener() method of mBtnOpen and pass this as the param.

接下来, 实现 initUI ()方法来初始化三个文本视图和按钮。 然后调用 mBtnOpen 的 setOnClickListener 方法, 然后将其作为 param 传递。

Lastly, override the onClick() method to implement the btn_open button action. Here we create an Intent object by passing "MainActivity.class" as the component class to be used for the intent. Then invoke the startActivity() method to start the MainActivity.

最后, 重写 onClick ()方法来实现 btn 开放按钮操作。 在这里, 我们通过将"MainActivity.class"作为用于该意图的组件类来创建意图对象。 然后调用 startActivity 方法来启动 MainActivity。

**Implementing the ConnectionActivity Layout**
**实现连接活动布局**

Open the activity_connection.xml layout file and replace the code with the following:

打开活动连接。 xml 布局文件, 并用以下代码取代代码:

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <TextView
        android:id="@+id/text_connection_status"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="Status: No Product Connected"
        android:textColor="@android:color/black"
        android:textSize="20dp"
        android:textStyle="bold"
        android:layout_alignBottom="@+id/text_product_info"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="89dp" />
    <TextView
        android:id="@+id/text_product_info"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="270dp"
        android:text="@string/product_information"
        android:textColor="@android:color/black"
        android:textSize="20dp"
        android:gravity="center"
        android:textStyle="bold"
        />
    <Button
        android:id="@+id/btn_open"
        android:layout_width="150dp"
        android:layout_height="55dp"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="350dp"
        android:background="@drawable/round_btn"
        android:text="Open"
        android:textColor="@color/colorWhite"
        android:textSize="20dp"
        />
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="430dp"
        android:text="@string/sdk_version"
        android:textSize="15dp"
        android:id="@+id/textView2" />
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceSmall"
        android:text="DJIGEODemo"
        android:id="@+id/textView"
        android:layout_marginTop="58dp"
        android:textStyle="bold"
        android:textSize="20dp"
        android:textColor="@color/colorBlack"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true" />
</RelativeLayout>
In the xml file, we create four TextViews and one Button within a RelativeLayout. We use the TextView(id: text_connection_status) to show the product connection status and use the TextView(id:text_product_info) to show the connected product name. The Button(id: btn_open) is used to open the MainActivity.

在 xml 文件中, 我们在相对论文件中创建了四个 TextViews 和一个 Button。 我们使用 TextView (id: text connection status)来显示无人机连接状态, 并使用 TextView (id: text product info)来显示连接的无人机名称。 按钮(id: btn open)用于打开 MainActivity。

**Configuring the Resource XMLs**
**配置资源 XMLs**

Once you finish the above steps, let's copy all the images file from this Github sample project's drawable folder (app->src->main->res->drawable) to the same folder in your project.

完成上述步骤后, 让我们将这个 Github 示例项目的可绘制文件夹(app-src-main-res-drawable)到项目中的同一个文件夹。

imageFiles

Moreover, open the "colors.xml" file and update the content as shown below:

此外, 打开"colors.xml"文件并更新如下所示的内容:

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="title_dark">#212121</color>
    <color name="white">#FFFFFF</color>
    <color name="button_normal">#50808080</color>
    <color name="button_press">#5086BFFF</color>
    <color name="colorWhite">#FFFFFF</color>
    <color name="colorBlack">#000000</color>
</resources>
Furthermore, open the "strings.xml" file and replace the content with the followings:

此外, 打开"strings.xml"文件并用下面的内容替换内容:

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">DJIGEODemo</string>
    <string name="title_activity_GEODemo">GEODemo</string>
    <string name="action_settings">Settings</string>
    <string name="disconnected">Disconnected</string>
    <string name="product_information">Product Information</string>
    <string name="connection_loose">Status: No Product Connected</string>
    <string name="sdk_version">DJI SDK Version: 3.3</string>
</resources>
Lastly, open the "styles.xml" file and replace the content with the followings:

最后, 打开"styles.xml"文件, 用下面的内容替换内容:

<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>
</resources>
Now, if you open the activity_main.xml file, and click on the Design tab on the bottom left, you should see the preview screenshot of ConnectionActivity as shown below:

现在, 如果你打开活动 main.xml 文件, 点击左下角的设计选项卡, 你会看到 ConnectionActivity 的预览截图如下:

ConnectionActivity

**3. Creating the MainActivity**
**3. 这是一个很好的示例。 创建 MainActivity**
 
**Implementing the MainActivity Layout**
**实现主活动布局**

Open the activity_main.xml layout file and replace the code with the following:

打开活动 main.xml 布局文件, 并用以下代码替换代码:

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="com.dji.geodemo.MainActivity">
    <RelativeLayout
        android:id="@+id/main_title_rl"
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@color/title_dark">
        <ImageButton
            android:id="@+id/ReturnBtnCamera"
            android:layout_width="wrap_content"
            android:layout_height="35dp"
            android:layout_alignParentLeft="true"
            android:layout_centerVertical="true"
            android:layout_marginLeft="5dp"
            android:adjustViewBounds="true"
            android:background="@android:color/transparent"
            android:onClick="onReturn"
            android:scaleType="centerInside"
            android:src="@drawable/selector_back_button" />
        <TextView
            android:id="@+id/ConnectStatusTextView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="GEODemo"
            android:textColor="@android:color/white"
            android:textSize="21sp" />
    </RelativeLayout>
    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <fragment xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            xmlns:map="http://schemas.android.com/apk/res-auto"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:id="@+id/map"
            tools:context="com.dji.myapplication.MainActivity"
            android:name="com.google.android.gms.maps.SupportMapFragment"/>
        <ScrollView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true"
            android:layout_centerVertical="true"
            android:scrollbars="vertical">
            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:orientation="vertical">
                <Button
                    android:id="@+id/geo_login_btn"
                    style="@style/left_button_list_button"
                    android:text="@string/geo_login"/>
                <Button
                    android:id="@+id/geo_logout_btn"
                    style="@style/left_button_list_button"
                    android:text="@string/geo_logout"/>
                <Button
                    android:id="@+id/geo_unlock_nfzs_btn"
                    style="@style/left_button_list_button"
                    android:text="@string/geo_unlock_nfzs"/>
                <Button
                    style="@style/left_button_list_button"
                    android:id="@+id/geo_get_unlock_nfzs_btn"
                    android:text="@string/geo_get_unlock_nfzs"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent" />
                <Button
                    style="@style/left_button_list_button"
                    android:id="@+id/geo_get_surrounding_nfz_btn"
                    android:text="@string/geo_get_surrounding_nfz"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content" />
                <Button
                    android:id="@+id/geo_update_location_btn"
                    style="@style/left_button_list_button"
                    android:text="@string/geo_update_location" />
            </LinearLayout>
        </ScrollView>
        <TextView
            android:layout_width="180dp"
            android:layout_height="wrap_content"
            android:id="@+id/login_status"
            android:textSize="14sp"
            android:textColor="@android:color/black"
            android:layout_alignParentRight="true"
            android:layout_marginRight="0dp"
            android:textAlignment="center" />
        <ScrollView
            android:layout_width="180dp"
            android:layout_height="400dp"
            android:layout_alignParentRight="true"
            android:scrollbars="vertical"
            android:layout_below="@+id/login_status">
            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textColor="@android:color/black"
                android:id="@+id/fly_zone_tv"
                />
        </ScrollView>
    </RelativeLayout>
</LinearLayout>
In the xml file, we implement the following UIs:

在 xml 文件中, 我们实现了以下 UIs:

Create a RelativeLayout to add a back button and a TextView to show the SDK connection status on the top.

创建一个 RelativeLayout 来添加一个后退按钮和一个 TextView 来显示顶部的 SDK 连接状态。

Then create a RelativeLayout and add a scrollView on the left side with eight Buttons from top to bottom: "Login", "Logout", "Unlock NFZs", "Get Unlock NFZs", "Get Surrounding NFZ" and "Update Location", place them vertically.

然后创建一个 RelativeLayout, 在左侧添加一个横滚视图, 从上到下有8个按钮:"Login","Logout","Unlock NFZs","Get Unlock NFZs","Get Surrounding NFZ","Get Surrounding NFZ"和"Update Location", 将它们垂直放置。

Lastly, on the right side, we add a TextView to show the login status and a scrollView with a textView inside to show the fly zone infos.

最后, 在右侧, 我们添加了一个文本视图来显示登录状态和一个带有文本内部视图的横滚视图来显示飞区信息。

Next, open the styles.xml file in the "values" folder and add the following code below the "AppTheme" style:

接下来, 打开"值"文件夹中的样式表.xml 文件, 并在"AppTheme"样式下添加以下代码:

<style name="left_button_list_button">
    <item name="android:minHeight">@dimen/left_button_list_button_height</item>
    <item name="android:layout_width">@dimen/left_button_list_button_width</item>
    <item name="android:layout_height">wrap_content</item>
    <item name="android:paddingLeft">@dimen/left_button_list_button_padding_left</item>
    <item name="android:paddingRight">@dimen/left_button_list_button_padding_right</item>
    <item name="android:layout_marginLeft">@dimen/left_button_list_button_margin_left</item>
    <item name="android:layout_marginTop">@dimen/left_button_list_button_margin_top</item>
    <item name="android:background">@drawable/selector_button</item>
    <item name="android:textSize">@dimen/left_button_list_button_text_size</item>
    <item name="android:textColor">@color/white</item>
</style>
Furthermore, create an xml file named "dimens.xml" inside the "values" folder and replace the code with the followings:

此外, 在"值"文件夹中创建一个名为"dimens.xml"的 xml 文件, 并用下面的代码替换代码:

<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    <!-- left button list -->
    <dimen name="left_button_list_button_width">150dp</dimen>
    <dimen name="left_button_list_button_height">45dp</dimen>
    <dimen name="left_button_list_button_padding_left">5dp</dimen>
    <dimen name="left_button_list_button_padding_right">5dp</dimen>
    <dimen name="left_button_list_button_margin_left">10dp</dimen>
    <dimen name="left_button_list_button_margin_top">10dp</dimen>
    <dimen name="left_button_list_button_text_size">14sp</dimen>
</resources>
Lastly, open the "strings.xml" file and replace the code with the followings:

最后, 打开"strings.xml"文件, 用下面的代码替换代码:

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">DJIGEODemo</string>
    <string name="title_activity_GEODemo">GEODemo</string>
    <string name="action_settings">Settings</string>
    <string name="disconnected">Disconnected</string>
    <string name="product_information">Product Information</string>
    <string name="connection_loose">Status: No Product Connected</string>
    <string name="sdk_version">DJI SDK Version: 3.3</string>
    <!-- GEO with map testing activity-->
    <string name="title_activity_geo_with_map_testing">GeoWithMapTestingActivity</string>
    <string name="demo_desc_geo_with_map">Geo System With Map</string>
    <string name="item_top_left_title">Category</string>
    <string name="item_top_title">EventName</string>
    <string name="Message_WaitStatus">Upload Status</string>
    <string name="title_activity_geo_testing">GeoTestingActivity</string>
    <string name="demo_desc_geo">Geo System</string>
    <string name="geo_get_surrounding_nfz">Get Surrounding NFZ</string>
    <string name="geo_get_location_nfz">Get location NFZ</string>
    <string name="geo_get_unlock_nfz">Get Unlock NFZ</string>
    <string name="geo_refresh_nfz">Refresh Local Data</string>
    <string name="geo_unlock_nfzs">Unlock NFZs</string>
    <string name="geo_get_unlock_nfzs">Get Unlock NFZs</string>
    <string name="geo_login">Login</string>
    <string name="geo_logout">Logout</string>
    <string name="start_simulator">Start Simulator</string>
    <string name="stop_simulator">Stop Simulator</string>
    <string name="geo_update_location">Update Location</string>>
</resources>
Now, if you open the "activity_maps.xml" file, and click on the Design tab on the bottom left, you should see the preview screenshot of MainActivity as shown below:

现在, 如果你打开"activity maps.xml"文件, 点击左下角的"设计"选项卡, 您可以看到 MainActivity 的预览截图如下:

MainActivity

**Implementing UI Elements in MainActivity Class**
**在 MainActivity 类中实现 UI 元素**

Let's come back to the MainActivity.java class, and replace the code with the following, remember to import the related classes as Android Studio suggested:

让我们回到 MainActivity.java 类, 用下面的代码替换代码, 记住按照 Android Studio 的建议导入相关的类:

public class MainActivity extends FragmentActivity implements View.OnClickListener, OnMapReadyCallback {
    private static final String TAG = MainActivity.class.getName();
    
    private GoogleMap map;
    protected TextView mConnectStatusTextView;
    private Button btnLogin;
    private Button btnLogout;
    private Button btnUnlock;
    private Button btnGetUnlock;
    private Button btnGetSurroundNFZ;
    private Button btnUpdateLocation;
    private TextView loginStatusTv;
    private TextView flyZonesTv;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initUI();
        // Obtain the SupportMapFragment and get notified when the map is ready to be used.
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }
    private void initUI() {
        mConnectStatusTextView = (TextView) findViewById(R.id.ConnectStatusTextView);
        btnLogin = (Button) findViewById(R.id.geo_login_btn);
        btnLogout = (Button) findViewById(R.id.geo_logout_btn);
        btnUnlock = (Button) findViewById(R.id.geo_unlock_nfzs_btn);
        btnGetUnlock = (Button) findViewById(R.id.geo_get_unlock_nfzs_btn);
        btnGetSurroundNFZ = (Button) findViewById(R.id.geo_get_surrounding_nfz_btn);
        btnUpdateLocation = (Button) findViewById(R.id.geo_update_location_btn);
        loginStatusTv = (TextView) findViewById(R.id.login_status);
        loginStatusTv.setTextColor(Color.BLACK);
        flyZonesTv = (TextView) findViewById(R.id.fly_zone_tv);
        flyZonesTv.setTextColor(Color.BLACK);
        btnLogin.setOnClickListener(this);
        btnLogout.setOnClickListener(this);
        btnUnlock.setOnClickListener(this);
        btnGetUnlock.setOnClickListener(this);
        btnGetSurroundNFZ.setOnClickListener(this);
        btnUpdateLocation.setOnClickListener(this);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.geo_login_btn:
                break;
            case R.id.geo_logout_btn:
                break;
            case R.id.geo_unlock_nfzs_btn:
                break;
            case R.id.geo_get_unlock_nfzs_btn:
                break;
            case R.id.geo_get_surrounding_nfz_btn:
                break;
            case R.id.geo_update_location_btn:
                break;
        }
    }
    /**
     * Manipulates the map once available.
     * This callback is triggered when the map is ready to be used.
     * This is where we can add markers or lines, add listeners or move the camera. In this case,
     * we just add a marker near Sydney, Australia.
     * If Google Play services is not installed on the device, the user will be prompted to install
     * it inside the SupportMapFragment. This method will only be triggered once the user has
     * installed Google Play services and returned to the app.
     */
    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;
        // Add a marker in Shenzhen and move the camera
        LatLng shenzhen = new LatLng(22.537018, 113.953640);
        mMap.addMarker(new MarkerOptions().position(shenzhen).title("Marker in shenzhen"));
        mMap.moveCamera(CameraUpdateFactory.newLatLng(shenzhen));
    }
}
In the code above, we implement the following features:

在上面的代码中, 我们实现了以下特性:

1. In the onCreate() method, we invoke the initUI() method and create "SupportMapFragment" variable to call the OnMapReady() method asynchronously.

1. 在 onCreate ()方法中, 我们调用 initUI ()方法, 并且异步地创建"SupportMapFragment"变量来调用 OnMapReady ()方法。

2. In the initUI() method, we create a GoogleMap variable, eight Buttons and three TextViews variables for the UI elements, then create the initUI() method to init the UI elements and implement their setOnClickListener method and pass "this" as the parameter.

第二名。 在 initUI ()方法中, 我们为用户界面元素创建一个 GoogleMap 变量、8个按钮和3个 TextViews 变量, 然后创建 initUI ()方法来嵌入 UI 元素, 并实现他们的 setOnClickListener 方法, 并将"this"作为参数。

3. Next, we override the onClick() method for the eight buttons.

3. 这是一个很好的示例。 接下来, 我们重写8个按钮的 onClick ()方法。

4. Lastly, we override the onMapReady() method to initialize the mMap. Then add a marker of Palo Alto, California here for example. So when the Google map is loaded, you will see a red pin tag on Palo Alto, California.

4. 这是一个很好的示例。 最后, 我们重写 onMapReady ()方法来初始化 mMap。 然后在这里加上一个加州帕洛阿尔托的标记。 所以当谷歌地图被加载时, 你会看到加利福尼亚州帕洛阿尔托的红色标签。

We have gone through a long process to setup the UI of the application. Now, let's build and run the project and install it in your Android device to test it. Here we use Nexus 5 for testing. When the application is launched, press the Open button in the ConnectionActivity to open the MainActivity view, then you should see the following screenshot:

我们经历了一个很长的过程来设置APP的用户界面。 现在, 让我们建立并运行这个项目, 并把它安装到你的 Android 设备中来测试它。 在这里我们使用 Nexus 5进行测试。 当APP启动时, 在 ConnectionActivity 中按一下打开按钮来打开 MainActivity 视图, 然后你就可以看到下面的截图:

p4MissionsUIDemo

**Registering Your Application**
**登记你的申请**

**1. Modifying AndroidManifest file**
**1. 修改 AndroidManifest 文件**

After you finish the above steps, let's register our application with the App Key you apply from DJI Developer Website. If you are not familiar with the App Key, please check the Get Started.

完成上述步骤后, 让我们用从 DJI 开发者网站应用的APP密钥来注册我们的APP。 如果您不熟悉APP密钥, 请检查 Get Started。

Let's open the AndroidManifest.xml file and add the following elements on top of <application> element:

让我们打开 AndroidManifest.xml 文件, 在应用元素之上添加以下元素:

<!-- SDK permission requirement -->
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_CONFIGURATION" />
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<uses-permission android:name="android.permission.WRITE_SETTINGS" />
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
<uses-feature
    android:name="android.hardware.usb.host"
    android:required="false" />
<uses-feature
    android:name="android.hardware.usb.accessory"
    android:required="true" />
<uses-feature
    android:glEsVersion="0x00020000"
    android:required="true" />
<!-- SDK requirement permission end -->
In the code above, we specify the permissions of your application needs by adding <uses-permission> elements as children of the <manifest> element.

在上面的代码中, 我们通过添加使用权限元素作为清单元素的子元素来指定APP需求的权限。

Moreover, because not all Android-powered devices are guaranteed to support the USB accessory and host APIs, include two elements that declare that your application uses the "android.hardware.usb.accessory" and "android.hardware.usb.host" feature.

此外, 因为并不是所有的 android 设备都保证支持 USB 配件和主机 api, 因此包含两个元素, 声明你的APP使用了 android.hardware.USB.access"和 android.hardware.USB.host。

Finally, we need to specify the requirement for OpenGL ES version 2.

最后, 我们需要指定 OpenGL ES 版本2的需求。

For more details of description on the permissions, refer to https://developers.google.com/maps/documentation/android/config.

有关权限的详细描述, 请参考 https: / / developers.google.com / maps / documentation / android / config。

Furthermore, let's replace the <application> element with the followings:

此外, 让我们用以下方法替换APP元素:

<!-- SDK requirement permission end -->
<application
    android:name="com.dji.geodemo.MApplication"
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:supportsRtl="true"
    android:theme="@style/AppTheme">
    <!-- DJI SDK -->
    <uses-library android:name="com.android.future.usb.accessory" />
    <meta-data
        android:name="com.dji.sdk.API_KEY"
        android:value="Please enter your App Key here." />
    <meta-data
        android:name="com.google.android.geo.API_KEY"
        android:value="@string/google_maps_key" />
    <meta-data
        android:name="com.google.android.gms.version"
        android:value="@integer/google_play_services_version" />
    <activity
        android:name="dji.sdk.sdkmanager.DJIAoaControllerActivity"
        android:screenOrientation="landscape"
        android:theme="@android:style/Theme.Translucent">
        <intent-filter>
            <action android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED" />
        </intent-filter>
        <meta-data
            android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED"
            android:resource="@xml/accessory_filter" />
    </activity>
    <!-- DJI SDK -->
    <activity android:name=".ConnectionActivity"
        android:screenOrientation="portrait">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
    <activity android:name=".MainActivity"
        android:screenOrientation="landscape"></activity>
</application>
Please enter the App Key of the application in the value part of android:name="com.dji.sdk.API_KEY" attribute. For more details of the AndroidManifest.xml file, please check this tutorial's Github source code of the demo project.

请在 android APP的APP键中输入"com.dji.sdk.API 密钥"属性。 有关 AndroidManifest.xml 文件的更多细节, 请查看本教程的 Github 源代码演示项目。

**2. Working on the GEODemoApplication and ConnectionAcitity**
**2. 工作的地理应用和连接**

For the implementation of the registration logics in the "GEODemoApplication.java" and "ConnectionAcitity.java" files, we don't explain the details here. Please check this tutorial's Github source code.

对于在"GEODemoApplication.java"和"ConnectionAcitity.java"文件中的注册日志, 我们不会在此解释详情。 请检查本教程的 Github 源代码。

Now let's build and run the project and install it to your Android device. If everything goes well, you should see the "Register Success" textView like the following screenshot when you register the app successfully.

现在, 让我们建立并运行这个项目并把它安装到你的 Android 设备上。 如果一切顺利, 当你成功注册APP时, 你应该会看到"注册成功"文本, 就像下面的截图一样。

registerSuccess

**Implementing GEO Features in MainActivity**
**在主活动中实现 GEO 特性**

**Update the Connection Status TextView**
**更新连接状态文本视图**

Let's open MainActivity.java file and add the following two methods to update the mConnectStatusTextView content when product's connection changes:

让我们打开 MainActivity.java 文件, 在无人机连接改变时, 添加以下两种方法来更新 mConnectStatusTextView 内容:

@Override
public void onResume() {
    Log.e(TAG, "onResume");
    super.onResume();
    updateTitleBar();
}
private void updateTitleBar() {
    if (mConnectStatusTextView == null) return;
    boolean ret = false;
    BaseProduct product = GEODemoApplication.getProductInstance();
    if (product != null) {
        if (product.isConnected()) {
            //The product is connected
            MainActivity.this.runOnUiThread(new Runnable() {
                public void run() {
                    mConnectStatusTextView.setText(GEODemoApplication.getProductInstance().getModel() + " Connected");
                }
            });
            ret = true;
        } else {
            if (product instanceof Aircraft) {
                Aircraft aircraft = (Aircraft) product;
                if (aircraft.getRemoteController() != null && aircraft.getRemoteController().isConnected()) {
                    // The product is not connected, but the remote controller is connected
                    MainActivity.this.runOnUiThread(new Runnable() {
                        public void run() {
                            mConnectStatusTextView.setText("only RC Connected");
                        }
                    });
                    ret = true;
                }
            }
        }
    }
    if (!ret) {
        // The product or the remote controller are not connected.
        MainActivity.this.runOnUiThread(new Runnable() {
            public void run() {
                mConnectStatusTextView.setText("Disconnected");
            }
        });
    }
}

**Working on Login and Logout Features**
**关于登录和登出功能的工作**

Now, let's add the following code at the bottom of initUI() method in MainActivity.java file:

现在, 让我们在 MainActivity.java 文件中添加 initUI 方法底部的下面代码:

MainActivity.this.runOnUiThread(new Runnable() {
    public void run() {
        loginStatusTv.setText(loginStatusTv.setText(UserAccountManager.getInstance().getUserAccountState().name());
    }
});
In the code above, we invoke the getUserAccountState() method of UserAccountManager to fetch the current user account status and update the textView loginStatusTv's text content.

在上面的代码中, 我们调用 UserAccountManager 的 getuseraccountaccountstate ()方法来获取当前用户帐户状态, 并更新文本视图、文本内容。

Next, let's implement the onClick() method for btnLogin and btnLogout buttons as shown below:

接下来, 让我们实现 btnLogin 和 btnLogout 按钮的 onClick ()方法, 如下所示:

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.geo_login_btn:
            UserAccountManager.getInstance().logIntoDJIUserAccount(this,
                    new CommonCallbacks.CompletionCallbackWith<UserAccountState>() {
                        @Override
                        public void onSuccess(final UserAccountState userAccountState) {
                            showToast(userAccountState.name());
                            MainActivity.this.runOnUiThread(new Runnable() {
                                @Override
                                public void run() {
                                    loginStatusTv.setText(userAccountState.name());
                                }
                            });
                        }
                        @Override
                        public void onFailure(DJIError error) {
                            showToast(error.getDescription());
                        }
                    });
            break;
        case R.id.geo_logout_btn:
            UserAccountManager.getInstance().logoutOfDJIUserAccount(new CommonCallbacks.CompletionCallback() {
                @Override
                public void onResult(DJIError error) {
                    if (null == error) {
                        showToast("logoutOfDJIUserAccount Success");
                        MainActivity.this.runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                loginStatusTv.setText("NotLoggedin");
                            }
                        });
                    } else {
                        showToast(error.getDescription());
                    }
                }
            });
            break;
        case R.id.geo_unlock_nfzs_btn:
            break;
        case R.id.geo_get_unlock_nfzs_btn:
            break;
        case R.id.geo_get_surrounding_nfz_btn:
            break;
        case R.id.geo_update_location_btn:
            break;
    }
}
In the code above, we invoke the logIntoDJIUserAccount() method of UserAccountManager to present a login view for the user to login. When login success, we update the loginStatusTv's text content with the user account status. Similarly, invoke the logoutOfDJIUserAccount() method of UserAccountManager to log out the user account.

在上面的代码中, 我们调用 useraccountmanagermanager 的 logIntoDJIUserAccount 方法来为用户提供登录视图。 当登录成功时, 我们将 loginStatusTv 的文本内容更新为用户帐户状态。 类似地, 调用 UserAccountManager 的 logoutOfDJIUserAccount ()方法来登出用户帐户。

**Working on GEO System Features**
**开发地理系统功能**

**Update Fly Zone Info and Aircraft Location**
**更新飞行区信息和无人机位置**

If you want to unlock a fly zone, you may need to get the fly zone's ID first. Now let's update the fly zone info in the flyZonesTv and update the aircraft's location when simulated coordinate data changes.

如果你想解锁一个飞行区域, 你可能需要先获得飞行区的 ID。 现在让我们更新 flyZonesTv 中的飞行区信息, 并在模拟坐标数据更改时更新无人机的位置。

Create the following variables above the onCreate() method as shown below:

在 onCreate ()方法上创建以下变量, 如下所示:

private Marker marker;
private LatLng latLng;
private double droneLocationLat = 181, droneLocationLng = 181;
private FlightController mFlightController = null;
Then add the following two methods above the onMapReady() method as shown below:

然后在 onMapReady ()方法之上添加以下两种方法, 如下所示:

private void initFlightController() {
    if (isFlightControllerSupported()) {
        mFlightController = ((Aircraft) DJISDKManager.getInstance().getProduct()).getFlightController();
        mFlightController.setStateCallback(new FlightControllerState.Callback() {
            @Override
            public void onUpdate(FlightControllerState
                                         djiFlightControllerCurrentState) {
                if (mMap != null) {
                    droneLocationLat = djiFlightControllerCurrentState.getAircraftLocation().getLatitude();
                    droneLocationLng = djiFlightControllerCurrentState.getAircraftLocation().getLongitude();
                    updateDroneLocation();
                }
            }
        });
    }
}
public static boolean checkGpsCoordinates(double latitude, double longitude) {
    return (latitude > -90 && latitude < 90 && longitude > -180 && longitude < 180) && (latitude != 0f && longitude != 0f);
}
private void updateDroneLocation(){
    runOnUiThread(new Runnable() {
        @Override
        public void run() {
            if (marker != null) {
                marker.remove();
            }
            if (checkGpsCoordinates(droneLocationLat, droneLocationLng)) {
                LatLng pos = new LatLng(droneLocationLat, droneLocationLng);
                //Create MarkerOptions object
                final MarkerOptions markerOptions = new MarkerOptions();
                markerOptions.position(pos);
                markerOptions.icon(BitmapDescriptorFactory.fromResource(R.drawable.aircraft));
                marker = mMap.addMarker(markerOptions);
            }
        }
    });
}
private boolean isFlightControllerSupported() {
    return DJISDKManager.getInstance().getProduct() != null &&
            DJISDKManager.getInstance().getProduct() instanceof Aircraft &&
            ((Aircraft) DJISDKManager.getInstance().getProduct()).getFlightController() != null;
}
In the code above, we mainly initialize the mFlightController variable and implement the setStateCallback() method of FlightController to invoke the updateDroneLocation() method to update the aircraft location on the map view when it's moving.

在上面的代码中, 我们主要初始化 mFlightController 变量并实现了 FlightController 的 setStateCallback ()方法来调用 updateDroneLocation ()方法来在地图视图中更新无人机位置。

Moreover, let's update the onMapReady() method with the following codes:

此外, 让我们使用下面的代码来更新 onMapReady ()方法:

@Override
public void onMapReady(GoogleMap googleMap) {
    LatLng paloAlto = new LatLng(37.4613697, -122.1237315);
    mMap = googleMap;
    mMap.moveCamera(CameraUpdateFactory.newLatLng(paloAlto));
    mMap.animateCamera(CameraUpdateFactory.zoomTo(17.0f));
    if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
        mMap.setMyLocationEnabled(true);
        return;
    }
    printSurroundFlyZones();
}
In the code above, we initialize the mMap variable and invoke the moveCamera() and animateCamera() methods of GoogleMap class to move the camera and zoom in on the map. Then, invoke the printSurroundFlyZones() method to update the fly zone info.

在上面的代码中, 我们初始化 mMap 变量, 并调用 moveCamera ()和 animateCamera ()。 然后, 调用"surroundflyzones"方法来更新飞行区信息。

Lastly, add the following two methods below the onMapReady() method as shown below:

最后, 在 onMapReady ()方法之下添加以下两种方法, 如下所示:

private void printSurroundFlyZones() {
DJISDKManager.getInstance().getFlyZoneManager().getFlyZonesInSurroundingArea(new CommonCallbacks.CompletionCallbackWith<ArrayList<FlyZoneInformation>>() {
    @Override
    public void onSuccess(ArrayList<FlyZoneInformation> flyZones) {
        showToast("get surrounding Fly Zone Success!");
        updateFlyZonesOnTheMap(flyZones);
        showSurroundFlyZonesInTv(flyZones);
    }
    @Override
    public void onFailure(DJIError error) {
        showToast(error.getDescription());
    }
});
}
private void showSurroundFlyZonesInTv(final List<FlyZoneInformation> flyZones) {
    MainActivity.this.runOnUiThread(new Runnable() {
        @Override
        public void run() {
            StringBuffer sb = new StringBuffer();
            for (FlyZoneInformation flyZone : flyZones) {
                if (flyZone != null && flyZone.getCategory() != null){
                    sb.append("FlyZoneId: ").append(flyZone.getFlyZoneID()).append("\n");
                    sb.append("Category: ").append(flyZone.getCategory().name()).append("\n");
                    sb.append("Latitude: ").append(flyZone.getCoordinate().getLatitude()).append("\n");
                    sb.append("Longitude: ").append(flyZone.getCoordinate().getLongitude()).append("\n");
                    sb.append("FlyZoneType: ").append(flyZone.getFlyZoneType().name()).append("\n");
                    sb.append("Radius: ").append(flyZone.getRadius()).append("\n");
                    sb.append("Shape: ").append(flyZone.getShape().name()).append("\n");
                    sb.append("StartTime: ").append(flyZone.getStartTime()).append("\n");
                    sb.append("EndTime: ").append(flyZone.getEndTime()).append("\n");
                    sb.append("UnlockStartTime: ").append(flyZone.getUnlockStartTime()).append("\n");
                    sb.append("UnlockEndTime: ").append(flyZone.getUnlockEndTime()).append("\n");
                    sb.append("Name: ").append(flyZone.getName()).append("\n");
                    sb.append("\n");
                }
            }
            flyZonesTv.setText(sb.toString());
        }
    });
}
In the code above, we invoke the getFlyZonesInSurroundingArea method of FlyZoneManager to fetch the fly zone informations list, then in the onSuccess() method, invoke the showSurroundFlyZonesInTv() method to update the fly zone infos on flyZonesTv textView.

在上面的代码中, 我们调用 flyzzemanemanager 的 getflyzonesinsurantarea 方法来获取飞区信息列表, 然后在 onSuccess 方法中调用 surroundflyzonesintv ()方法来更新 flyZonesTv 文本中的苍蝇区信息。

Lastly, let's implement the OnClick() method of btnGetSurroundNFZ and btnUpdateLocation buttons as shown below:

最后, 让我们实现 btnsurroundnfz 和 btnUpdateLocation 的 OnClick 方法, 如下所示:

case R.id.geo_get_surrounding_nfz_btn:
    printSurroundFlyZones();
    break;
case R.id.geo_update_location_btn:
    latLng = new LatLng(DataOsdGetPushCommon.getInstance().getLatitude(),
            DataOsdGetPushCommon.getInstance().getLongitude());
    if (latLng != null) {
        //Create MarkerOptions object
        final MarkerOptions markerOptions = new MarkerOptions();
        markerOptions.position(latLng);
        markerOptions.icon(BitmapDescriptorFactory.fromResource(R.drawable.aircraft));
        marker = mMap.addMarker(markerOptions);
    }
    mMap.moveCamera(CameraUpdateFactory.newLatLng(latLng));
    mMap.animateCamera(CameraUpdateFactory.zoomTo(15.0f));
    break;
When you press the btnGetSurroundNFZ button, it will invoke the printSurroundFlyZones() method to update the fly zone infos on the flyZonesTv textView. When you press the btnUpdateLocation method, it will get the updated latitude and longitude data of the aircraft from DataOsdGetPushCommon and update the aircraft location on the map view. Then invoke the moveCamera() and animateCamera() method of GoogleMap to move and zoom in the camera to the aircraft's updated location on the map.

当你按下 getsurroundnfz 按钮时, 它将调用 printSurroundFlyZones ()方法来更新 flyZonesTv textView 上的飞行区信息。 当您按下 btnUpdateLocation 方法时, 它将获取来自 DataOsdGetPushCommon 的无人机的最新经纬度数据, 并在地图视图中更新无人机位置。 然后调用 GoogleMap 的 moveCamera ()和 animateCamera ()方法来移动和缩小摄像头到无人机在地图上的更新位置。

**Unlock Fly Zones**
**解锁飞行区**

Once you finished the above steps, let's create more variables on top of onCreate() method as shown below:

一旦完成上面的步骤, 让我们在 onCreate ()方法之上创建更多的变量, 如下图所示:

private MarkerOptions markerOptions = new MarkerOptions();
private ArrayList<Integer> unlockFlyZoneIds = new ArrayList<Integer>();
Next, update the onResume() method and add the following methods under the onCreate() method:

接下来, 更新简历方法, 并在 onCreate ()方法下添加以下方法:

@Override
public void onResume() {
    Log.e(TAG, "onResume");
    super.onResume();
    updateTitleBar();
    initFlightController();
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
public void onReturn(View view) {
    Log.e(TAG, "onReturn");
    this.finish();
}
In the code above, we mainly override methods of android.app.Activity. In the onResume() method, we invoke the initFlightController() methods to initialize the mFlightController variable.

在上面的代码中, 我们主要是重写 android.app.Activity 的方法。 在 onResume ()方法中, 我们调用 initFlightController 方法来初始化 mFlightController 变量。

Next, add the following code at the bottom of onCreate() method:

接下来, 在 onCreate ()方法的底部添加下面的代码:

DJISDKManager.getInstance().getFlyZoneManager()
        .setFlyZoneStateCallback(new FlyZoneState.Callback() {
            @Override
            public void onUpdate(FlyZoneState status) {
                showToast(status.name());
            }
        });
The code above will show the fly forbid status to the user. For example, if the aircraft is approaching a restricted fly area, it will pop up a message to warn the user.

上面的代码将向用户显示禁飞状态。 例如, 如果无人机正在接近受限制的飞行区域, 它会弹出一个消息来警告用户。

Before we unlock the fly zones, we should show the fly zone on the map by drawing polygons or circles with different colors. Let's define a unlockableIds arrayList, two int values and a FlyfrbBasePainter object above the onCreate() method first:

在我们解锁苍蝇区之前, 我们应该通过绘制不同颜色的多边形或圆来显示在地图上的苍蝇区。 让我们先定义一个不可锁定的 ids 数组列表, 两个 int 值和一个 FlyfrbBasePainter 对象在 onCreate ()方法之上:

private ArrayList<Integer> unlockableIds = new ArrayList<Integer>();
private final int limitFillColor = Color.HSVToColor(120, new float[] {0, 1, 1});
private final int limitCanUnlimitFillColor = Color.argb(40, 0xFF, 0xFF, 0x00);
private FlyfrbBasePainter painter = new FlyfrbBasePainter();
For more details of the FlyfrbBasePainter class, please check the "FlyfrbBasePainter.java" file in this tutorial's Github Sample Project.

有关 FlyfrbBasePainter 类的详细信息, 请在本教程的 Github 示例项目中检查"FlyfrbBasePainter.java"文件。

Then create the updateFlyZonesOnTheMap() method and invoke it in printSurroundFlyZones() method as shown below:

然后创建 updateFlyZonesOnTheMap ()方法, 并在"surroundflyzones ()方法中调用该方法, 如下所示:

private void updateFlyZonesOnTheMap(final ArrayList<FlyZoneInformation> flyZones) {
        if (mMap == null) {
            return;
        }
        MainActivity.this.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                mMap.clear();
                if (latLng != null) {
                    //Create MarkerOptions object
                    final MarkerOptions markerOptions = new MarkerOptions();
                    markerOptions.position(latLng);
                    markerOptions.icon(BitmapDescriptorFactory.fromResource(R.drawable.aircraft));
                    marker = mMap.addMarker(markerOptions);
                }
                for (FlyZoneInformation flyZone : flyZones) {
                    //print polygon
                    if(flyZone.getSubFlyZones() != null){
                        SubFlyZoneInformation[] polygonItems = flyZone.getSubFlyZones();
                        int itemSize = polygonItems.length;
                        for(int i = 0; i != itemSize; ++i) {
                            if(polygonItems[i].getShape() == SubFlyZoneShape.POLYGON) {
                                DJILog.d("updateFlyZonesOnTheMap", "sub polygon points " + i + " size: " + polygonItems[i].getVertices().size());
                                DJILog.d("updateFlyZonesOnTheMap", "sub polygon points " + i + " category: " + flyZone.getCategory().value());
                                DJILog.d("updateFlyZonesOnTheMap", "sub polygon points " + i + " limit height: " + polygonItems[i].getMaxFlightHeight());
                                addPolygonMarker(polygonItems[i].getVertices(), flyZone.getCategory().value(), polygonItems[i].getMaxFlightHeight());
                            }
                            else if (polygonItems[i].getShape() == SubFlyZoneShape.CYLINDER){
                                LocationCoordinate2D tmpPos = polygonItems[i].getCenter();
                                double subRadius = polygonItems[i].getRadius();
                                DJILog.d("updateFlyZonesOnTheMap", "sub circle points " + i + " coordinate: " + tmpPos.getLatitude() + "," + tmpPos.getLongitude());
                                DJILog.d("updateFlyZonesOnTheMap", "sub circle points " + i + " radius: " + subRadius);
                                CircleOptions circle = new CircleOptions();
                                circle.radius(subRadius);
                                circle.center(new LatLng(tmpPos.getLatitude(),
                                        tmpPos.getLongitude()));
                                switch (flyZone.getCategory()) {
                                    case WARNING:
                                        circle.strokeColor(Color.GREEN);
                                        break;
                                    case ENHANCED_WARNING:
                                        circle.strokeColor(Color.BLUE);
                                        break;
                                    case AUTHORIZATION:
                                        circle.strokeColor(Color.YELLOW);
                                        unlockableIds.add(flyZone.getFlyZoneID());
                                        break;
                                    case RESTRICTED:
                                        circle.strokeColor(Color.RED);
                                        break;
                                    default:
                                        break;
                                }
                                mMap.addCircle(circle);
                            }
                        }
                    }
                    else {
                        CircleOptions circle = new CircleOptions();
                        circle.radius(flyZone.getRadius());
                        circle.center(new LatLng(flyZone.getCoordinate().getLatitude(), flyZone.getCoordinate().getLongitude()));
                        switch (flyZone.getCategory()) {
                            case WARNING:
                                circle.strokeColor(Color.GREEN);
                                break;
                            case ENHANCED_WARNING:
                                circle.strokeColor(Color.BLUE);
                                break;
                            case AUTHORIZATION:
                                circle.strokeColor(Color.YELLOW);
                                unlockableIds.add(flyZone.getFlyZoneID());
                                break;
                            case RESTRICTED:
                                circle.strokeColor(Color.RED);
                                break;
                            default:
                                break;
                        }
                        mMap.addCircle(circle);
                    }
                }
            }
        });
    }
private void addPolygonMarker(List<LocationCoordinate2D> polygonPoints, int area_level, int height) {
    if(polygonPoints == null) {
        return;
    }
    ArrayList<LatLng> points = new ArrayList<>();
    for (LocationCoordinate2D point : polygonPoints) {
        points.add(new LatLng(point.getLatitude(), point.getLongitude()));
    }
    int fillColor = limitFillColor;
    if(painter.getmHeightToColor().get(height) != null) {
        fillColor = painter.getmHeightToColor().get(height);
    }
    else if(area_level == FlyForbidProtocol.LevelType.CAN_UNLIMIT.value()) {
        fillColor = limitCanUnlimitFillColor;
    } else if(area_level == FlyForbidProtocol.LevelType.STRONG_WARNING.value() || area_level == FlyForbidProtocol.LevelType.WARNING.value()) {
        fillColor = getResources().getColor(R.color.gs_home_fill);
    }
    Polygon plg = mMap.addPolygon(new PolygonOptions().addAll(points)
            .strokeColor(painter.getmColorTransparent())
            .fillColor(fillColor));
}
private void printSurroundFlyZones() {
    DJISDKManager.getInstance().getFlyZoneManager().getFlyZonesInSurroundingArea(new CommonCallbacks.CompletionCallbackWith<ArrayList<FlyZoneInformation>>() {
        @Override
        public void onSuccess(ArrayList<FlyZoneInformation> flyZones) {
            showToast("get surrounding Fly Zone Success!");
            updateFlyZonesOnTheMap(flyZones);
            showSurroundFlyZonesInTv(flyZones);
        }
        @Override
        public void onFailure(DJIError error) {
            showToast(error.getDescription());
        }
    });
}
In the code above, we implement the following features:

在上面的代码中, 我们实现了以下特性:

In the updateFlyZonesOnTheMap() method, we use a for loop to get each flyZone object in the flyZones arraylist and then check if the flyZone has polygon fly zone and add different shape of fly zones with different colors on the map.

在 updateFlyZonesOnTheMap ()方法中, 我们使用 for 循环将每个 flyZone 对象放入 flyZones 数组列表中, 然后检查 flyZone 是否有多边形飞行区域, 并在地图上添加不同颜色的不同形状的飞区。

Next, in the printSurroundFlyZones() method, we invoke getFlyZonesInSurroundingArea method of FlyZoneManager to get the fly zone infos in the surrounding area. Then invoke the updateFlyZonesOnTheMap() method and pass the flyZones object to draw flyzone shapes on the map. Also, invoke the showSurroundFlyZonesInTv() method to show fly zone infos on the flyZonesTv textView.

接下来, 在环绕飞越区域()方法中, 我们调用 flyzonfuremanager 的 flyzonesrams 方法来获得周围区域的飞行区信息。 然后调用 updateFlyZonesOnTheMap ()方法, 然后通过 flyZones 对象在地图上绘制飞越区域的形状。 此外, 调用 surroundflyzonesintv 方法(surroundflyzonesintv)方法来显示 flyZonesTv textView 上的飞行区信息。

Finally, let's implement the onClick() method of btnUnlock and btnGetUnlock buttons as shown below:

最后, 让我们实现 btnUnlock 和 btnGetUnlock 按钮的 onClick 方法, 如下所示:

case R.id.geo_unlock_nfzs_btn:
    final AlertDialog.Builder builder = new AlertDialog.Builder(this);
    final EditText input = new EditText(this);
    input.setHint("Enter Fly Zone ID");
    input.setInputType(EditorInfo.TYPE_CLASS_NUMBER);
    builder.setView(input);
    builder.setTitle("Unlock Fly Zones");
    builder.setItems(new CharSequence[]
                    {"Continue", "Unlock", "Cancel"},
            new DialogInterface.OnClickListener() {
                public void onClick(DialogInterface dialog, int which) {
                    // The 'which' argument contains the index position
                    // of the selected item
                    switch (which) {
                        case 0:
                            if (TextUtils.isEmpty(input.getText())) {
                                dialog.dismiss();
                            } else {
                                String value1 = input.getText().toString();
                                unlockFlyZoneIds.add(Integer.parseInt(value1));
                            }
                            break;
                        case 1:
                            if (TextUtils.isEmpty(input.getText())) {
                                dialog.dismiss();
                            } else {
                                String value2 = input.getText().toString();
                                unlockFlyZoneIds.add(Integer.parseInt(value2));
                                DJISDKManager.getInstance().getFlyZoneManager().unlockFlyZones(unlockFlyZoneIds, new CommonCallbacks.CompletionCallback() {
                                    @Override
                                    public void onResult(DJIError error) {
                                        unlockFlyZoneIds.clear();
                                        if (error == null) {
                                            showToast("unlock NFZ Success!");
                                        } else {
                                            showToast(error.getDescription());
                                        }
                                    }
                                });
                            }
                            break;
                        case 2:
                            dialog.dismiss();
                            break;
                    }
                }
            });
    builder.show();
    break;
case R.id.geo_get_unlock_nfzs_btn:
    DJISDKManager.getInstance().getFlyZoneManager().getUnlockedFlyZones(new CommonCallbacks.CompletionCallbackWith<List<FlyZoneInformation>>(){
        @Override
        public void onSuccess(final List<FlyZoneInformation> flyZoneInformations) {
            showToast("Get Unlock NFZ success");
            showSurroundFlyZonesInTv(flyZoneInformations);
        }
        @Override
        public void onFailure(DJIError djiError) {
            showToast(djiError.getDescription());
        }
    });
    break;
In the code above, we implement the following features:

在上面的代码中, 我们实现了以下特性:

1. For the case of btnUnlock button, we create an "AlertDialog" with the title of "Unlock Fly Zone ID", and add a EditText with the hint of "Enter Fly Zone ID". Then create three items for Continue, Unlock, and Cancel actions:

1. 对于 btnUnlock 按钮, 我们创建了一个"AlertDialog", 标题为"Unlock Fly Zone ID", 并添加一个带有"进入飞行区 ID"提示的 EditText。 然后为"继续"、"解锁"和"取消"操作创建三个项:

Continue Action

继续行动

It will add the current input fly zone ID to the unlockFlyZoneIds ArrayList and dismiss the "AlertDialog".

它将把当前输入的飞行区 ID 添加到非锁定的 zoneids ArrayList 中, 并解除"AlertDialog"。

Unlock Action

解锁行动

It will add the current input fly zone ID to unlockFlyZoneIds ArrayList and invoke the unlockFlyZones() method of FlyZoneManager by passing the unlockFlyZoneIds array to unlock fly zones.

它将添加当前输入苍蝇区 ID 到解锁 flyzoneids ArrayList 并调用 FlyZoneManager 的非锁定区()方法, 通过解锁 flyzoneids 阵列来解锁飞区。

Cancel Action

取消操作

It will dismiss the "AlertDialog".

它将撤销"AlertDialog"。

2. For the case of btnGetUnlock button, we invoke the getUnlockedFlyZones() method of FlyZoneManager to fetch unlocked fly zone infos, then override the onSuccess() method and invoke the showSurroundFlyZonesInTv() method by passing the flyZoneInformations ArrayList to update the fly zone infos in the right flyZonesTv textView.

第二名。 对于 btnGetUnlock 按钮, 我们调用 flyzonemanemanager 的 getUnlockedFlyZones ()方法来获取未解锁的 fly zone infos, 然后重写 onSuccess ()方法, 并调用 surroundflyzonesintv ()方法, 通过 flyZoneInformations ArrayList 来更新 flyZonesTv textView 中的飞区信息。

For more details of the implementation, please check this tutorial's Github Sample Project.

有关实现的更多细节, 请查看本教程的 Github 示例项目。

**Running the Sample Code**
**运行示例代码**

We have gone through a long way so far, now, let's build and run the project, connect the demo application to your Phantom 4 (Please check the Run Application for more details) and check all the features we have implemented so far.

到目前为止, 我们已经经历了很多, 现在, 让我们建立和运行这个项目, 将演示APP连接到您的 Phantom 4(请检查运行APP更多的细节) , 并检查我们迄今为止已经实现的所有功能。

**Unlock Authorization Fly Zone Workflow**
**解锁授权飞行区工作流程**

1. Login your verified DJI account, if it's a new account, you need to complete the verification process.

1. 如果是一个新帐户, 请登录您的已验证的 DJI 帐户, 您需要完成验证过程。

2. Open the Simulator of DJI Assistant 2 or DJI PC Simulator and enter the coordinate data (37.4613697, -122.1237315) (Near Palo Alto Airport) to start simulating the aircraft's coordinate to the authorization area.

第二名。 打开 DJI 助手2或 DJI PC 模拟器的模拟器, 输入坐标数据(37.4613697-122.1237315)(近帕洛阿尔托机场) , 开始模拟无人机与授权区域的坐标。

3. Press UPDATE LOCATION and GET SURROUNDING NFZ buttons to update the aircraft location on the map and update the fly zone information around the aircraft on the right textView.

3. 这是一个很好的示例。 按下更新位置和 GET SURROUNDING NFZ 按钮以更新地图上的无人机位置, 并更新右文本文本中无人机周围的飞行区信息。

4. Get the authorization fly zone ID you want to unlock from the textView, the category of it should be Authorization.

4. 这是一个很好的示例。 从 textView 中获取要解锁的授权飞行区 ID, 它的类别应该是授权。

5. Press UNLOCK NFZS button and enter the fly zone ID to unlock it.

第五名。 按下 NFZS 按钮, 然后输入飞行区域 ID 来解锁它。

6. If you unlock the fly zone successfully, you can press the GET SURROUNDING NFZ button to refresh the fly zone infos on the right textView, you may notice that one of the yellow circle will disappear in the map. And you can take off the aircraft in the simulator now.

6. 这是一个很好的示例。 如果你成功解锁了飞行区域, 你可以按下 GET 周围的 NFZ 按钮来刷新右边文本上的苍蝇区信息, 你可能会注意到其中一个黄色的圆圈将在地图中消失。 你现在可以在模拟器里把无人机取下来了。

Note: Limited Simulation Area

注意: 模拟区域有限

Currently, you can only test the GEO feature within 50km of (37.453671, -122.118101), which is the location of Palo Alto Airport in California, United States.

目前, 你只能在美国加州帕洛阿尔托机场50公里(37.453671, -122.118101)的50公里范围内进行测试。

**Login and Logout DJI Account**
**登入和登出 DJI 帐户**

**1. Login DJI Account**
**1. 登入 DJI 帐户**

Press the LOGIN button and a login view will pop up as shown below:

按下登录按钮, 登录视图将弹出, 如下所示:

login

If it's a new DJI account, it will show a verification view as shown below:

如果是一个新的 DJI 帐户, 它将显示一个验证视图, 如下所示:

verificationView

**2. Logout DJI Account**
**第二名。 登出 DJI 帐户**

Press the LOGOUT button to logout your DJI account.

按 LOGOUT 按钮登出您的 DJI 帐户。

On the upper right corner of the screenshot, you can check the loginStatusTv's info for the user account status as shown below:

在截图的右上角, 你可以查看 loginStatusTv 的用户帐户状态信息如下:

accountStatus

**Use DJISimulator to Simulate Aircraft Location**
**使用 DJISimulator 模拟无人机位置**

We will use the DJISimulator to simulate the test environment to locate the aircraft to specific latitude and longitude coordinate.

我们将使用 DJISimulator 来模拟测试环境, 将无人机定位到特定的经纬度坐标。

If you are using Phantom 4 for testing, please check DJI Assistant 2 Simulator tutorial for details, otherwise, if you are using Phantom 3 Professional, Inspire 1, etc, please check DJI PC Simulator tutorial for details.

如果您正在使用精灵4进行测试, 请检查 DJI 助手2模拟器教程详细信息, 否则, 如果您使用的是 Phantom 3 Professional, Inspire 1等, 请检查 DJI PC 模拟器教程。

Open the Simulator of DJI Assistant 2 or DJI PC Simulator and enter the coordinate data (37.4613697, -122.1237315) (Near Palo Alto Airport) to start simulating the aircraft's coordinate to the authorization area.

打开 DJI 助手2或 DJI PC 模拟器的模拟器, 输入坐标数据(37.4613697-122.1237315)(近帕洛阿尔托机场) , 开始模拟无人机与授权区域的坐标。

Press UPDATE LOCATION and GET SURROUNDING NFZ buttons to update the aircraft's location on the map and update the fly zone information around the aircraft on the right textView.

按下更新位置和 GET SURROUNDING NFZ 按钮, 以更新无人机在地图上的位置, 并更新无人机右侧文本中的飞行区信息。

Wait for a while, you may see there a red aircraft placed inside the yellow circle, which is an authorization fly zone you can unlock as shown below:

等一会儿, 你可能会看到一个红色的无人机放在黄色的圆圈里, 这是一个授权飞行区域, 你可以解锁, 如下图所示:

updateFlyZone

Also the textView on the right side will show the FlyZoneInformation info, includes the fly zone name, fly zone id (required in the unlock process), fly zone category, type, etc.

右侧的 textView 还会显示 FlyZoneInformation 信息, 包括飞行区域名称、飞行区域 id (在解锁过程中需要)、飞行区类别、类型等。

Here are the explanation of the three fly zone circles:

以下是对三个苍蝇圈的解释:

Green Circle

绿圈

It represents the warning fly zones, which do not restrict flight and are informational to alert the user. In a warning fly zone, users should be prompted with a warning message describing the zone.

它代表了警告飞行区域, 它不限制飞行, 并且提供信息提醒用户。 在一个警告飞行区, 用户应该被提示一个描述该区域的警告信息。

Yellow Circle

黄色圆圈

It represents the authorization fly zone, which will restrict the flight by default, it can be unlocked by a GEO verified user.

它代表授权飞行区, 这将限制默认的飞行, 它可以通过 GEO 验证的用户解锁。

Red Circle

红圈

It represents the restricted fly zone, it will restrict the flight by default and cannot be unlocked by a GEO verified user.

它代表了限制飞行区域, 它将默认地限制飞行, 并且不能被地球同步轨道验证的用户解锁。

**Unlock and Get Unlock Fly Zones**
**解锁和获得解锁飞行区**

**1. Unlock Fly Zone**
**1. 解锁飞行区**
 
After you login with your DJI account and locate the aircraft to the coordinate of (37.4613697, -122.1237315), you can press the UNLOCK NFZS button and type in the fly zone ID to unlock it.

当你登录了 DJI 账户并将无人机定位到坐标(37.4613697-122.1237315)之后, 你可以按下解锁开锁的 nfz 按钮并在飞行区 ID 中键入来解锁它。

If you unlock the fly zone successfully, you can press the GET SURROUNDING NFZ button to refresh the fly zone infos on the right textView, and one of the yellow circle will disappear in the map as shown in the following gif animation:

如果你成功地解锁了飞行区域, 你可以按下 GET 周围的 NFZ 按钮来刷新右边 textView 上的苍蝇区信息, 黄色的圆圈中的一个将消失在地图中, 如下面的 gif 动画所示:

unlockFlyZone

**2. Get Unlock Fly Zone List**
**第二名。 获取解锁飞行区名单**

You can press the GET SURROUNDING NFZ button to get the fly zone you have unlocked before on the right textView as shown below:

你可以按下 GET 周围的 NFZ 按钮获取之前在右文本视图上打开的飞行区域, 如下图所示:

getUnlockFlyZones

Lastly, please restart the aircraft to make the settings become effective.

最后, 请重新启动无人机, 使设置变得有效。

**Summary**
**摘要**

In this tutorial, you've learned how to use the FlyZoneManager and FlyZoneInformation of DJI Mobile SDK to get the fly zone information, how to unlock authorization fly zones and how to add aircraft annotation and draw fly zone circle overlays on the map view to represent the fly zones. Moreover, you've learned how to use the DJISimulator to simulate the aircraft's coordinate and test the GEO System feature indoor without flying outside.

在本教程中, 您已经学会了如何使用 DJI Mobile SDK  的 flyzyemanager 和 FlyZoneInformation 来获取飞区信息, 如何解锁授权飞行区域, 如何添加无人机注意, 如何在地图视图上绘制飞行区域圆图来表示飞区。 此外, 您已经学会了如何使用 DJISimulator 来模拟无人机的坐标, 并在室内测试 GEO 系统的特性, 而不需要在室外飞行。

Hope this tutorial can help you integrate the GEO System feature in your DJI SDK based Application. Good luck, and hope you enjoyed this tutorial!

希望这个教程能够帮助您在基于 DJI SDK 的APP中集成 GEO 系统功能。 祝你好运, 希望你喜欢这个教程！


如果您觉得文档翻译有不妥，欢迎到Github上发起push请求，
如果你觉得本文档对您有帮助，可以通过赞赏来帮助我持续维护文档
也可以扫描下面的二维码加我微信拉您进DJI Mobile SDK 开发者群 探讨DJI SDK开发相关问题
![](images/20180303_092058.jpg)