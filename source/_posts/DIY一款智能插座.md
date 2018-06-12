---
title: DIY一款智能插座
tags: esp8266
---

----------

基于esp8266和机智云的远程控制设备的设计

----------

> 比如这个插座
> ![智能插座](https://i.loli.net/2018/05/08/5af15bd109209.jpg)

----------
<!--more-->

> 比如手机端的app
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15bf58c8ce.jpg)
> 会安卓编程的也可以自己修改一下布局文件，修改一下背景和logo什么的，这样就可以做成自己的软件喽。


----------


> 再可以看下这段视频
> <iframe frameborder="0" width="640" height="498" src="https://v.qq.com/iframe/player.html?vid=q05162syqld&tiny=0&auto=0" allowfullscreen></iframe>

----------
## 前言 ##
>前言：（此教程针对新手，大神略过）
> 我这个人比较懒，挣扎了很久才决定写这个教程，主要是源于闲鱼的很多朋友问教程毕竟我在闲鱼从来不卖东西，偶尔发个玩意分享分享教程，哎呀，平时时间不是太多，最近的学习状态也不是太好，还有比赛，说实话（我计算机二级还没过），最近还要考试，哎呦难得很，理论和现实还是有很大差距的，写了那么久的程序，计算机二级也算是难倒我了，主要是没有太多时间去看那些知识点，风萧萧兮易水寒，今天果断下定决心坐下来，给朋友写一个教程。

```
我还想说的一些话：有些东西的制作，实践比理论要重要得多，当你拿到esp8266的时候商家或者论坛肯定会给给你一些资料，让你一步一步调AT指令，建服务器，，固然有用，但是你不能从中获得优越感，和成就感，因为你根本没有做出一个能实际远程控制的一个实物，只能慢慢的从入门到放弃，让它吃灰。
```

----------

> 关于标题：
> 为什么说是--*远程控制智能插座不用入门直接上手* --呢？
 1. 有对应的平台服务器可以对接这次试用机智云--
 2. 服务器自动生成C语言代码
 3. 服务器自动生成安卓SDK

----------

![这里写图片描述](https://i.loli.net/2018/05/08/5af15c1ab5f2b.png)
> 机智云平台--[http://www.gizwits.com/](http://www.gizwits.com/)
> 为什么不选择onenet？为什么不要选择link？和其他的IOT网站？
> 因为其他的我都做失败了。。。。。哈哈
> 备注：我们使用的是mcu方案，为什么不采用soc的嵌入式开发呢，不太适合新手，再说了成本也差不了多少钱，仅仅一个arduino mini板的钱，


----------
## 材料准备 ##
> 开始吧，教程开始：
> 首先时软件准备--机智云账号， arduinoIDE
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15c3255c55.png)
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15c42aa3c7.png)
> 其次是硬件准备--arduino板，经测试什么样的板子都可以，无论是arduinoR3还是arduino nano还是arduinomini都可以的，
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15c614963b.jpg)
> 还有esp8266 ESP01
> 为什么选择ESP01呢？-------便宜呀！！
> 其次针对mcu方案，没必要买esp12F那样的板子，接线不方便，也没必要。
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15c7b86585.jpg)


----------
## 正式开始 ##

