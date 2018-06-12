---
title: 树莓派+百度api实现人脸识别
tags: 树莓派
date: 2018-5-31 20:06:00
---


----------
## 树莓派对接百度api ##

> ![树莓派实现人脸识别](https://i.loli.net/2018/05/31/5b0fedc7d7810.jpg)
> 我以前玩安卓的时候一直用的讯飞的平台和api，对于百度的api很陌生，也很少用，
>今年百度开发平台提出了“所有功能免费”的口号，确实，其他平台的开放都是局限的。有些需要开会员，基础的功能能免费是最好的了。
<!--more-->

----------


![树莓派zerow](https://i.loli.net/2018/05/31/5b0fedc76fa9c.jpg)


----------

> 之前，我用python做过face++的人脸识别，效果还是不错的，后来也在学校进行了展览，face++的平台可是支付宝用的呀，所以也是很强大的。
> 后来买了树莓派，一直想用opencv自己做，可是opencv装了很久，貌似一直出问题，迟迟不能解决，非常吃力。
> 今天遇到了一个教程是做的百度api，就想跟着做-----谁曾想，总是不易的，总出问题！！
> [https://github.com/az666/pizerow_facelock/blob/master/face.py](https://github.com/az666/pizerow_facelock/blob/master/face.py)
> 这位大神的资料是百度API2.0的教程，可是我登录百度开发者平台发现现在已经是api3.0了。
> 只能自己照着官方的文档，一点一点的调，最终成功，效果还可以，和笔记本上的python同时实现了“人脸搜索”（api2.0叫做人脸查找）
> 


----------


> [百度文档中心](https://ai.baidu.com/docs#/)
> 后台数据：
![后台数据](https://i.loli.net/2018/05/31/5b0ff1a90ec04.png)


----------

> ![电脑python实现](https://i.loli.net/2018/05/31/5b0ff3d3e02fa.png)
> 电脑端的输出结果为：
> 

```
D:\python_64_projects\venv\Scripts\python.exe D:/python_64_projects/pizreow.py
{'error_code': 0, 'error_msg': 'SUCCESS', 'log_id': 3049016445, 'timestamp': 1527771832, 'cached': 0, 'result': {'face_token': '08c78a3239ad1d06548ec031fbb7f320', 'user_list': [{'group_id': 'wenzheng', 'user_id': 'wenzheng', 'user_info': 'pengwenzheng', 'score': 98.010856628418}]}}
```

> 可见：相似度为：'user_info': 'pengwenzheng', 'score': 98.010856628418
> 注：*python 3.x中urllib库和urilib2库合并成了urllib库。。其中urllib2.urlopen()变成了urllib.request.urlopen().......urllib2.Request()变成了urllib.request.Request()*
> 


----------


> 树莓派代码
> 


----------

```
def search ():
    '''
    人脸搜索
    '''
    f = open("E:/opencv_pictures/face++/image/my_face.jpg", 'rb')
    img = base64.b64encode(f.read())
    request_url = "https://aip.baidubce.com/rest/2.0/face/v3/search"
    params = {"image":img,"image_type":"BASE64","group_id_list":"wenzheng","quality_control":"LOW","liveness_control":"NORMAL"}
    access_token = '24.1d38fa613271b16392ddf5bad969480b.2592000.1530352882.282335-11330742'
    request_url = request_url + "?access_token=" + access_token
    response = requests.post(request_url, data=params)
    test = response.json().get('score')
    print(response.json())
    print(test)
search()
```