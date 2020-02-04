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