>  1. 开始注册机智云账号并生成应用并配置数据点，这方面不再详述，如果有需求，下次我再下一个文章，一步一步截图发出来。官方教程如下--[http://docs.gizwits.com/zh-cn/quickstart/UseMCU.html](http://docs.gizwits.com/zh-cn/quickstart/UseMCU.html)
>  比如我的插座（带定时功能）
>  ![这里写图片描述](https://i.loli.net/2018/05/08/5af15ca15cf0f.png)
 2. 当你按照上面的教程做好之后，不夸张的说，你已经完成了

三分之一
----

了。哈哈，是不是很简单，
3.烧写固件--这是一个重点！
论坛的资料和教程我试了很多最终一个稳定的方案就是如图的烧写方式
![这里写图片描述](https://i.loli.net/2018/05/08/5af15cb6a8a79.png)
详细教程可以看我的博客园文档
[http://www.cnblogs.com/pengwenzheng/p/8053167.html](http://www.cnblogs.com/pengwenzheng/p/8053167.html)
烧写的固件为机智云官方的固件
下载地址--[https://download.gizwits.com/zh-cn/p/92/94](https://download.gizwits.com/zh-cn/p/92/94)
![这里写图片描述](https://i.loli.net/2018/05/08/5af15ccd32a58.png)
固件烧写完成之后就要进行调试了，使用机智云官方的调试工具进行远程调试，这个时候你就可以在手机下载调试软件实现远程的调试了，
![这里写图片描述](https://i.loli.net/2018/05/08/5af15ceb6aaeb.png)


----------
到这里呢，你已经完成

一半
--

> 了，剩下的就是到机智云的服务器开发者中心，生成mcu代码，就是机智云自动生成的arduino的ino文件，是不是很舒服的说。。。。。。
> 流程如下：
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15d00820a2.png)
接着下载即可：
![这里写图片描述](https://i.loli.net/2018/05/08/5af15d170fa33.png)
下载之后就是一个压缩包，接下之后是机智云针对你的应用的库文件。
![这里写图片描述](https://i.loli.net/2018/05/08/5af15d2b563dd.png)
解压之后打开，只有一个文件名字为--Gizwits
把这个库拷贝到arduinoIDE的库文件夹里即可：不然无法变编译的，大家应该是知道的。![这里写图片描述](https://i.loli.net/2018/05/08/5af15d40d26f1.png)
ok到这里差不多

四分之三
----

> 了，恩恩，下面的工作就剩代码的调试和硬件的组装了，
> 代码调试如下：比如我的文件为：D:\1arduino2018\Arduino\libraries\Gizwits\examples
> 就是解压下来的库文件里面的两个历程：
> ![这里写图片描述](https://i.loli.net/2018/05/08/5af15d4fd6c3e.png)
> 机智云官方是自动生成两个文件的，一个是联网的文件，一个是针对你设置的数据点的应用的控制代码
> 好了将两者融合如下：例如我的插座的代码为：
>

```
#include <Gizwits.h>
#include <Wire.h>
#include <SoftwareSerial.h>
SoftwareSerial mySerial(A2,A3); // A2 -> RX, A3 -> TX
Gizwits myGizwits;
#define   KEY1              6
#define   KEY2              7
#define   KEY1_SHORT_PRESS  1
#define   KEY1_LONG_PRESS   2
#define   KEY2_SHORT_PRESS  4
#define   KEY2_LONG_PRESS   8
#define   NO_KEY            0
#define   KEY_LONG_TIMER    3
int flag =0;
unsigned long Last_KeyTime = 0;
unsigned long gokit_time_s(void)
{
  return millis() / 1000;
}
char gokit_key1down(void)//按键函数，不用管
{
  unsigned long keep_time = 0;
  if (digitalRead(KEY1) == LOW)
  {
    delay(100);
    if (digitalRead(KEY1) == LOW)
    {
      keep_time = gokit_time_s();
      while (digitalRead(KEY1) == LOW)
      {
        if ((gokit_time_s() - keep_time) > KEY_LONG_TIMER)
        {
          Last_KeyTime = gokit_time_s();
          return KEY1_LONG_PRESS;
        }
      } //until open the key

      if ((gokit_time_s() - Last_KeyTime) > KEY_LONG_TIMER)
      {
        return KEY1_SHORT_PRESS;
      }
      return 0;
    }
    return 0;
  }
  return 0;
}

char gokit_key2down(void)//按键函数不用管。
{
  int unsigned long keep_time = 0;
  if (digitalRead(KEY2) == LOW)
  {
    delay(100);
    if (digitalRead(KEY2) == LOW)
    {
      keep_time = gokit_time_s();
      while (digitalRead(KEY2) == LOW) //until open the key
      {

        if ((gokit_time_s() - keep_time) > KEY_LONG_TIMER)
        {
          Last_KeyTime = gokit_time_s();
          return KEY2_LONG_PRESS;
        }
      }
      if ((gokit_time_s() - Last_KeyTime) > KEY_LONG_TIMER)
      {
        return KEY2_SHORT_PRESS;
      }
      return 0;
    }
    return 0;
  }
  return 0;
}
char gokit_keydown(void)
{
  char ret = 0;
  ret |= gokit_key2down();
  ret |= gokit_key1down();
  return ret;
}
void KEY_Handle(void)//这里是检测按键的函数，不用管
{
  switch (gokit_keydown())
  {
    case KEY1_SHORT_PRESS:
      myGizwits.setBindMode(WIFI_PRODUCTION_TEST);
      break;
    case KEY1_LONG_PRESS:
      myGizwits.setBindMode(WIFI_RESET_MODE);
      break;
    case KEY2_SHORT_PRESS:
      myGizwits.setBindMode(WIFI_SOFTAP_MODE);
      break;
    case KEY2_LONG_PRESS:
      myGizwits.setBindMode(WIFI_AIRLINK_MODE);//这里我自己加了一个如果开启了配网功能，蜂鸣器就响一秒。很好用哦
    digitalWrite(5,HIGH);
    digitalWrite(8,HIGH);
    delay(1000);
   digitalWrite(8,LOW);
   digitalWrite(5,LOW);
      break;
    default:
      break;
  }
}
void wifiStatusHandle()//这个函数我做了修改，因为没什么用。
{
  if(myGizwits.wifiHasBeenSet(WIFI_SOFTAP))
  {
  }  
  if(myGizwits.wifiHasBeenSet(WIFI_AIRLINK))
  {
  } 
}
void setup() {
  // put your setup code here, to run once:
  mySerial.begin(115200);
   pinMode(KEY1, INPUT_PULLUP);
  pinMode(KEY2, INPUT_PULLUP);
  pinMode(5,OUTPUT);//指示灯
  pinMode(8,OUTPUT);//beeWIFI_AIRLINK成功报警提示这里是配网提示
  pinMode(9,OUTPUT);//接继电器
  digitalWrite(5,LOW);
  digitalWrite(8,LOW);
  digitalWrite(9,HIGH);
  myGizwits.begin();
}
void loop() {  
   KEY_Handle();//key handle , network configure网络配置
  wifiStatusHandle();//WIFI Status Handle无线网络状态处理
  unsigned long varW_back = 0;//Add Sensor Data Collection
  myGizwits.write(VALUE_back, varW_back);
  bool varR_on_off = 0;
  if(myGizwits.hasBeenSet(EVENT_on_off))
  {
    myGizwits.read(EVENT_on_off,&varR_on_off);//Address for storing data
    //////////////////////////////////////////////////////////////////////控制区
     if(varR_on_off==1)
    {
      digitalWrite(9,LOW);
      }
     else
     digitalWrite(9,HIGH);
////////////////////////////////////////////////////////////////////////////////下面是定时的代码，暂且没有写定时的程序，先不管。
  }
  unsigned long varR_time_h = 0;
  if(myGizwits.hasBeenSet(EVENT_time_h))
  {
    myGizwits.read(EVENT_time_h,&varR_time_h);//Address for storing data
    mySerial.println(F("EVENT_time_h"));
    mySerial.println(varR_time_h,DEC);
  }
  unsigned long varR_time_m = 0;
  if(myGizwits.hasBeenSet(EVENT_time_m))
  {
    myGizwits.read(EVENT_time_m,&varR_time_m);//Address for storing data
    mySerial.println(F("EVENT_time_m"));
    mySerial.println(varR_time_m,DEC);
  }
  //////////////////////////////////////////////////////////////////////////
  myGizwits.process();
}
```

> ![引用块内容](http://img.blog.csdn.net/20180317150427416?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dpdGNoX2xvdmVfY2FzZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
> 大功告成，装机调试，稳定运行，哎呦累死我了，写了好久，
> 既然能控制一个设备了，哪2个呢？8个呢？
> ![这里写图片描述](http://img.blog.csdn.net/20180317150440013?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dpdGNoX2xvdmVfY2FzZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
> 肯定不是问题喽。
> 

```
好了教程到此结束，累死了，有什么疑问欢迎下方留言，有问必答！
```

