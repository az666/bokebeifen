---
title: 微信服务器get反馈
tags: 温湿度
date: 2018-5-12 13:06:00
---

> 昨天无意间发现了一个很好的教程，用于微信的简易反馈，效果还可以，很好用。
> ![硬件端](https://i.loli.net/2018/05/12/5af674213345b.jpg)
> 用到了一个开源免费的服务器，大神总是默默无闻奉献的。
> [Server酱](http://sc.ftqq.com/3.version)
> 具体的教程源于microPython，其实他可以用于几乎所有的平台，无论是硬件和软件都可以的。
> 像app的反馈，bug提交，硬件的数据反馈等等，都是很不错的。
<!--more-->

----------

> 我按照上面的教程做了一个微信温湿度反馈效果还可以。
> ![微信端](https://i.loli.net/2018/05/12/5af674d5e993e.png)

----------

>Python语言实现：
>

----------


> boot.py

```
import network
import utime

pdcn = network.WLAN(network.STA_IF)
pdcn.active(True)
pdcn.connect('maker_space', 'chuangke666')
utime.sleep(5)
if pdcn.isconnected():
    print("WiFi is connected %s."%pdcn.ifconfig()[0])
else:
    pdcn.active(False)
    utime.sleep(5)
    print("WiFi cannot connect.")
```

----------

> main.py

----------

```
# coding=utf-8
import urequests
import dht
import machine
from machine import Pin
import time

class AlarmSystem:
        def __init__(self):
                self.d = dht.DHT11(machine.Pin(5))

        def dht11(self):
                try:
                        self.d.measure()
                        return 'Temp:'+str(self.d.temperature())+'Hum:'+str(self.d.humidity())+'%'

                except:
                        return '0'

        def push(self, result):
                title = "TPYBoardv202"
                content = 'text='+title+'&'+'desp='+result
                url="https://sc.ftqq.com/这里是注册的key.send?%s" % content
                r = urequests.get(url)
                r.close()

p2=Pin(2,Pin.OUT)
a = AlarmSystem()

def SendData():
        p2.value(not p2.value())
        data_= a.dht11()
	print(data_)
        if(data_!='0'):
                print(data_)
                a.push(data_)
        else:
                print('GET Data Fail')

if __name__ == '__main__':

        while True:
                SendData()
                time.sleep(300)
```