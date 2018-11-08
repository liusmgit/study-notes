# python+appium+Androidsdk



## 一、Android sdk环境搭建
**1.sdk下载安装**
- [sdk下载地址](http://tools.android-studio.org/index.php/sdk)
  ![下载zip包解压安装](https://upload-images.jianshu.io/upload_images/13678389-37ed49a1c2bbc0e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 - 解压安装（**jidk版本必须为1.8**）
  ![解压后双击SDK Manager.exe进行安装](https://upload-images.jianshu.io/upload_images/13678389-f01a8119f5fbd8cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**注：jidk版本必须为1.8**
![点击安装默认的所有包](https://upload-images.jianshu.io/upload_images/13678389-fd144f4a7dadd438.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.配置环境变量**
- ANDROID_HOME    ：   D:\Tools\android-sdk-windows（解压目录）
- PATH   :  %ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools;（固定不变）

**3.验证sdk环境是否搭建完成**

- 进入cmd
- 输入命令 adb version 
  ![出现adb版本号则表示搭建成功](https://upload-images.jianshu.io/upload_images/13678389-4078ea5ae0d8c4bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二、appium环境搭建

**1.appium下载安装**

- [appium下载地址](https://github.com/appium/appium-desktop/releases/latest)
- Windows版本
  ![Windows版本](https://upload-images.jianshu.io/upload_images/13678389-9b1bf0ce03cf3f1a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 双击默认安装即可
  **注：新版appium不需要指定安装目录也不需要多余配置**

**2.appium配置**

- 启动、配置
  ![启动服务](https://upload-images.jianshu.io/upload_images/13678389-ed89a5f754d0d573.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  ![点击配置](https://upload-images.jianshu.io/upload_images/13678389-ee539ccdfdeee6e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  ![添加需要测试的设备和APP相关信息并保存或启动](https://upload-images.jianshu.io/upload_images/13678389-ebc3012ad687a255.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注：
>{
>			"platformName": "Android",
>			"platformVersion": "4.4.2",
>			"deviceName": "127.0.0.1:62001",
>			"appPackage": "com.tencent.mobileqq",
>			"appActivity": ".activity.SplashActivity",
>                               "noReset": "true"
>}

platformName:    Android  或 ios
platformVersion  ： Android版本号
deviceName   ：  127.0.0.1:设备序列号
appPackage  ：  包名
appActivity  ：  包名入口
noReset   ： 是否保留app历史数据（这里建议填写true，不清除历史数据）

**查看设备号**
1.保证手机正常连接电脑并开启usb调试模式
2.cmd命令查看
![adb查看设备号](https://upload-images.jianshu.io/upload_images/13678389-84896b1d075f364e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**查看包名和入口**

1.运行需要测试的app
2.cmd 进入adb shell命令查看
![adb shell 命令查看](https://upload-images.jianshu.io/upload_images/13678389-34122bdc777d92bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 三、python编写脚本

**1.导入Appium-python-Client库**
![添加导入Appium库](https://upload-images.jianshu.io/upload_images/13678389-142bd57820d39b08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.调用库方法、指定设备和app、建立连接**

引入appium 库的 webdriver 模块
> from appium import webdriver

告诉appium需要操作哪个设备、哪个APP
> conf = {
>   "platformName": "Android",
>   "platformVersion": "5.1.1",
>   "deviceName": "127.0.0.1:76UBCKT225TN",
>   "appPackage": "com.simpleway.firebit",
>   "appActivity": "com.huoyidian.splashscreen.LauncherActivity",
>   "noReset": "true"
> }

通过Remote方法连接appium服务
> driver = webdriver.Remote("http://localhost:4723/wd/hub",conf)
> 注：4723为appium默认启动端口，conf为前面自定义变量，其他格式不变。

**3.常用操作**

设置隐性等待时间
> driver.implicitly_wait(10)

强制等待（先全局引入time 方法）

> time.sleep(10)

清空输入框
> driver.find_element_by_xpath('').clear()

输入手机号
> driver.find_element_by_xpath('').send_keys('13688888888')

点击登录
> driver.find_element_by_xpath('').click()

指定滑动
> driver.swipe(500,800,500,400,200)
> （起始坐标X，起始坐标y，结束坐标x，结束坐标y，滑动时间）
> （以屏幕左上角为坐标原点，向右为x，向下为y）

比例滑动
>打印屏幕大小
>print(driver.get_window_size())
>获取屏幕的宽
>x = driver.get_window_size()['width']
>获取屏幕的高
>y = driver.get_window_size()['height']
>向上滑动
>driver.swipe(1/2*x,4/5*y,1/2*x,2/5*y,1000)
>注：建议使用比例滑动，以免换了设备脚本报错问题



