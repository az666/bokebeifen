---
title: python 爬虫制作校园网一键登录软件
tags: python
---

----------

python爬虫制作校园网一键登录软件

----------

> 登录页面，与成功页面
> ![登录页面](https://i.loli.net/2018/05/08/5af1621e59d74.png)
>
> ![成功页面](https://i.loli.net/2018/05/08/5af1636b892ef.jpg)

----------
<!--more-->

> ![调试页面](https://i.loli.net/2018/05/08/5af163fe8160e.png)

----------
> 总结：
> 首先呢思路和普通的post登录原理一样，而且，我也做过手机端的，但是除此调试并没有成功，不知为何。
> 首先post抓包，然后再模拟浏览器发送，这是很普通的操作
> 之后就是对内容的处理了，这里也学到了很多东西，包括html网页的解析，网页源码的处理等等，正则表达式也用到了一些[莫烦python](https://morvanzhou.github.io/)莫烦老师的课程也是非常棒的，教会了我很多知识，
> 最后我的小软件运行了几天之后出问题了，就是校园网每隔几天会换一下ip地址，这使得之前保存下来的ip就不能用了，这让我也搞了好一会儿，最终还是巧妙的查到了更换的ip实现了自动捕捉ip应该可以长期使用了。
> 哎呀，还是自己太懒，学的太慢，也特想自己快速的学东西，但是欲速则不达，有些东西还是要脚踏实地的去做才可以。
> 



----------


代码放在这里一份吧，留作参考[coding仓库项目](https://coding.net/u/pengwenzheng/p/python_papapa/git/blob/master/xiaoyuandenglu.py?public=true)

```
# -*- coding: UTF-8 -*-
from bs4 import BeautifulSoup
from urllib import request
from urllib import parse
import json
import easygui
import chardet
import re
"""
Request_URL = 'http://1.1.1.1:801/eportal/?c=ACSetting&a=Login&protocol=http:&hostname=1.1.1.1&iTermType=1&wlanuserip=10.133.173.186&wlanacip=10.10.9.200&mac=00-00-00-00-00-00&ip=10.133.173.186&enAdvert=0&queryACIP=0&loginMethod=1'
Request_URL = 'http://1.1.1.1:801/eportal/?c=ACSetting&a=Login&protocol=http:&hostname=1.1.1.1&iTermType=1&wlanuserip='+dongtai_ip()+'&wlanacip=10.10.9.200&mac=00-00-00-00-00-00&ip=10.133.173.186&enAdvert=0&queryACIP=0&loginMethod=1'
"""
def yulu ():
    yulu = "http://word.rainss.cn/api_system.php?type=txt"
    response = request.urlopen(yulu)
    html = response.read().decode('utf-8')
    #print(str(html))
def dongtai_ip ():
    url = 'http://1.1.1.1/'
    response3 = request.urlopen(url)
    html = response3.read().decode('gb2312')
    soup = BeautifulSoup(html, 'lxml')
    #  正则表达式寻找字符
    jieguo = re.findall("v46m=0;v4ip='(.*)';v6ip='::", html)
    jieguo2 = re.findall("m46=0;v46ip='(.*)'", html)
    #print(html)
   # print(str(jieguo2))
    if jieguo2:
        print(jieguo2[0])
        return jieguo2[0]
    else:
        print(jieguo[0])
        return jieguo[0]
   # print(str(jieguo))
    # 用beautiful soup 测试
    #print(soup.prettify())
    #print(soup.title.string)
def post_denglu():
    msg = "请输入运营商，账号，密码(此窗口只会出现一次**版本号1.0)"
    title = "校园网一键登录-阿正原创"
    user_info = []
    user_info = easygui.multpasswordbox(msg, title, ("运营商", "账号", "密码"))
    #print(user_info)
    #print(user_info[0])
    #对应上图的Request URL
    test_url = 'http://1.1.1.1/'
    #创建Form_Data字典，存储上图的Form Data
    Form_Data = {}
    Request_URL = 'http://1.1.1.1:801/eportal/?c=ACSetting&a=Login&protocol=http:&hostname=1.1.1.1&iTermType=1&wlanuserip=' + dongtai_ip() + '&wlanacip=10.10.9.200&mac=00-00-00-00-00-00&ip=10.133.173.186&enAdvert=0&queryACIP=0&loginMethod=1'
    fuhao = ",0,"
    zhanghao = user_info[1]
    yunyingshang = "@cmcc"
    Form_Data['DDDDD'] = zhanghao+yunyingshang
    Form_Data['upass'] = user_info[2]
    Form_Data['R1'] = '0'
    Form_Data['R2'] = '0'
    Form_Data['R3'] = '0'
    Form_Data['R6'] = '0'
    Form_Data['para'] = '00'
    Form_Data['0MKKey'] = "123456"
    #使用urlencode方法转换标准格式
    data = parse.urlencode(Form_Data).encode('utf-8')
    #传递Request对象和转换完格式的数
    response = request.urlopen(Request_URL,data)
    response2 = request.urlopen(test_url)
    #print(response.getcode())
    # 判断网页的编码
    bianma = chardet.detect(response2.read())
    #print(bianma)
    bianma = bianma.get("encoding","bianma")
   # print(bianma)
    #读取信息并解码
    html = response.read().decode(bianma)
    #print(html)
    soup = BeautifulSoup(html,'lxml')
   # print(soup.prettify())
   # print(soup.title.string)
    if soup.title.string == "认证成功页":
        yulu = "http://word.rainss.cn/api_system.php?type=txt"
        response4 = request.urlopen(yulu)
        yulu_txt = response4.read().decode('utf-8')
     #   print(str(yulu_txt))
        easygui.buttonbox("登录成功您的动态IP为："+dongtai_ip()+"\n"+yulu_txt,image="success.gif",choices=("无敌","寂寞"))
      #  print("登录成功")
        f = open("zhanghao.txt", "w")
        for i in user_info:
            json_i = json.dumps(i)
            f.write(json_i+"\n")
        f.close()
    else:
        easygui.msgbox("登录失败")
    ##UI设计
def gogogo():
    # 利用json读取数据
    jiance_result = []
    with open("zhanghao.txt", "r") as f:
        jiance_jieguo = f.read().split('\n')[:-1]
        for x in jiance_jieguo:
            json_x = json.loads(x)
            jiance_result.append(json_x)
   # print(jiance_result)
    #print(jiance_result[1])
    f.close()
    if jiance_result[1]=='':
        post_denglu()
    else:
        test_url = 'http://1.1.1.1/'
         # 创建Form_Data字典，存储上图的Form Data
        Form_Data = {}
        Request_URL = 'http://1.1.1.1:801/eportal/?c=ACSetting&a=Login&protocol=http:&hostname=1.1.1.1&iTermType=1&wlanuserip=' + dongtai_ip() + '&wlanacip=10.10.9.200&mac=00-00-00-00-00-00&ip=10.133.173.186&enAdvert=0&queryACIP=0&loginMethod=1'
        zhanghao = jiance_result[1]
        yunyingshang = "@cmcc"
        Form_Data['DDDDD'] = zhanghao + yunyingshang
        Form_Data['upass'] = jiance_result[2]
        Form_Data['R1'] = '0'
        Form_Data['R2'] = '0'
        Form_Data['R3'] = '0'
        Form_Data['R6'] = '0'
        Form_Data['para'] = '00'
        Form_Data['0MKKey'] = "123456"
        # 使用urlencode方法转换标准格式
        data = parse.urlencode(Form_Data).encode('utf-8')
        # 传递Request对象和转换完格式的数
        response = request.urlopen(Request_URL, data)
        response2 = request.urlopen(test_url)
        #print(response.getcode())
        if response.getcode() == 200:
            #print("登录成功")
            yulu = "http://word.rainss.cn/api_system.php?type=txt"
            response4 = request.urlopen(yulu)
            yulu_txt = response4.read().decode('utf-8')
           # print(str(yulu_txt))
            easygui.buttonbox("登录成功您的动态IP为："+dongtai_ip()+"\n随机语录：\n"+yulu_txt,image="success.gif",choices=("666","666"))
        # 判断网页的编码
        """
        bianma = chardet.detect(response2.read())
        print(bianma)
        bianma = bianma.get("encoding", "bianma")
        print(bianma)
        # 读取信息并解码
        html = response.read().decode(bianma)
        print(html)
        soup = BeautifulSoup(html, 'lxml')
        print(soup.prettify())
        print(soup.title.string)
        """
gogogo()
#post_denglu()
#dongtai_ip()
#yulu()
```

----------

> 感谢教程，以后也继续努力学习！！
> [莫烦python](https://morvanzhou.github.io/)
> [廖雪峰老师](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)



