# quick_app
quick_app

# 安装

npm install  or cnpm install or yarn

# 执行

npm run server & npm run watch

# 华为快应用——开发流程

详细看官网

https://developer.huawei.com/consumer/cn/service/hms/catalog/fastapp.html?page=fastapp_fastapp_car_devguide

# 寻找 adb

adb.exe 
1. 在安装 Android Studio 的 sdk 中，d:\sdk\platform-tools
2. 网上找个安装程序
3. 如果你安装了 Huawei QuickApp IDE 的话, Huawei QuickApp IDE\resources\app\extensions\deveco-debug\lib\toolkit

# 模拟器的安装

1.安装Java并配置环境变量：[jdk1.8下载](https://developer.huawei.com/consumer/cn/service/hms/doc/fastapp_fastapp_IDE_car_operguide.html)
2019开始Javasdk要开始收费，需要oracle账户下载，用户名：490204629@qq.com，密码：Huang528*2*。

2.windows开启仿真性能硬件加速
参考如下链接启用Hyper-V加速/启用HAXM加速：[Look]
(https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?pivots=windows)
[Hyper-v](https://docs.microsoft.com/zh-cn/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

3.通过SDK Tools命令行安装
1、下载SDK Tools。[下载链接]：(https://developer.android.com/studio/?gclid=EAIaIQobChMIgcCry_6f5AIV2aqWCh2RXAX-EAAYASAAEgLhgfD_BwE#downloads)

Command line tools only
![images](https://obs.cn-north-2.myhwclouds.com/hms-ds-wf/b/466391b98b2d4e1385a6b9a9065518ce-5186114038772426112.png)

2、解压到{Android_SDK_ROOT}( Android_SDK_ROOT为用户自定义Android SDK文件夹路径，例如D:\sdk)，进入Android_SDK_ROOT目录，在当前目录打开cmd命令行。
3、下载platform，在cmd中执行以下命令：tools\bin\sdkmanager platforms;android-28。
4、下载platform-tools，在cmd中执行以下命令：tools\bin\sdkmanager platform-tools。
5、下载emulator，在cmd中执行以下命令：tools\bin\sdkmanager emulator。

![images](https://obs.cn-north-2.myhwclouds.com/hms-ds-wf/b/aeb1d54347a64e06866089104afd73e8-7781874948842649685.png)


# 调试中的问题

1.使用模拟器：
问题a:emulator: ERROR: AdbHostServer.cpp:102: Unable to connect to adb daemon on port: 5037
啊~adb端口被占用

解决方法：

运行：adb devices

~~~ nodejs
List of devices attached
* daemon not running. starting it now on port 5037 *
error: could not install *smartsocket* listener: cannot bind to 127.0.0.1:5037:
通常每个套接字地址(协议/网络地址/端口)只允许使用一次。 (10048)
could not read ok from ADB Server
* failed to start daemon *
error: cannot connect to daemon
~~~

运行：adb nodaemon server

~~~ nodejs
error: could not install *smartsocket* listener: cannot bind to 127.0.0.1:5037:
通常每个套接字地址(协议/网络地址/端口)只允许使用一次。 (10048)
~~~

运行：netstat -ano | findstr "5037"

~~~ nodejs
查看5037进程
~~~

运行：tasklist | findstr "0000"

~~~ nodejs
找到0000的进程
~~~

运行：taskkill /f /pid 0000

~~~ nodejs
杀掉进程~~
~~~

运行：adb kill-server
运行：adb devices
