1、为什么在OC中不能函数重载，就是函数名相同，参数不同？

因为在runtime的objc_method结构体中的SEL method_name的命名规则类似className+method，即同一类中SEL不能重复，不同类中SEL可以重复，它的命名并没有包含参数名。

2、为什么利用runtime可以给分类添加实例变量？

在objc_category的表示指向分类的结构体的指针的定义中，有个属性为struct property_list_t *instanceProperties; instanceProperties：表示Category里所有的properties，这就是我们可以通过objc_setAssociatedObject和objc_getAssociatedObject增加实例变量的原因，不过这个和一般的实例变量是不一样的。

3、**KVO实现原理**

4、**Block实现原理**

5、**Runtime底层**

6、计算机网络基础

7、算法与数据结构

8、<a href= "https://blog.devtang.com/2016/03/13/iOS-transition-guide/" target="_blank">iOS 视图控制器转场详解</a>

9、多线程与锁

10、<a href= "https://www.jianshu.com/p/e99cb4310482" target="_blank">RAC使用</a>

11、<a href= "https://casatwy.com/iosying-yong-jia-gou-tan-viewceng-de-zu-zhi-he-diao-yong-fang-an.html" target="_blank">架构，，模块，，MVVM</a>

12、Podfile制作、framework制作

13、<a href= "https://juejin.im/entry/58e45768ac502e4957a22909" target="_blank">常用的 23 种设计模式基本定义</a>、

#### 目录：

<a href= "https://github.com/ChenYilong/iOSInterviewQuestions/blob/master/01%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88/%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88%EF%BC%88%E4%B8%8A%EF%BC%89.md#11-synthesize%E5%92%8Cdynamic%E5%88%86%E5%88%AB%E6%9C%89%E4%BB%80%E4%B9%88%E4%BD%9C%E7%94%A8" target="_blank">《招聘一个靠谱的iOS -上》</a>

<a href= "https://github.com/ChenYilong/iOSInterviewQuestions/blob/master/01%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88/%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88%EF%BC%88%E4%B8%8B%EF%BC%89.md#49-kvc%E5%92%8Ckvo%E7%9A%84keypath%E4%B8%80%E5%AE%9A%E6%98%AF%E5%B1%9E%E6%80%A7%E4%B9%88" target="_blank">《招聘一个靠谱的iOS -下》</a>

<a href= "https://www.jianshu.com/p/836ac5f1b31d" target="_blank">基础题</a>、<a href= "http://www.cocoachina.com/ios/20190213/26321.html" target="_blank">200道题目</a>、







Iphone - 传感器：

协处理器 M7（Motion coprocessor，不是传感器）

生物识别 - TouchID、FaceID -> LocalAuthentication（本地验证）

压力传感器（3D Touch）<- TAPTIC Engine 振动器

摄像头（广交、长焦）、图像传感器、光学防抖、闪烁传感器（Flicker sensor）

麦克风、音响、多点触控屏幕

Infared camera（红外摄像机）、Flood illuminator（泛光照明器）、Proximity sensor（接近传感器）、Ambient linght sensor（环境光传感器）、Speaker（扬声器）、Microphone（麦克风）、Front camera（前置摄像头）、Dot projector（点投影仪）-> 真深度摄像系统（深度传感器）

加速度传感器（Accelerometer）

湿度传感器（Moisture Sensor）、内部温度传感器（Internal Temperature Sensor）

2G、3G、4G（LTE）、5G / Wi-Fi / 蓝牙（BlueTooth）/NFC（近场通信）

GPS

磁力传感器（Compass）

陀螺仪（Gyroscope）六轴陀螺仪(iphone6)

气压计（Barometer）









