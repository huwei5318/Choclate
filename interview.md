
 ---
    面试中应该注意的问题 
 ---
# 1，移动端协同ReactNative开发。
## ReactNative优点：
- 由于react不在ui主线程运行，所以应用可以在不牺牲灵活性的前提下保持高性能（当属性props和状态发生改变时，reactnative会重新渲染视图）
- 大减少开发移动应用所需要的资源。避免了平台分工的需要，可以让团队更快的迭代产品，并且更加高效的共享知识和资源。
## 缺点：
- 整个框架还不成熟，文档还有提升的控件。一些特性在ios和android平台仍然得不到支持。
- 使用中，调试不是像以前原生代码那么流畅。
# 2，Android视频，流媒体，蓝牙，等操作，掌握各个机型及系统版本适配。
## 视频：
## 蓝牙：
- 蓝牙技术是一种无线技术标准，可实现设备之间的短距离数据交换。Android为蓝牙技术提供了4个工具类，分别是蓝牙适配器BluetoothAdapter、蓝牙设备BluetoothDevice、蓝牙服务端套接字BluetoothServerSocket
和蓝牙客户端套接字BluetoothSocket。

- 蓝牙连接的 5个步骤：
    1,连接蓝牙适配器 BluetoothAdapter mAdapter= BluetoothAdapter.getDefaultAdapter();
### 2,打开蓝牙
        if(!mAdapter.isEnabled()){
        //弹出对话框提示用户是后打开
        Intent enabler = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
        startActivityForResult(enabler, REQUEST_ENABLE);
        //不做提示，强行打开，此方法需要权限&lt;uses-permissionandroid:name="android.permission.BLUETOOTH_ADMIN" /&gt;
        // mAdapter.enable();
        }
### 3,搜索设备
### 4,建立连接（通过BluetoothSocket简历连接）服务端（BluetoothSocket)和客户端（BluetoothServerSocket）需要
    指定相同的uuid，才能建立连接，因为建立连接的方法会阻塞线程，所以服务器端和客户端都应该启动新线程连接。
        服务器端：BluetoothServerSocket serverSocket = mAdapter. listenUsingRfcommWithServiceRecord(serverSocketName,UUID);
    serverSocket.accept();

        客户端：BluetoothSocket clienSocket=dcvice. createRfcommSocketToServiceRecord(UUID);
    clienSocket.connect();
 ### 5,数据传递（通过流传递）

# 4、热更新修复原理及应用实现。
## 为甚么需要热更新：
        1，无需重新发布版本，及时的修复问题。
        2，用户无需下载新应用
        3，修复成功率搞
## 热更新主要核心技术：
        1，腾讯tinker
        2,
# 5、掌握客户端网络、图片、内存、动画优化等设计，增强用户体验。
## 图片优化：
        1，为什么bitmap会导致一个应用堆内存vm值上限，用来限定每个应用可用的最大内存，超出这个值就会报oom，这个值
            1，一般根据手机屏幕dpi大小递增，dpi越小的手机，每个应用可用最大的内存就越低。所以加载图片数量很多时，就会造成oom。
            2，图片分辨率越高，消耗内存就越大。
            3，在使用列表组件的时候，如果没有合适的缓存处理，大量加载bitmap时候，就很容易引发oom
        2,Bitmap的优化策略
            1，对图片质量进行压缩。
            2，对尺寸进行压缩。  
            3，多使用点9图片，体积小，拉伸不变形。
            4，使用成熟的图片框架
        3，图片的三级缓存策略
            1，一级缓存指的是内存缓存，
            2，二级缓存指手机sd卡的files或手机内部filesz中的缓存图片文件。
            3，服务端保存的文件图片
 ## 内存优化：
        1，珍惜Service，尽量使用intentService。IntentService在内部通过线程以及handler实现，有新的intent到来的时候，
        会创建线程来处理这个intent，处理完后就自动销毁，所以使用IntentService会大大地节省系统资源。
        2，上述图片优化
        3，尽量少用枚举变量，抽象，避免使用依赖注入框架。使用代码混淆。
        4，即时回收内存中不使用的对象，app内存段时间内快速增长或GC就会非常容易出现内存溢出的现象。

# 在项目设计中会用到设计模式，掌握常见的算法。
## 设计模式
    1，观察者模式
> 让多个观察者对象同时监听一个主题对象，这个主题对象在状态上发生变化是，会通知所有的观察者对象，使观察者们能自己更新自己。
> 
    2，单例模式
>确保某一个类只有一个实例，自行实例化并向整个系统提供这个实例单例模式。

>
    3，适配器模式
>主要用于listview列表数据集合，对应适配器作为桥梁，处理响应的数据。
>
    4，工厂模式
>简单工厂模式提供一个方法，方法的参数是标志位，根据标志位来创建不同的对象，这样调用的 时候只需要提供一个标志位就能创建一个实现了接口的类。
>
# 拥有良好的编程习惯和思想，对项目结构重构优化有深入的理解。
## Android系统框架的理解
	首先，Android系统是以Linux操作系统为核心的，从下至上依次为
- 1，	Linux核心提供了电源管理、进程调度、内存管理等核心系统服务，
- 2，	android运行时   核心包（jdk提供的包，虚拟机、及c++/c的一些库，
- 3，	应用程序框架（包含应用开发所必须的一些api，提供软件复用）
- 4，	应用程序层  包含了系统应用及第三方应用
## 	四大组件
1，	Activity主要是负责与用户交互的组件
2，	Service 为其他组件提供后台服务或者监控其他组件的运行状态。经常用来执行一些耗时操作。
3，	BroadcastReceiver：用于监听应用程序中的其他组件。
4，	ContentProvider：Android应用程序之间实现实时数据交换。

Handler发送消息，发送出的消息由消息队列管理，然后Looper将消息从消息队列中取出来，最终再次交给handler来处理。

# 华为快应用开发
